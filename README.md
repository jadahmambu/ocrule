# V2Ray & OpenClash Custom Ruleset Generator

[![Build V2Ray rules dat files](https://github.com/jadahmambu/ocrule/actions/workflows/run.yml/badge.svg)](https://github.com/jadahmambu/ocrule/actions/workflows/run.yml)
[![GitHub Release](https://img.shields.io/github/v/release/jadahmambu/ocrule?color=blue&label=Latest%20Release)](https://github.com/jadahmambu/ocrule/releases/latest)

Repositori ini menyediakan berkas kompilasi harian otomatis `geosite.dat` dan `geoip.dat` yang dioptimalkan untuk **OpenClash**, **Mihomo (Clash Meta)**, **Sing-box**, dan **V2Ray/Xray**.

Proyek ini dirancang untuk memprioritaskan performa routing, pemblokiran iklan yang intensif, keandalan konektivitas perbankan Indonesia, serta kebebasan penuh dari ketergantungan infrastruktur pihak ketiga.

---

## 🚀 Tautan Unduhan Langsung (Direct Downloads)

Gunakan tautan rilis terbaru berikut langsung pada konfigurasi OpenClash, V2Ray, atau skrip pembaruan otomatis Anda:

| Berkas | Tautan Unduhan Rilis Terbaru |
| :--- | :--- |
| **`geosite.dat`** | `https://github.com/jadahmambu/ocrule/releases/latest/download/geosite.dat` |
| **`geoip.dat`** | `https://github.com/jadahmambu/ocrule/releases/latest/download/geoip.dat` |

---

## 🏷️ Daftar Tag Geosite yang Tersedia

Seluruh domain disaring, dibersihkan dari duplikat (*deduplicated*), dan dikompilasi ke dalam tag-tag berikut:

| Nama Tag | Deskripsi & Sumber Domain | Peruntukan Akses |
| :--- | :--- | :--- |
| **`rule-ads`** | Pemblokiran iklan dasar & *trackers* (Turtlecute33 D3Host + Jadahmambu). | `REJECT` / `Block` |
| **`ads-extra`** | Pemblokiran iklan tingkat lanjut & malware/phishing (OISD Full + AdGuard DNS + AntiScam jarelllama & Discord-AntiScam). | `REJECT` / `Block` |
| **`bank-id`** | Domain Perbankan Indonesia, FinTech, & E-Wallet (BCA, Mandiri, BRI, BNI, GoPay, OVO, Dana, ShopeePay, dll). | `DIRECT` |
| **`rule-eco`** | Domain ekosistem, update sistem (OPPO, ColorOS, Avast), dan kustomasi direktori lokal (`rule_direct.txt`). | `DIRECT` |
| **`rule-microsoft`** | Layanan & ekosistem Microsoft (Windows Update, Office365, Azure, Teams). | `DIRECT` / Proxy |
| **`sosmed`** | Media Sosial populer (Facebook, Instagram, TikTok, Twitter/X, WhatsApp). | Proxy / `DIRECT` |
| **`streaming`** | Platform Streaming Video & Musik (YouTube, Netflix, Disney+, Spotify). | Proxy / `DIRECT` |
| **`vidconference`** | Aplikasi Konferensi Video (Zoom, Google Meet, Microsoft Teams). | `DIRECT` |

---

## 🛠️ Contoh Penggunaan Konfigurasi

### 1. OpenClash / Mihomo (Clash Meta)
Tambahkan ke dalam bagian **`rules:`** pada berkas `config.yaml` OpenClash Anda:

```yaml
rules:
  # 1. Sinkronisasi Waktu (NTP Wajib Direct)
  - DST-PORT,123,DIRECT

  # 2. Pemblokiran Iklan & Scam
  - GEOSITE,rule-ads,REJECT
  - GEOSITE,ads-extra,REJECT

  # 3. Bypass Perbankan & Ekosistem System (DIRECT)
  - GEOSITE,bank-id,DIRECT
  - GEOSITE,rule-eco,DIRECT
  - GEOSITE,vidconference,DIRECT

  # 4. GEOIP Indonesia
  - GEOIP,id,DIRECT

  # 5. Fallback Utama (VPN/Proxy Anda)
  - MATCH,HK-VPN
```

### 2. V2Ray / Xray (`config.json`)

```json
"routing": {
  "domainStrategy": "IPIfNonMatch",
  "rules": [
    {
      "type": "field",
      "outboundTag": "blocked",
      "geosite": ["rule-ads", "ads-extra"]
    },
    {
      "type": "field",
      "outboundTag": "direct",
      "geosite": ["bank-id", "rule-eco", "vidconference"]
    }
  ]
}
```

---

## 🔄 Pembaruan Otomatis

Proyek ini berjalan secara otomatis melalui **GitHub Actions** setiap hari pada pukul **00:30 WIB (17:30 UTC)** untuk menyedot data *up-to-date* dari seluruh sumber utama, membuang duplikasi, serta memperbarui berkas di halaman **GitHub Releases**.

---

## 🤝 Kredit Sumber Upstream

Terima kasih kepada proyek-proyek *open-source* yang menjadi fondasi kompilasi data ini:

* **Compiler Core:** [v2fly/domain-list-community](https://github.com/v2fly/domain-list-community)
* **GeoIP Data:** [Loyalsoldier/v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat)
* **AdBlock & Trackers:** [Turtlecute33/adblocktest](https://github.com/Turtlecute33/adblocktest), [OISD](https://oisd.nl/), [AdGuard DNS Filter](https://github.com/AdguardTeam/AdGuardSDNSFilter)
* **AntiScam & Phishing:** [jarelllama/Scam-Blocklist](https://github.com/jarelllama/Scam-Blocklist), [Discord-AntiScam/scam-links](https://github.com/Discord-AntiScam/scam-links)
* **Local & Custom Rules:** [jadahmambu/ocrule](https://github.com/jadahmambu/ocrule)

---

## 📜 Lisensi

Lisensi mengikuti aturan dari masing-masing penyedia sumber data *upstream* (MIT / GPL-3.0). Perangkat lunak ini bebas untuk digunakan, di-fork, dan disebarluaskan kembali.
