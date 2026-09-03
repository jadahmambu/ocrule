# Custom V2Ray Rules Dat Generator

Pipa otomatisasi berbasis GitHub Actions untuk membuat berkas `geosite.dat` dan `geoip.dat` yang ringan, efisien, dan dikonsolidasikan khusus untuk **OpenClash / Mihomo Core** pada perangkat dengan spesifikasi atau memori terbatas (seperti STB OpenWrt B760H).

---

## 🚀 Fitur Utama

- **`rule-ads` Terkonsolidasi Total:** Menggabungkan *AdGuard DNS Filter*, *StevenBlack Porn List*, *OGAH / TrustPositif Komdigi ID*, *v2fly Category Ads ID*, *D3Host*, dan *adsblock.txt* lokal ke dalam **satu tag tunggal**.
- **Dioptimalkan untuk Indonesia:** Menggunakan sumber penipuan, *phishing*, judi online, dan iklan lokal Indonesia aktif sebagai pengganti daftar *scam* global.
- **Sangat Ringan & Hemat RAM (~5 MB):** Memangkas berkas dari ukuran umum (~17 MB) dengan membuang domain global yang tidak dipakai, menghemat hingga 50 MB penggunaan RAM pada STB.
- **`geoip.dat` Ringan dari MetaCubeX (~3.5 MB):** Mendukung penuh tag `geoip:facebook`, `geoip:telegram`, `geoip:google`, `geoip:id`, dan `geoip:private`.
- **Pembersihan Otomatis (*Automated Deduplication & Dependency Patching*):** Menghapus domain duplikat secara otomatis saat kompilasi dan menambal dependensi `include:` agar tidak pernah terjadi kegagalan *build*.
- **Pembaruan Otomatis:** Berkas diperbarui secara otomatis setiap hari via GitHub Actions (*cron schedule*).

---

## 🏷️ Daftar Tag Geodata

### 1. Tag GEOSITE (`geosite.dat`)

| Tag Geosite | Sumber & Cakupan | Rekomendasi Action |
| :--- | :--- | :--- |
| **`rule-ads`** | AdGuard DNS + StevenBlack Porn + OGAH/TrustPositif ID + Category Ads ID + D3Host + `adsblock.txt` lokal | `REJECT` |
| **`bank-id`** | Domain perbankan & *financial* Indonesia (`rule_bank.txt`) | `Direct` / `DIRECT` |
| **`rule-eco`** | Domain hemat/sistem (`rule_eco.txt` + `rule_direct.txt`) | `HK-VPN` / `DIRECT` |
| **`rule-microsoft`** | Ekosistem & layanan Microsoft (`rule_microsoft.txt`) | `Direct` / `DIRECT` |
| **`sosmed`** | Domain media sosial (`rule_sosmed.txt`: FB, IG, WA, TikTok, X, dll.) | `HK-VPN` / Proxy |
| **`streaming`** | Layanan media streaming (`rule_streaming.txt`: YT, Netflix, Disney+, dll.) | `HK-VPN` / Proxy |
| **`vidconference`** | Aplikasi konferensi video (`rule_videoconference.txt`: Zoom, Meet, Teams) | `HK-VPN` / `DIRECT` |

### 2. Tag GEOIP (`geoip.dat`)

| Tag GeoIP | Cakupan IP | Rekomendasi Action |
| :--- | :--- | :--- |
| **`private`** | IP LAN / Router lokal (192.168.x.x, 10.x.x.x, 127.0.0.1) | `DIRECT` |
| **`facebook`** | Rentang IP server Meta (Facebook, Instagram, WhatsApp) | `HK-VPN` / `DIRECT` |
| **`telegram`** | Rentang IP server Telegram | `HK-VPN` / `DIRECT` |
| **`google`** | Rentang IP infrastruktur Google | `HK-VPN` / `DIRECT` |
| **`id`** | Seluruh alokasi IP negara Indonesia | `HK-VPN` / `DIRECT` |

---

## ⚙️ Contoh Penggunaan di OpenClash (`config.yaml`)

```yaml
rules:
  # 1. IP Network Lokal (Bypass Instan)
  - GEOIP,private,DIRECT

  # 2. Saklar Kondisional Mihomo / BlockClient (Opsional)
  - AND,((OR,((RULE-SET,EcoMode),(GEOIP,facebook))),(RULE-SET,BlockClient)),Eco Mode
  - RULE-SET,BlockClient,BlockClient

  # 3. Filter Pemblokiran Utama (Terpusat)
  - GEOSITE,rule-ads,REJECT

  # 4. Filter Domain & IP Akses Langsung (Direct)
  - GEOSITE,rule-microsoft,Direct
  - GEOSITE,bank-id,Direct
  - RULE-SET,Direct,Direct

  # 5. Pengarahan Trafik Spesifik ke HK-VPN / Proxy Group
  - GEOSITE,sosmed,HK-VPN
  - GEOSITE,streaming,HK-VPN
  - GEOSITE,vidconference,HK-VPN
  - GEOSITE,rule-eco,HK-VPN

  # 6. Pengarahan Berdasarkan GEOIP
  - GEOIP,telegram,HK-VPN,no-resolve
  - GEOIP,facebook,HK-VPN,no-resolve
  - GEOIP,google,HK-VPN,no-resolve
  - GEOIP,id,HK-VPN,no-resolve

  # Match Sisa Trafik
  - MATCH,HK-VPN
