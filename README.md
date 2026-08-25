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

---

Terima kasih kepada para penyedia sumber data domain:
* 🌐 **Malikshi:** [v2ray-rules-dat](https://github.com/malikshi/v2ray-rules-dat) | [Antiscam](https://github.com/malikshi/antiscam)
* 🌐 **Jadahmambu:** [ocrule](https://github.com/jadahmambu/ocrule)
* 🛡️ **OISD Blocklist:** [oisd.nl](https://oisd.nl)
* 🛡️ **AdGuard Team:** [AdGuardSDNSFilter](https://github.com/AdguardTeam/AdGuardSDNSFilter)

