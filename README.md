# TrayTools

Dua aplikasi kecil buat system tray **Windows 11**: **BatteryTray** dan **NetSpeedTray**.
Gratis, tanpa iklan, tanpa telemetri. Kode sumbernya tertutup (*closed source*), tapi aplikasinya bebas dipakai.

<!-- Taruh screenshot di folder docs/ lalu aktifkan baris ini:
![BatteryTray](docs/batterytray.png) ![NetSpeedTray](docs/netspeedtray.png)
-->

## BatteryTray

Ikon tray menampilkan **persen baterai laptop**. Klik kiri untuk membuka panel detail:

- Persen, status (memakai baterai / mengisi / tercolok), dan **estimasi sisa waktu** yang dihitung dari daya yang sedang terpakai (W), bukan sekadar tebakan persen.
- Kapasitas baterai (Wh) dan **kesehatan baterai**, plus **tren kesehatan** dari catatan harian.
- **Daftar perangkat terhubung** (Bluetooth dan gamepad Xbox) beserta level baterainya dan estimasi waktu habis. List perangkat akan memuat ulang saat perangkat tersambung atau terputus.
- **Pengingat cabut charger**: notifikasi saat baterai 100%, lalu diingatkan lagi kalau masih tercolok setelah waktu yang kamu atur.
- Notifikasi saat baterai perangkat rendah.
- Panel menutup otomatis (waktunya bisa diatur) dan tidak memakai polling untuk baterai laptop, jadi ringan.

## NetSpeedTray

Dua ikon tray yang menampilkan **kecepatan download dan upload secara langsung** dalam MB/s. Hover untuk melihat total data sesi, klik kanan untuk memilih adapter jaringan, interval pembaruan, dan menampilkan atau menyembunyikan ikon upload.

## Unduh

Ambil dari halaman **[Releases](../../releases/latest)**. Ada dua varian per aplikasi:

| File | Keterangan |
|---|---|
| `NamaApp-x.y.z-win-x64.zip` | Ringan. Butuh **.NET 8 Desktop Runtime** terinstall ([unduh dari Microsoft](https://dotnet.microsoft.com/download/dotnet/8.0)). |
| `NamaApp-x.y.z-win-x64-standalone.zip` | Mandiri, .NET sudah di dalamnya. Ukuran lebih besar, tidak perlu pasang apa-apa. |

`SHA256SUMS.txt` berisi checksum untuk memastikan file yang kamu unduh tidak berubah.

## Cara pakai

1. Ekstrak zip ke folder tetap (misalnya `C:\Tools\BatteryTray`), lalu jalankan `.exe`-nya.
2. Windows 11 menaruh ikon baru di area tersembunyi (panah **^**). Seret ikonnya ke taskbar supaya selalu terlihat.
3. Klik kanan ikon untuk pengaturan, termasuk **Mulai bersama Windows**.

## Peringatan Windows SmartScreen atau antivirus

Aplikasi ini belum ditandatangani (*code signing*), jadi Windows bisa menampilkan "Windows protected your PC". Klik **More info → Run anyway** jika kamu percaya. Bandingkan juga SHA-256 file dengan `SHA256SUMS.txt`:

```powershell
Get-FileHash .\NamaApp-x.y.z-win-x64.zip -Algorithm SHA256
```

Aplikasi single-file yang belum bertanda tangan kadang salah ditandai antivirus. Kalau itu terjadi, kabari lewat Issues.

## Privasi

- Tidak ada koneksi internet, tidak ada telemetri, tidak ada akun.
- Semua data disimpan lokal:
  - BatteryTray: registry `HKCU\Software\BatteryTray`, folder `%LocalAppData%\BatteryTray` (riwayat baterai perangkat dan kesehatan baterai).
  - NetSpeedTray: registry `HKCU\Software\NetSpeedTray`.
  - Opsi **Mulai bersama Windows** menambah satu entri di `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`.

## Hapus aplikasi

Matikan **Mulai bersama Windows** dari menu klik kanan, pilih **Keluar**, lalu hapus folder aplikasinya. Untuk membersihkan sisa data, hapus kunci registry dan folder `%LocalAppData%\BatteryTray` di atas.

## Keterbatasan

- Baterai perangkat hanya muncul kalau perangkatnya **melaporkan baterai ke Windows**. Yang tidak melapor tidak bisa ditampilkan.
- Estimasi waktu habis untuk perangkat Bluetooth bersifat **perkiraan kasar**: Windows hanya memberi persen, dan banyak perangkat melapor dalam kelipatan 10%. Estimasi baru muncul setelah ada data pemakaian beberapa menit sampai beberapa jam.
- Estimasi sisa waktu laptop mengikuti daya yang terpakai saat ini, jadi berubah kalau beban berubah.

## Lapor bug atau minta fitur

Buka tab **Issues**. Sertakan versi Windows, versi aplikasi, dan langkah untuk mengulang masalahnya. Untuk masalah perangkat Bluetooth di BatteryTray, klik kanan ikon → **Simpan log perangkat (debug)** lalu lampirkan file log-nya.

## Lisensi

Hak cipta dilindungi. Aplikasi bebas dipakai, tetapi tidak boleh dimodifikasi atau disebarkan ulang. Detail di [LICENSE.txt](LICENSE.txt). Komponen pihak ketiga ada di [THIRD-PARTY-NOTICES.txt](THIRD-PARTY-NOTICES.txt).
