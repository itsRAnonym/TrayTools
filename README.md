# TrayTools

Tiga aplikasi kecil buat system tray Windows 11: **BatteryTray**, **NetSpeedTray**, sama **LockKeysTray**. Awalnya gw bikin buat kebutuhan sendiri, terus kepikiran dibagi aja ke yang butuh. Free, gak ada iklan, gak ada telemetry.

## Soal repo ini

Repo ini cuma buat distribusi. Isinya README ini, tab **Releases** (tempat file download-nya), **Issues** buat lapor bug atau request fitur, sama LICENSE. Source code-nya gak gw publish (closed source), jadi jangan heran kalau gak ada folder kode di sini. Kalau lu cuma mau pake aplikasinya, langsung aja ke [Releases](../../releases/latest).

## Update terbaru (v2.2.5)

<!-- Ganti bagian ini tiap rilis baru. Detail lengkapnya tetep ada di halaman Releases. -->

- BatteryTray punya tab **Kontrol** baru: battery saver, mode daya, power plan, sama kecerahan layar yang diinget terpisah buat pas dicolok dan pas pake baterai.
- Estimasi waktu habis buat device Bluetooth dihitung ulang biar lebih akurat, plus ada toggle buat nyembunyiin.
- NetSpeedTray: tampilan ikon bisa diatur penuh (satuan, desimal, segitiga arah, label satuan, ketebalan font, warna), plus riwayat pemakaian data (harian, bulanan, total) yang direset tiap jam 12 malam.
- Semua app sekarang punya menu **Tentang dan update...**: versi, author, link GitHub, link donasi, sama tombol cek update.
- **LockKeysTray** app baru: nampilin overlay sebentar tiap lu pencet Caps Lock atau Num Lock.

Catatan lengkap per versi ada di Releases.

<!-- Taruh screenshot di folder docs/ terus aktifin baris ini:
![BatteryTray](docs/batterytray.png) ![NetSpeedTray](docs/netspeedtray.png)
-->

## BatteryTray

Ikon tray-nya nampilin persen baterai laptop. Klik kiri buat buka panel, isinya dua tab.

**Tab Baterai**

- Persen, status (lagi dipake / ngecas / tercolok), plus estimasi sisa waktu. Estimasinya dihitung dari daya yang lagi kepake (watt), bukan nebak dari persen doang.
- Kapasitas baterai (Wh), battery health, sama tren health-nya dari catatan harian. Trennya baru muncul setelah ada data kurang lebih seminggu.
- List device yang konek (Bluetooth sama gamepad Xbox) beserta level baterainya. List-nya auto refresh pas device konek atau putus. Ada toggle **Estimasi** buat nampilin atau ngumpetin perkiraan waktu habis tiap device.
- Pengingat cabut charger. Ada notif pas baterai nyampe 100%, terus diingetin lagi kalau masih nancep setelah waktu yang lu atur (default 30 menit).
- Notif kalau baterai device mau abis.

**Tab Kontrol**

- Battery saver on/off, mode daya (Hemat daya / Seimbang / Performa), sama ganti power plan.
- Kecerahan layar laptop: tombol 25/50/75/100% plus slider. Kecerahannya diinget terpisah buat pas dicolok dan pas pake baterai, jadi otomatis ganti sendiri waktu charger dicolok atau dicabut.

Popup-nya nutup sendiri (waktunya bisa diatur) dan selalu balik ke tab Baterai tiap dibuka lagi. Buat baterai laptop gak ada polling, jadi ringan.

## NetSpeedTray

Dua ikon tray yang nampilin kecepatan download sama upload secara realtime. Hover buat liat kecepatan lengkap plus pemakaian hari ini.

Klik kanan, **Tampilan ikon**, semuanya bisa lu atur dan bisa dimatiin:

- **Satuan**: KB/s, MB/s, GB/s, Kbps, Mbps, Gbps, atau otomatis (byte atau bit, satuannya ganti sendiri sesuai kecepatan).
- **Desimal**: 0, 0.0, 0.00, atau 0.000. Kalau angkanya udah gede, desimalnya dipangkas sendiri biar tetep muat di ikon.
- **Segitiga arah**: turun buat download, naik buat upload.
- **Label satuan kecil** di bawah angka (MB, Mbps, dan seterusnya).
- **Ketebalan font**: tipis, sedang, tebal.
- **Warna ikon**: teks tetap dan cuma segitiganya yang menyala pas ada trafik (bawaan), berwarna biru dan oranye, atau ikut tema.

