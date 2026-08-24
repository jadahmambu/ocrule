# Custom V2Ray Rules Dat (Ultra-Lightweight)

Repositori ini menyediakan berkas kompilasi aturan `geosite.dat` dan `geoip.dat` versi **ringan (ultra-lightweight)** yang diperbarui secara otomatis setiap hari via GitHub Actions.

Dirancang khusus untuk router/STB (OpenWrt, OpenClash, PassWall, ShadowSocksR Plus+) maupun aplikasi desktop/mobile (v2rayN, Matsuri, Nekobox) agar efisien dalam penggunaan memori (RAM) tanpa mengorbankan fungsi pemblokiran iklan dan rute trafik harian.

---

## 🔗 Tautan Unduhan Langsung (Direct Download)

Gunakan URL rilis langsung di bawah ini untuk memperbarui aturan secara otomatis di aplikasi/router Anda:

| Berkas | Deskripsi | Tautan Unduhan (URL) |
| :--- | :--- | :--- |
| **`geosite.dat`** | Aturan Domain (Iklan, Sosmed, Streaming, dll.) | `https://github.com/USERNAME/REPO_NAME/releases/latest/download/geosite.dat` |
| **`geoip.dat`** | Aturan IP (Indonesian IPs & Private Networks) | `https://github.com/USERNAME/REPO_NAME/releases/latest/download/geoip.dat` |

> *Catatan: Ganti `USERNAME/REPO_NAME` dengan nama username dan repositori GitHub Anda.*

---

## 🏷️ Tag Geosite yang Tersedia

Anda dapat menggunakan tag-tag berikut dalam konfigurasi routing client (Clash / V2Ray / Xray):

| Tag Geosite | Sumber / Deskripsi Aturan | Kegunaan Utama |
| :--- | :--- | :--- |
| `geosite:rule-ads` | Extended Ad Block List | Memblokir iklan, tracker, dan analytics |
| `geosite:antiscam` | Anti-Scam & Phishing List | Memblokir situs penipuan, judi, dan malware |
| `geosite:bank-id` | Perbankan & Fintek Indonesia | Rute langsung (DIRECT) untuk transaksi bank aman |
| `geosite:sosmed` | WhatsApp, Instagram, Facebook, TikTok, X, dll. | Rute khusus media sosial |
| `geosite:streaming` | YouTube, Netflix, Disney+, Viu, Vidio, dll. | Rute khusus layanan video/music streaming |
| `geosite:vidconference` | Zoom, Google Meet, Teams, Webex, dll. | Rute prioritas/bebas hambatan untuk vicon |
| `geosite:rule-microsoft` | Microsoft Services, Office365, Azure, Windows Update | Rute layanan Microsoft |
| `geosite:rule-eco` | E-commerce (Tokopedia, Shopee, Lazada, Blibli, dll.) | Rute belanja online lokal |

---

## ⚙️ Contoh Penggunaan Konfigurasi

### 1. OpenClash / Clash (Rule Provider)

```yaml
rule-providers:
  rule-ads:
    type: http
    behavior: domain
    url: "https://raw.githubusercontent.com/USERNAME/REPO_NAME/master/community/data/rule-ads"
    path: ./rule_provider/rule-ads.yaml
    interval: 86400

rules:
  # Pemblokiran Iklan & Scam
  - GEOSITE,rule-ads,REJECT
  - GEOSITE,antiscam,REJECT
  
  # Rute Domestik / Direct
  - GEOSITE,bank-id,DIRECT
  - GEOSITE,rule-eco,DIRECT
  
  # Rute Traffic Spesifik (Ke Proxy)
  - GEOSITE,sosmed,Proxy-Sosmed
  - GEOSITE,streaming,Proxy-Streaming
  - GEOSITE,vidconference,DIRECT
  
  # Fallback IP & Final
  - GEOIP,private,DIRECT,no-resolve
  - GEOIP,id,DIRECT
  - MATCH,GLOBAL
```

---

### 2. Xray / V2Ray (Config JSON)

```json
"routing": {
  "domainStrategy": "IPIfNonMatch",
  "rules": [
    {
      "type": "field",
      "outboundTag": "blocked",
      "domain": [
        "geosite:rule-ads",
        "geosite:antiscam"
      ]
    },
    {
      "type": "field",
      "outboundTag": "direct",
      "domain": [
        "geosite:bank-id",
        "geosite:rule-eco",
        "geosite:vidconference"
      ],
      "ip": [
        "geoip:private",
        "geoip:id"
      ]
    },
    {
      "type": "field",
      "outboundTag": "proxy",
      "domain": [
        "geosite:sosmed",
        "geosite:streaming"
      ]
    }
  ]
}
```

---

## 🔄 Pembaruan Otomatis

Aturan ini dikompilasi secara otomatis menggunakan **GitHub Actions** setiap hari pada pukul **00:30 WIB** (`30 17 * * * UTC`).

## 📜 Lisensi & Kredit

Aturan ini mengompilasi data dari berbagai proyek *open-source*:
- [domain-list-community](https://github.com/v2fly/domain-list-community)
- [malikshi/v2ray-rules-dat](https://github.com/malikshi/v2ray-rules-dat)
- [jadahmambu/ocrule](https://github.com/jadahmambu/ocrule)
