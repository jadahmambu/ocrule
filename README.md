@'
===================================================================
 V2Ray Rules Dat (Custom Geosite & GeoIP Build)
===================================================================

Repositori ini secara otomatis mengompilasi dan memperbarui berkas 
geosite.dat dan geoip.dat secara harian menggunakan GitHub Actions. 

Dioptimalkan khusus untuk OpenWrt / OpenClash / Mihomo Core, dengan 
fokus pada kecepatan kompilasi native (AWK/SED), pembersihan syntax 
invalid (wildcards, trailing dots, double hyphens), serta efisiensi RAM.

-------------------------------------------------------------------
1. FITUR UTAMA
-------------------------------------------------------------------
- Super Fast Build Engine: Pemrosesan domain menggunakan AWK & SED native.
- Rigorously Sanitized: Otomatis membersihkan wildcard (*), trailing dots (.), 
  format non-RFC, dan duplikat domain.
- All-in-One Ads & Security (ads-extra): Menggabungkan OISD Full, 
  AdGuard DNS Filter, dan Malikshi Antiscam ke dalam 1 tag tunggal.
- Clean Banking Routing (bank-id): Pembersihan circular include agar 
  transaksi bank/e-wallet Indonesia tidak terdeteksi proxy.
- Automated Daily Release: Diperbarui otomatis setiap hari pukul 00:30 WIB.

-------------------------------------------------------------------
2. ISI & RINGKASAN TAG GEOSITE.DAT
-------------------------------------------------------------------
- rule-ads        : Iklan Utama (Malikshi + Jadahmambu) -> REJECT
- ads-extra       : Super-Blocklist (OISD Full + AdGuard + Antiscam) -> REJECT
- bank-id         : Perbankan ID & E-Wallet (BCA, Mandiri, DANA, dll) -> DIRECT
- sosmed          : Media Sosial (Jadahmambu) -> HK-VPN
- streaming       : Platform Streaming (Jadahmambu) -> HK-VPN
- vidconference   : Zoom, Teams, Meet (Jadahmambu) -> HK-VPN
- rule-microsoft  : Layanan Microsoft & Windows Update -> DIRECT
- rule-eco        : Bypass Ekonomi / Saklar khusus -> DIRECT / Eco Mode
- netflix         : Bawaan V2Fly DLC (Sangat presisi) -> HK-VPN

-------------------------------------------------------------------
3. TAUTAN UNDUHAN LANGSUNG (DIRECT URL)
-------------------------------------------------------------------
Gunakan tautan berikut untuk dimasukkan ke dalam rule-providers OpenClash:

* Geosite:
  https://github.com/USERNAME/REPO_ANDA/releases/latest/download/geosite.dat

* GeoIP:
  https://github.com/USERNAME/REPO_ANDA/releases/latest/download/geoip.dat

(Ganti USERNAME/REPO_ANDA sesuai nama akun dan repositori GitHub Anda)

-------------------------------------------------------------------
4. LISENSI & KREDIT
-------------------------------------------------------------------
Di-build menggunakan pustaka v2fly/domain-list-community.
Penyedia sumber data domain:
- Malikshi (https://github.com/malikshi)
- Jadahmambu (https://github.com/jadahmambu)
- OISD Blocklist (https://oisd.nl)
- AdGuard Team (https://github.com/AdguardTeam)
'@ | Out-File -Encoding utf8 README.txtv
