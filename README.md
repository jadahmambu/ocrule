# Custom V2Ray Rules Generator

Repositori ini berisi berkas `geosite.dat` dan `geoip.dat` terkompilasi yang diperbarui secara otomatis setiap hari menggunakan GitHub Actions.

## Sumber Data (Upstream)
- Compiler Core: v2fly/domain-list-community
- GeoIP Data: Loyalsoldier/v2ray-rules-dat
- AdBlock & Trackers: Turtlecute33/adblocktest, OISD, AdGuard DNS Filter
- AntiScam & Phishing: jarelllama/Scam-Blocklist, Discord-AntiScam/scam-links
- Local & Custom Rules: jadahmambu/ocrule

---

## Tag GEOSITE (geosite.dat)

Gunakan daftar tag ini untuk aturan berbasis domain (GEOSITE) di OpenClash / Mihomo:

| Nama Tag | Deskripsi & Cakupan |
| :--- | :--- |
| rule-ads | Pemblokir iklan, pelacak (tracker), scam, dan phishing. |
| ads-extra | Aturan iklan tambahan dan elemen pelacak sekunder. |
| bank-id | Situs perbankan Indonesia (BCA, Mandiri, BRI, BNI, dll). |
| rule-eco | Domain umum yang direkomendasikan masuk rute DIRECT (termasuk isi rule_direct.txt). |
| rule-microsoft | Layanan dan server pembaruan Microsoft / Windows. |
| sosmed | Media sosial (Facebook, Instagram, WhatsApp, TikTok, Twitter/X). |
| streaming | Layanan streaming video & musik (YouTube, Netflix, Disney+, Spotify). |
| vidconference | Platform rapat virtual (Zoom, Microsoft Teams, Google Meet). |

---

## Tag GEOIP (geoip.dat)

Gunakan daftar tag ini untuk aturan berbasis alamat IP (GEOIP) di OpenClash / Mihomo:

| Nama Tag | Deskripsi & Cakupan |
| :--- | :--- |
| private | IP Lokal/LAN (192.168.x.x, 10.x.x.x, 127.0.0.1, CGNAT 100.64.x.x). |
| id | Seluruh alokasi blok IP publik penyedia internet di Indonesia (Indihome, Telkomsel, XL, Biznet, dll). |
| telegram | Blok IP server pusat dan CDN aplikasi Telegram. |
| netflix | Blok IP server infrastruktur streaming Netflix. |
| google | Blok IP server dan layanan infrastruktur Google. |
| facebook | Blok IP server Meta (Facebook, Instagram, WhatsApp). |
| sg, us, hk, jp | Blok IP publik berdasarkan negara (Singapura, AS, Hong Kong, Jepang, dll). |

---

## Contoh Penggunaan di OpenClash (config.yaml)

```yaml
rules:
  # Aturan IP LAN / Jaringan Lokal
  - GEOIP,private,DIRECT,no-resolve

  # Aturan Geosite Buatan
  - GEOSITE,rule-ads,REJECT
  - GEOSITE,bank-id,DIRECT
  - GEOSITE,rule-eco,DIRECT
  - GEOSITE,sosmed,PROXIES

  # Aturan GeoIP Negara / Layanan
  - GEOIP,id,DIRECT
  - GEOIP,telegram,PROXIES

  # Final Fallback
  - MATCH,PROXIES# Custom V2Ray Rules Generator

Repositori ini berisi berkas `geosite.dat` dan `geoip.dat` terkompilasi yang diperbarui secara otomatis setiap hari menggunakan GitHub Actions.

## Sumber Data (Upstream)
- Compiler Core: v2fly/domain-list-community
- GeoIP Data: Loyalsoldier/v2ray-rules-dat
- AdBlock & Trackers: Turtlecute33/adblocktest, OISD, AdGuard DNS Filter
- AntiScam & Phishing: jarelllama/Scam-Blocklist, Discord-AntiScam/scam-links
- Local & Custom Rules: jadahmambu/ocrule

---

## Tag GEOSITE (geosite.dat)

Gunakan daftar tag ini untuk aturan berbasis domain (GEOSITE) di OpenClash / Mihomo:

| Nama Tag | Deskripsi & Cakupan |
| :--- | :--- |
| rule-ads | Pemblokir iklan, pelacak (tracker), scam, dan phishing. |
| ads-extra | Aturan iklan tambahan dan elemen pelacak sekunder. |
| bank-id | Situs perbankan Indonesia (BCA, Mandiri, BRI, BNI, dll). |
| rule-eco | Domain umum yang direkomendasikan masuk rute DIRECT (termasuk isi rule_direct.txt). |
| rule-microsoft | Layanan dan server pembaruan Microsoft / Windows. |
| sosmed | Media sosial (Facebook, Instagram, WhatsApp, TikTok, Twitter/X). |
| streaming | Layanan streaming video & musik (YouTube, Netflix, Disney+, Spotify). |
| vidconference | Platform rapat virtual (Zoom, Microsoft Teams, Google Meet). |

---

## Tag GEOIP (geoip.dat)

Gunakan daftar tag ini untuk aturan berbasis alamat IP (GEOIP) di OpenClash / Mihomo:

| Nama Tag | Deskripsi & Cakupan |
| :--- | :--- |
| private | IP Lokal/LAN (192.168.x.x, 10.x.x.x, 127.0.0.1, CGNAT 100.64.x.x). |
| id | Seluruh alokasi blok IP publik penyedia internet di Indonesia (Indihome, Telkomsel, XL, Biznet, dll). |
| telegram | Blok IP server pusat dan CDN aplikasi Telegram. |
| netflix | Blok IP server infrastruktur streaming Netflix. |
| google | Blok IP server dan layanan infrastruktur Google. |
| facebook | Blok IP server Meta (Facebook, Instagram, WhatsApp). |
| sg, us, hk, jp | Blok IP publik berdasarkan negara (Singapura, AS, Hong Kong, Jepang, dll). |

---

## Contoh Penggunaan di OpenClash (config.yaml)

```yaml
rules:
  # Aturan IP LAN / Jaringan Lokal
  - GEOIP,private,DIRECT,no-resolve

  # Aturan Geosite Buatan
  - GEOSITE,rule-ads,REJECT
  - GEOSITE,bank-id,DIRECT
  - GEOSITE,rule-eco,DIRECT
  - GEOSITE,sosmed,PROXIES

  # Aturan GeoIP Negara / Layanan
  - GEOIP,id,DIRECT
  - GEOIP,telegram,PROXIES

  # Final Fallback
  - MATCH,PROXIES# Custom V2Ray Rules Generator

