# TrayTools

Dua aplikasi kecil buat system tray Windows 11: **BatteryTray** sama **NetSpeedTray**. Awalnya gw bikin buat kebutuhan sendiri, terus kepikiran dibagi aja ke yang butuh. Free, gak ada iklan, gak ada telemetry.

## Soal repo ini

Repo ini cuma buat distribusi. Isinya README ini, tab **Releases** (tempat file download-nya), **Issues** buat lapor bug atau request fitur, sama LICENSE. Source code-nya gak gw publish (closed source), jadi jangan heran kalau gak ada folder kode di sini. Kalau lu cuma mau pake aplikasinya, langsung aja ke [Releases](../../releases/latest).

## TrayTools v2.1.0

Update lumayan gede kali ini, plus ada satu app baru. Banyak fitur baru, dan estimasi waktu habis buat device Bluetooth gw hitung ulang biar lebih akurat.

### BatteryTray

- Tab **Kontrol** baru di popup: battery saver, mode daya (Hemat daya / Seimbang / Performa), ganti power plan, sama kecerahan layar (25/50/75/100% plus slider). Kecerahannya diinget terpisah buat pas dicolok dan pas pake baterai, terus otomatis dipake waktu charger dicolok atau dicabut.
- Estimasi waktu habis buat device Bluetooth dihitung ulang. Sekarang pake momen level turun yang beneran kejadian, bukan tebakan. Tetep kasar buat device yang ngelapor per 10%, dan baru muncul setelah level turun dua kali.
- Toggle **Estimasi** di list device, kalau lu gak mau liat perkiraannya.
- List device auto refresh pas ada yang konek atau putus.
- Pengingat cabut charger: notif pas 100%, terus diingetin lagi kalau masih nancep setelah waktu yang lu atur.
- Notif kalau baterai device mau abis.
- Riwayat battery health plus trennya.
- Popup nutup sendiri (waktunya bisa diatur), selalu balik ke tab Baterai tiap dibuka, dan udah gak kedip pas refresh.

### NetSpeedTray

- Ikon sekarang angka doang (MB/s), biar kebaca di ukuran tray yang kecil. Biru download, oranye upload.
- Riwayat pemakaian data: hari ini, kemarin, bulan ini, total, 7 hari terakhir, sama 3 bulan terakhir. Klik kiri ikon buat buka.
- Hitungan harian direset tiap jam 12 malam.
- Riwayat bisa diexport ke CSV atau dihapus dari menu klik kanan.

### LockKeysTray (app baru)

- Overlay sebentar tiap pencet Caps Lock atau Num Lock (opsional Scroll Lock), nunjukin ON atau OFF. Gak ngambil fokus, tembus klik.
- Ikon tray nunjukin status sekarang (A buat Caps, 1 buat Num).
- Bisa diatur: tombol yang dipantau, tampil pas OFF atau enggak, durasi, posisi, ukuran.
- Gak ada polling, jadi ringan.

### Semua app

- Menu baru **Tentang dan update...** di klik kanan: versi, author, link GitHub, link donasi, sama tombol **Cek update**.
- Cek update ngecek rilis terbaru di GitHub dan buka halaman download. Ada opsi cek otomatis (maksimal sekali sehari), default-nya mati.

### Catatan

- Windows 11 itu target utama. Windows 10 (1607+) harusnya jalan, tapi belum semua fitur dites di sana. Windows 7/8/8.1 gak didukung karena .NET 8.

- Kontrol daya dan kecerahan pake API Windows yang sebagian gak resmi, jadi hasilnya bisa beda antar laptop. Kalau ada yang gak jalan, kabarin lewat Issues, sebut laptop lu apa.
- App belum di-sign, jadi SmartScreen mungkin muncul. Cek SHA-256 pake `SHA256SUMS.txt` kalau mau mastiin.

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
3. Klik kanan icon buat setting, termasuk **Mulai bersama Windows**.

## Kalau muncul peringatan SmartScreen atau antivirus

App ini belum di-sign (code signing itu mahal), jadi Windows bisa munculin "Windows protected your PC". Klik **More info**, terus **Run anyway** kalau lu percaya. Mau mastiin file-nya asli? Bandingin SHA-256-nya sama `SHA256SUMS.txt`:

```powershell
Get-FileHash .\NamaApp-x.y.z-win-x64.zip -Algorithm SHA256
```

Antivirus juga kadang salah deteksi app single-file yang belum di-sign. Kalau kejadian, kabarin lewat Issues.

## Privasi

- Gak ada koneksi internet, gak ada telemetry, gak ada akun.
- Semua data disimpen lokal:
  - BatteryTray: registry `HKCU\Software\BatteryTray` sama folder `%LocalAppData%\BatteryTray` (riwayat baterai device dan battery health).
  - NetSpeedTray: registry `HKCU\Software\NetSpeedTray` sama folder `%LocalAppData%\NetSpeedTray` (riwayat pemakaian data harian).
  - Opsi **Mulai bersama Windows** nambah satu entri di `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`.

## Hapus aplikasi

Matiin **Mulai bersama Windows** dari menu klik kanan, pilih **Keluar**, terus hapus folder app-nya. Mau bersih total? Hapus juga key registry sama folder `%LocalAppData%` yang disebut di atas.

## Keterbatasan

- Baterai device cuma muncul kalau device-nya **ngelapor baterai ke Windows**. Yang gak ngelapor ya gak bisa ditampilin.
- Estimasi waktu habis buat device Bluetooth sifatnya **perkiraan kasar**. Windows cuma ngasih persen, dan banyak device ngelapornya per 10%. Estimasinya baru muncul setelah level turun dua kali, jadi butuh pemakaian sejam dua jam dulu.
- Estimasi sisa waktu laptop ngikutin daya yang kepake saat ini, jadi bakal berubah kalau bebannya berubah.
- Kontrol kecerahan cuma buat layar internal laptop, monitor eksternal belum didukung. Mode daya pake API Windows yang gak terdokumentasi resmi. Battery saver diatur lewat ambang nyala otomatis, soalnya Windows gak punya API resmi buat nyalain langsung. Hasilnya bisa beda antar laptop, jadi kalau ada yang gak jalan, kabarin aja.
- Riwayat pemakaian data cuma ngitung selama NetSpeedTray jalan (nyalain **Mulai bersama Windows** biar gak ada yang kelewat). Angkanya dari counter adapter jaringan, jadi bisa sedikit beda sama kuota yang ditagih operator.

## Lapor bug atau request fitur

Buka tab **Issues**. Tulis versi Windows, versi app, sama cara munculin masalahnya. Kalau soal Bluetooth di BatteryTray, klik kanan icon, pilih **Simpan log perangkat (debug)**, terus attach file lognya.

## Lisensi

Closed source. Bebas dipake (pribadi maupun kerja), tapi gak boleh dimodif atau disebar ulang. Detailnya ada di [LICENSE.txt](LICENSE.txt). Komponen pihak ketiga ada di [THIRD-PARTY-NOTICES.txt](THIRD-PARTY-NOTICES.txt).