Klik kiri ikon buat buka riwayat pemakaian data: hari ini, kemarin, bulan ini, total, 7 hari terakhir, sama 3 bulan terakhir. Hitungan hariannya direset tiap jam 12 malam, dan semua riwayat bisa diexport ke CSV. Klik kanan juga buat pilih adapter, interval update, sama nampilin atau ngumpetin ikon upload.

Catatan: ikon tray itu kecil banget (16 piksel di taskbar kecil atau layar 100%). Kalau susah kebaca, matiin label satuan dan kurangi desimal.

## LockKeysTray

Tiap lu pencet **Caps Lock** atau **Num Lock**, muncul overlay kecil sebentar di layar yang nunjukin tombolnya lagi ON atau OFF, terus ilang sendiri pelan-pelan. Overlay-nya gak ngambil fokus dan tembus klik, jadi gak ganggu yang lagi lu ketik.

- Ikon tray nunjukin status sekarang: huruf **A** (Caps) sama **1** (Num), hijau kalau nyala.
- Bisa pilih tombol yang dipantau (Caps, Num, dan opsional Scroll Lock), mau nampilin overlay pas OFF juga atau cuma pas ON, durasi tampil, posisi (bawah tengah, atas tengah, tengah layar, pojok), sama ukuran.
- Ada menu **Tes overlay** buat ngecek tampilannya. Klik kiri ikon tray juga sama.
- Gak ada polling, jadi cuma kerja pas lu beneran pencet tombolnya.

## Windows yang didukung

- **Windows 11**: target utama, semua fitur jalan.
- **Windows 10 (1607 ke atas)**: harusnya jalan, tapi fokus gw tetep Windows 11 jadi belum semua fitur gw tes di sana. Bedanya: popup gak punya sudut membulat (itu fitur Windows 11), tema terang atau gelap taskbar baru kebaca di versi 1903 ke atas, dan hasil mode daya sama level baterai Bluetooth bisa beda. Catatan: Windows 10 udah end of support sejak 14 Oktober 2025.
- **Windows 7, 8, 8.1**: gak didukung. App-nya pake .NET 8, dan .NET 8 emang gak jalan di sana.
- **Windows on ARM**: build-nya x64, harusnya jalan lewat emulasi di Windows 11 ARM. Versi 32-bit (x86) belum ada.

## Download

Ambil dari halaman [Releases](../../releases/latest). Tiap aplikasi ada dua varian:

