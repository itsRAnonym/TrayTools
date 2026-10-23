# TrayTools

Dua aplikasi kecil buat system tray Windows 11: **BatteryTray** sama **NetSpeedTray**. Awalnya gw bikin buat kebutuhan sendiri, terus kepikiran dibagi aja ke yang butuh. Free, gak ada iklan, gak ada telemetry.

## Soal repo ini

Repo ini cuma buat distribusi. Isinya README ini, tab **Releases** (tempat file download-nya), **Issues** buat lapor bug atau request fitur, sama LICENSE. Source code-nya gak gw publish (closed source), jadi jangan heran kalau gak ada folder kode di sini. Kalau lu cuma mau pake aplikasinya, langsung aja ke [Releases](../../releases/latest).

## Update terbaru (v0.4.0)

<!-- Ganti bagian ini tiap rilis baru. Detail lengkapnya tetep ada di halaman Releases. -->

- BatteryTray punya tab **Kontrol** baru: battery saver, mode daya, power plan, sama kecerahan layar yang diinget terpisah buat pas dicolok dan pas pake baterai.
- Estimasi waktu habis buat device Bluetooth dihitung ulang biar lebih akurat, plus ada toggle buat nyembunyiin.
- NetSpeedTray sekarang ikonnya angka doang, dan ada riwayat pemakaian data (harian, bulanan, total) yang direset tiap jam 12 malam.

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

Dua ikon tray yang nampilin kecepatan download sama upload secara realtime. Isinya angka doang dalam MB/s, biru buat download, oranye buat upload. Hover buat liat kecepatan lengkap plus pemakaian hari ini.

Klik kiri buat buka riwayat pemakaian data: hari ini, kemarin, bulan ini, total, 7 hari terakhir, sama 3 bulan terakhir. Hitungan hariannya direset tiap jam 12 malam, dan semua riwayat bisa diexport ke CSV. Klik kanan buat pilih adapter, interval update, sama nampilin atau ngumpetin ikon upload.

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
