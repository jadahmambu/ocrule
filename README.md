# V2Ray Rules Dat (Custom Geosite & GeoIP Build)

Repositori ini secara otomatis mengompilasi dan memperbarui berkas `geosite.dat` dan `geoip.dat` secara harian menggunakan **GitHub Actions**. 

Dioptimalkan khusus untuk **OpenWrt / OpenClash / Mihomo Core**, dengan fokus pada **kecepatan kompilasi native (AWK/SED)**, pembersihan syntax invalid (wildcards, trailing dots, double hyphens), serta **efisiensi memori RAM**.

---

## 🌟 Fitur Utama

- ⚡ **Super Fast Build Engine:** Pemrosesan ratusan ribu domain menggunakan `awk` & `sed` native (waktu *run* hanya ~30-60 detik).
- 🧹 **Rigorously Sanitized:** Otomatis membersihkan wildcard (`*`), trailing dots (`.`), format non-RFC, dan duplikat domain.
- 🛡️ **All-in-One Ads & Security (`ads-extra`):** Menggabungkan OISD Full, AdGuard DNS Filter, dan Malikshi Antiscam ke dalam 1 tag tunggal untuk efisiensi RAM router.
- 🏦 **Clean Banking Routing (`bank-id`):** Pembersihan circular include dan manipulasi syntax agar transaksi bank/e-wallet Indonesia tidak terdeteksi proxy.
- 🔄 **Automated Daily Release:** Diperbarui secara otomatis setiap hari pukul 00:30 WIB (17:30 UTC).

---

## 📦 Isi & Ringkasan Tag `geosite.dat`

| Tag Geosite | Sumber / Deskripsi | Aksi Rekomendasi di OpenClash |
| :--- | :--- | :--- |
| **`rule-ads`** | Iklan Utama (Malikshi + Jadahmambu Adsblock) | `REJECT` |
| **`ads-extra`** | **Super-Blocklist:** OISD Full + AdGuard DNS Filter + Malikshi Antiscam (Iklan, Tracker, Malware, Phishing, Judol) | `REJECT` |
| **`bank-id`** | Perbankan ID & E-Wallet (BCA, Mandiri, BRI, DANA, dll) | `DIRECT` |
| **`sosmed`** | Media Sosial (Jadahmambu) | `HK-VPN` / `Proxy` |
| **`streaming`** | Platform Streaming (Jadahmambu) | `HK-VPN` / `Proxy` |
| **`vidconference`** | Zoom, Teams, Meet (Jadahmambu) | `HK-VPN` / `Proxy` |
| **`rule-microsoft`**| Layanan Microsoft & Windows Update | `DIRECT` |
| **`rule-eco`** | Bypass Ekonomi / Saklar khusus | `DIRECT` / `Eco Mode` |
| **`netflix`** | Bawaan V2Fly DLC (Sangat presisi) | `HK-VPN` / `Proxy` |

---

## 🚀 Tautan Unduhan Langsung (Direct URL)

Gunakan tautan berikut untuk dimasukkan ke dalam `rule-providers` OpenClash Anda:

* **Geosite:**  
  `https://github.com/USERNAME/REPO_ANDA/releases/latest/download/geosite.dat`
* **GeoIP:**  
  `https://github.com/USERNAME/REPO_ANDA/releases/latest/download/geoip.dat`

*(Ganti `USERNAME/REPO_ANDA` sesuai nama akun dan repositori GitHub Anda)*

---

## 🛠️ Contoh Integrasi `config.yaml` OpenClash

```yaml
rule-providers:
  my-geosite:
    type: http
    behavior: domain
    format: mrs
    url: "[https://github.com/USERNAME/REPO_ANDA/releases/latest/download/geosite.dat](https://github.com/USERNAME/REPO_ANDA/releases/latest/download/geosite.dat)"
    path: ./rule_provider/geosite.dat
    interval: 86400

rules:
  # 1. Pengecualian Akses Lokal/LAN
  - IP-CIDR,198.18.0.1/16,REJECT,no-resolve
  - GEOIP,private,DIRECT,no-resolve

  # 2. Pengecualian Khusus (Direct Dulu Sebelum Filter Iklan)
  - DOMAIN-SUFFIX,googlesyndication.com,Direct

  # 3. Logika Saklar Mihomo Core
  - AND,((OR,((RULE-SET,EcoMode),(GEOSITE,rule-eco),(GEOIP,facebook))),(RULE-SET,BlockClient)),Eco Mode
  - RULE-SET,BlockClient,BlockClient

  # 4. Pemblokiran Massal (Iklan, Scam, NSFW & IP Malware)
  - GEOSITE,rule-ads,REJECT
  - GEOSITE,ads-extra,REJECT
  - RULE-SET,Block,REJECT
  - GEOIP,malware,REJECT,no-resolve
  - GEOIP,phishing,REJECT,no-resolve

  # 5. Aturan Unblock & Perbankan
  - GEOSITE,rule-microsoft,Direct
  - RULE-SET,Unblock,Unblock
  - GEOSITE,bank-id,Direct
  - RULE-SET,Direct,Direct

  # 6. Routing Aplikasi Ke HK-VPN
  - GEOSITE,netflix,HK-VPN
  - GEOSITE,sosmed,HK-VPN
  - GEOSITE,streaming,HK-VPN
  - GEOSITE,vidconference,HK-VPN

  # 7. Routing GEOIP Ke HK-VPN (Dengan Optimasi no-resolve)
  - GEOIP,telegram,HK-VPN,no-resolve
  - GEOIP,facebook,HK-VPN,no-resolve
  - GEOIP,google,HK-VPN,no-resolve
  - GEOIP,id,HK-VPN,no-resolve

  # 8. Fallback Utama
  - MATCH,HK-VPN