| File | Keterangan |
|---|---|
| `NamaApp-x.y.z-win-x64.zip` | Versi ringan. Butuh **.NET 8 Desktop Runtime** ([download dari Microsoft](https://dotnet.microsoft.com/download/dotnet/8.0)). |
| `NamaApp-x.y.z-win-x64-standalone.zip` | Standalone, .NET udah di dalem. Ukurannya lebih gede, tapi tinggal jalanin. |

Ada juga `SHA256SUMS.txt` buat ngecek file yang lu download gak berubah.

## Cara pakai

1. Extract zip-nya ke folder yang tetap (misal `C:\Tools\BatteryTray`), terus jalanin `.exe`-nya.
2. Windows 11 suka nyembunyiin icon baru di area panah **^**. Drag icon-nya ke taskbar biar kelihatan terus.
3. Klik kanan icon buat setting, termasuk **Mulai bersama Windows**. Menu **Tentang dan update...** nampilin versi, author, link GitHub, link donasi, sama tombol cek update.

## Kalau muncul peringatan SmartScreen atau antivirus

App ini belum di-sign (code signing itu mahal), jadi Windows bisa munculin "Windows protected your PC". Klik **More info**, terus **Run anyway** kalau lu percaya. Mau mastiin file-nya asli? Bandingin SHA-256-nya sama `SHA256SUMS.txt`:

```powershell
Get-FileHash .\NamaApp-x.y.z-win-x64.zip -Algorithm SHA256
```

Antivirus juga kadang salah deteksi app single-file yang belum di-sign. Kalau kejadian, kabarin lewat Issues.

## Privasi

- Gak ada telemetry dan gak ada akun. Koneksi internet cuma kepake buat satu hal, yaitu cek update (penjelasan di bawah). Selain itu semuanya jalan offline.
- Semua data disimpen lokal:
  - BatteryTray: registry `HKCU\Software\BatteryTray` sama folder `%LocalAppData%\BatteryTray` (riwayat baterai device dan battery health).
  - NetSpeedTray: registry `HKCU\Software\NetSpeedTray` sama folder `%LocalAppData%\NetSpeedTray` (riwayat pemakaian data harian).
  - LockKeysTray: registry `HKCU\Software\LockKeysTray` (setting overlay).
  - Opsi **Mulai bersama Windows** nambah satu entri di `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`.

Soal cek update: itu cuma jalan kalau lu klik **Cek update** di menu Tentang, atau lu sendiri nyalain opsi cek update otomatis (default-nya mati). Yang dilakuin cuma nanya ke api.github.com versi rilis terbaru, gak ada data lu yang dikirim. Ya, GitHub tetep bisa lihat IP lu kayak website lain. App gak install update sendiri, cuma ngasih tau dan buka halaman download.

LockKeysTray ngebaca event keyboard (lewat Raw Input) cuma buat tau kapan Caps, Num, atau Scroll Lock ditekan. Tombol lain langsung dibuang, gak disimpen, gak dicatat, gak dikirim ke mana-mana. Tapi karena sifatnya mantau keyboard, antivirus tertentu bisa curiga, dan karena ini closed source, gw cuma bisa jelasin, bukan ngebuktiin. Kalau lu gak nyaman, skip aja app yang satu ini.

## Hapus aplikasi

Matiin **Mulai bersama Windows** dari menu klik kanan, pilih **Keluar**, terus hapus folder app-nya. Mau bersih total? Hapus juga key registry sama folder `%LocalAppData%` yang disebut di atas.

## Keterbatasan

- Baterai device cuma muncul kalau device-nya **ngelapor baterai ke Windows**. Yang gak ngelapor ya gak bisa ditampilin.
- Estimasi waktu habis buat device Bluetooth sifatnya **perkiraan kasar**. Windows cuma ngasih persen, dan banyak device ngelapornya per 10%. Estimasinya baru muncul setelah level turun dua kali, jadi butuh pemakaian sejam dua jam dulu.
- Estimasi sisa waktu laptop ngikutin daya yang kepake saat ini, jadi bakal berubah kalau bebannya berubah.
- Kontrol kecerahan cuma buat layar internal laptop, monitor eksternal belum didukung. Mode daya pake API Windows yang gak terdokumentasi resmi. Battery saver diatur lewat ambang nyala otomatis, soalnya Windows gak punya API resmi buat nyalain langsung. Hasilnya bisa beda antar laptop, jadi kalau ada yang gak jalan, kabarin aja.
- Semua app versinya ngikutin tag rilis yang sama. Jadi kalau satu rilis cuma ngubah satu app, app yang lain tetep bakal nunjukin "ada versi baru" (isinya sama aja, tinggal download kalau mau).
- Overlay LockKeysTray gak bakal muncul di atas game yang jalan fullscreen eksklusif (borderless windowed aman). Kalau window yang lagi fokus jalan sebagai admin, bisa jadi event tombolnya gak kebaca, itu batasan Windows.
- Riwayat pemakaian data cuma ngitung selama NetSpeedTray jalan (nyalain **Mulai bersama Windows** biar gak ada yang kelewat). Angkanya dari counter adapter jaringan, jadi bisa sedikit beda sama kuota yang ditagih operator.

## Lapor bug atau request fitur

Buka tab **Issues**. Tulis versi Windows, versi app, sama cara munculin masalahnya. Kalau soal Bluetooth di BatteryTray, klik kanan icon, pilih **Simpan log perangkat (debug)**, terus attach file lognya. Kalau soal LockKeysTray (misalnya overlay gak muncul), klik kanan icon, pilih **Simpan log debug**, terus attach file lognya. Log itu cuma nyatet kejadian sistem dan tombol Lock, tombol lain gak pernah dicatat.

## Lisensi

Closed source. Bebas dipake (pribadi maupun kerja), tapi gak boleh dimodif atau disebar ulang. Detailnya ada di [LICENSE.txt](LICENSE.txt). Komponen pihak ketiga ada di [THIRD-PARTY-NOTICES.txt](THIRD-PARTY-NOTICES.txt).
