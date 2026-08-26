V2Ray & OpenClash Custom Ruleset GeneratorRepositori ini menyediakan berkas kompilasi harian otomatis geosite.dat dan geoip.dat yang dioptimalkan untuk OpenClash, Mihomo (Clash Meta), Sing-box, dan V2Ray/Xray.Proyek ini dirancang untuk memprioritaskan performa routing, pemblokiran iklan yang intensif, keandalan konektivitas perbankan Indonesia, serta kebebasan penuh dari ketergantungan infrastruktur pihak ketiga.🚀 Tautan Unduhan Langsung (Direct Downloads)Gunakan tautan rilis terbaru berikut langsung pada konfigurasi OpenClash, V2Ray, atau skrip pembaruan otomatis Anda:BerkasTautan Unduhan Rilis Terbarugeosite.dat[https://github.com/jadahmambu/v2ray-rules-dat/releases/latest/download/geosite.dat](https://github.com/jadahmambu/v2ray-rules-dat/releases/latest/download/geosite.dat)geoip.dat[https://github.com/jadahmambu/v2ray-rules-dat/releases/latest/download/geoip.dat](https://github.com/jadahmambu/v2ray-rules-dat/releases/latest/download/geoip.dat)🏷️ Daftar Tag Geosite yang TersediaSeluruh domain disaring, dibersihkan dari duplikat (deduplicated), dan dikompilasi ke dalam tag-tag berikut:Nama TagDeskripsi & Sumber DomainPeruntukan Aksesrule-adsPemblokiran iklan dasar & trackers (Turtlecute33 D3Host + Jadahmambu).REJECT / Blockads-extraPemblokiran iklan tingkat lanjut & malware/phishing (OISD Full + AdGuard DNS + AntiScam jarelllama & Discord-AntiScam).REJECT / Blockbank-idDomain Perbankan Indonesia, FinTech, & E-Wallet (BCA, Mandiri, BRI, BNI, GoPay, OVO, Dana, ShopeePay, dll).DIRECTrule-ecoDomain ekosistem, update sistem (OPPO, ColorOS, Avast), dan kustomasi direktori lokal (rule_direct.txt).DIRECTrule-microsoftLayanan & ekosistem Microsoft (Windows Update, Office365, Azure, Teams).DIRECT / ProxysosmedMedia Sosial populer (Facebook, Instagram, TikTok, Twitter/X, WhatsApp).Proxy / DIRECTstreamingPlatform Streaming Video & Musik (YouTube, Netflix, Disney+, Spotify).Proxy / DIRECTvidconferenceAplikasi Konferensi Video (Zoom, Google Meet, Microsoft Teams).DIRECT🛠️ Contoh Penggunaan Konfigurasi1. OpenClash / Mihomo (Clash Meta)Tambahkan ke dalam bagian rules: pada berkas config.yaml OpenClash Anda:YAMLrules:
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
2. V2Ray / Xray (config.json)JSON"routing": {
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
🔄 Pembaruan OtomatisProyek ini berjalan secara otomatis melalui GitHub Actions setiap hari pada pukul 00:30 WIB (17:30 UTC) untuk menyedot data up-to-date dari seluruh sumber utama, membuang duplikasi, serta memperbarui berkas di halaman GitHub Releases.🤝 Kredit Sumber Upstream
