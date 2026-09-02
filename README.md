# Custom V2Ray Rules Dat Generator

Pipa otomatisasi berbasis GitHub Actions untuk membuat berkas `geosite.dat` dan `geoip.dat` yang ringan, efisien, dan dikonsolidasikan khusus untuk **OpenClash / Mihomo Core** pada perangkat dengan spesifikasi atau memori terbatas (seperti STB OpenWrt).

---

## 🚀 Fitur Utama

- **`rule-ads` Terkonsolidasi Total:** Menggabungkan *AdGuard DNS Filter*, *StevenBlack Porn List*, *AntiScam (Jarell & Discord)*, *D3Host*, dan daftar blokir lokal ke dalam **satu tag tunggal**.
- **Ringan & Hemat RAM:** Menggunakan sumber `geoip.dat` terkompresi dari **MetaCubeX** (~3.5–4 MB) untuk efisiensi tinggi pada router/STB.
- **Pembersihan Otomatis (*Automated Deduplication & Dependency Patching*):** Menghapus domain duplikat secara otomatis saat kompilasi dan menambal dependensi `include:` agar tidak pernah terjadi kegagalan *build*.
- **Pembaruan Otomatis:** Berkas diperbarui secara otomatis setiap hari via GitHub Actions (*cron schedule*).

---

## 🏷️ Daftar Tag Geodata

### 1. Tag GEOSITE (`geosite.dat`)

| Tag Geosite | Sumber & Cakupan | Rekomendasi Action |
| :--- | :--- | :--- |
| **`rule-ads`** | AdGuard DNS + StevenBlack Porn + AntiScam + D3Host + `adsblock.txt` lokal | `REJECT` |
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
```

---

## 📦 Unduh Rilis Berkas `.dat`

Anda dapat mengunduh berkas kompilasi terbaru secara langsung melalui menu **Releases**:

- **`geosite.dat`** $
ightarrow$ `https://github.com/<username>/<repo>/releases/latest/download/geosite.dat`
- **`geoip.dat`** $
ightarrow$ `https://github.com/<username>/<repo>/releases/latest/download/geoip.dat`

---

## 📄 Lisensi & Sumber Daya

Proyek ini disusun dan mengompilasi data dari berbagai proyek *open-source*:
- Compiler: [v2fly/domain-list-community](https://github.com/v2fly/domain-list-community)
- GeoIP Source: [MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat)
- AdGuard DNS: [AdGuard Filter](https://adguard.com/)
- Adult Blocklist: [StevenBlack Hosts](https://github.com/StevenBlack/hosts)
- Scam Lists: [Jarell Scam Blocklist](https://github.com/jarelllama/Scam-Blocklist) & [Discord AntiScam](https://github.com/Discord-AntiScam/scam-links)