Repositori ini berisi berkas `geosite.dat` dan `geoip.dat` terkompilasi yang diperbarui secara otomatis setiap hari menggunakan GitHub Actions.

## Sumber Data (Upstream)
- Compiler Core: v2fly/domain-list-community
- GeoIP Data: Loyalsoldier/v2ray-rules-dat
- AdBlock & Trackers: Turtlecute33/adblocktest, OISD, AdGuard DNS Filter
- AntiScam & Phishing: jarelllama/Scam-Blocklist, Discord-AntiScam/scam-links
- Local & Custom Rules: jadahmambu/ocrule

---

## Tag GEOSITE (geosite.dat)

Gunakan daftar tag ini untuk aturan berbasis domain (GEOSITE) di OpenClash / Mihomo:

| Nama Tag | Deskripsi & Cakupan |
| :--- | :--- |
| rule-ads | Pemblokir iklan, pelacak (tracker), scam, dan phishing. |
| ads-extra | Aturan iklan tambahan dan elemen pelacak sekunder. |
| bank-id | Situs perbankan Indonesia (BCA, Mandiri, BRI, BNI, dll). |
| rule-eco | Domain umum yang direkomendasikan masuk rute DIRECT (termasuk isi rule_direct.txt). |
| rule-microsoft | Layanan dan server pembaruan Microsoft / Windows. |
| sosmed | Media sosial (Facebook, Instagram, WhatsApp, TikTok, Twitter/X). |
| streaming | Layanan streaming video & musik (YouTube, Netflix, Disney+, Spotify). |
| vidconference | Platform rapat virtual (Zoom, Microsoft Teams, Google Meet). |

---

## Tag GEOIP (geoip.dat)

Gunakan daftar tag ini untuk aturan berbasis alamat IP (GEOIP) di OpenClash / Mihomo:

| Nama Tag | Deskripsi & Cakupan |
| :--- | :--- |
| private | IP Lokal/LAN (192.168.x.x, 10.x.x.x, 127.0.0.1, CGNAT 100.64.x.x). |
| id | Seluruh alokasi blok IP publik penyedia internet di Indonesia (Indihome, Telkomsel, XL, Biznet, dll). |
| telegram | Blok IP server pusat dan CDN aplikasi Telegram. |
| netflix | Blok IP server infrastruktur streaming Netflix. |
| google | Blok IP server dan layanan infrastruktur Google. |
| facebook | Blok IP server Meta (Facebook, Instagram, WhatsApp). |
| sg, us, hk, jp | Blok IP publik berdasarkan negara (Singapura, AS, Hong Kong, Jepang, dll). |

---

## Contoh Penggunaan di OpenClash (config.yaml)

```yaml
rules:
  # Aturan IP LAN / Jaringan Lokal
  - GEOIP,private,DIRECT,no-resolve

  # Aturan Geosite Buatan
  - GEOSITE,rule-ads,REJECT
  - GEOSITE,bank-id,DIRECT
  - GEOSITE,rule-eco,DIRECT
  - GEOSITE,sosmed,PROXIES

  # Aturan GeoIP Negara / Layanan
  - GEOIP,id,DIRECT
  - GEOIP,telegram,PROXIES

  # Final Fallback
  - MATCH,PROXIES
