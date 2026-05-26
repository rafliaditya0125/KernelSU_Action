# KernelSU Action

[English](README.md) | [Indonesia](README_ID.md)

Action ini ditujukan untuk Kernel non-GKI, cukup universal, dan membutuhkan pengetahuan dasar tentang kernel dan Android.

## Peringatan :warning::warning::warning:

Jika Anda bukan pembuat Kernel ini dan menggunakan tenaga/hasil karya orang lain untuk mem-build KernelSU, harap gunakan untuk keperluan pribadi saja dan jangan bagikan ke orang lain. Hal ini bertujuan untuk menghargai kerja keras pembuat aslinya.

## Perangkat & Branch yang Didukung

Anda dapat dengan mudah berpindah branch tergantung pada target device dan versi Android Anda. Berikut adalah daftar branch yang tersedia:

| Device | Android Version | Branch |
| --- | --- | --- |
| Secara Umum (Default) | - | `main` |
| Beryllium (Poco F1) | 13 | `Beryllium/A13` |

## Versi Kernel yang Didukung

- `5.4`
- `4.19`
- `4.14`
- `4.9`

## Penggunaan

> Semua variabel dalam file `config.env` hanya memeriksa nilai `true`.

> Setelah kompilasi berhasil, AnyKernel3 akan diunggah pada tab `Action` dan device check pada AnyKernel tersebut telah dinonaktifkan. Silakan flash melalui TWRP/OrangeFox.

Fork repositori ini ke akun Anda dan edit file `config.env` sesuai kebutuhan. Setelah itu, masuk ke tab `Action`. Pada menu di sebelah kiri, pilih opsi `Build Kernel`. Kemudian klik tombol `Run workflows` yang muncul di bagian atas untuk memulai proses build.

### Kernel Source

Ubah dengan link repository Kernel Anda.

Contoh: https://github.com/Diva-Room/Miku_kernel_xiaomi_wayne

### Kernel Source Branch

Ubah dengan branch dari repository Kernel Anda.

Contoh: TDA

### Kernel Config

Ubah dengan nama file konfigurasi (defconfig) kernel Anda.

Contoh: `vendor/wayne_defconfig`

### Arch

Mendefinisikan arsitektur (architecture).
Contoh: arm64

### Kernel Image Name

Ubah menjadi nama file kernel yang akan di-flash, biasanya selaras dengan `BOARD_KERNEL_IMAGE_NAME` di device tree AOSP Anda.

Contoh: `Image.gz-dtb`

Nama yang umum digunakan biasanya mencakup `Image` atau `Image.gz`.

### Clang

#### Use custom clang

Anda dapat menggunakan toolchain clang unofficial seperti [proton-clang](https://github.com/kdrag0n/proton-clang).

#### Custom Clang Source

> Pastikan link berakhiran `.git` jika Anda menggunakan link dari repository Git.

Mendukung alamat repository Git atau direct link ke file zip.

#### Custom cmds

Jika Anda menggunakan custom clang, Anda seharusnya sudah paham cara memodifikasi parameter ini secara manual. :)

#### Clang Branch

Merujuk pada issue [#23](https://github.com/xiaoleGun/KernelSU_Action/issues/23), kami menyediakan opsi untuk memakai kustomisasi branch ke repositori utama Google. Opsi utamanya meliputi:

| Clang Branch |
| ------------ |
| master |
| master-kernel-build-2021 |
| master-kernel-build-2022 |

Untuk menggunakan branch lain, silakan cari sesuai kebutuhan Anda di https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86.

#### Clang Version

Masukkan versi Clang yang ingin digunakan.

| Clang Version | Corresponding Android Version | AOSP-Clang Version |
| ------------- | ----------------------------- | ------------------ |
| 12.0.5        | Android S                     | r416183b           |
| 14.0.6        | Android T                     | r450784d           |
| 14.0.7        |                               | r450784e           |
| 15.0.1        |                               | r458507            |
| 17.0.1        |                               | r487747b           |
| 17.0.2        | Android U                     | r487747c           |

Clang 12 umumnya sudah bisa dipakai mengkompilasi kernel 4.14 ke atas. Contohnya pada MI 6X dengan kernel 4.19 menggunakan r450784d.

### GCC

#### Enable GCC 64

Mengaktifkan cross-compiler GCC 64C.

#### Enable GCC 32

Mengaktifkan cross-compiler GCC 32C.

### Extra cmds

Beberapa kernel memerlukan command tambahan sebelum memulai compile. Umumnya Anda tidak perlu mengisi apapun di sini, silakan cari tahu sendiri referensi yang cocok dengan kernel Anda. Pisahkan multipel command dengan spasi.

Contoh: `LLVM=1 LLVM_IAS=1`

### Disable LTO

LTO digunakan untuk optimasi kernel namun tak jarang memicu error. Aktifkan opsi ini untuk mematikan instruksi LTO.

### Enable KernelSU

Diaktifkan jika Anda ingin melakukan build image kernel murni tanpa integrasi KernelSU untuk troubleshooting kesalahan kompilasi.

#### Branch atau Tag KernelSU

[KernelSU 1.0 tidak lagi mendukung kernel non-GKI](https://github.com/tiann/KernelSU/issues/1705). Versi stabil terakhir yang mendukung metode (non-GKI) adalah [v0.9.5](https://github.com/tiann/KernelSU/tree/v0.9.5). Pastikan Anda menggunakan branch yang tepat.

Tentukan branch atau tag KernelSU:

- ~~Branch utama (development): `KERNELSU_TAG=main`~~
- Versi stabil terbaru: `KERNELSU_TAG=v0.9.5`
- Tag spesifik (misal `v0.5.2`): `KERNELSU_TAG=v0.5.2`

#### Signature size & hash KernelSU Manager

Atur nilai size dan hash jika Anda me-repack Manager (APK). Jika Anda menggunakan versi manager resminya, **Biarkan Kosong**! Atau isi dengan nilai bawaan dari versi official-nya:

`KSU_EXPECTED_SIZE=0x033b`

`KSU_EXPECTED_HASH=c371061b19d8c7d7d6133c6a9bafe198fa944e50c1b31c9d8daa8d7f1fc2d2d6`

Gunakan perintah `ksud debug get-sign <apk_path>` di shell Anda untuk mendapatkan nilai size dan hash yang valid.

### Add Kprobes Config

Otomatis melakukan inject (autoinject) parameter dukungan Kprobes langsung ke file defconfig milik Anda.

### Add overlayfs Config

Otomatis melakukan inject parameter overlayfs ke defconfig untuk mendukung sistem operasi partisi (read & write) pada modul-modul (modules) KernelSU.

### Apply KernelSU Patch

Opsi ini sangat berguna jika fungsi kprobe di kernel Anda tidak bisa dieksekusi dengan normal (biasanya bug pada upstream kernel versi lawas di bawah 4.8).

Sistem akan otomatis memodifikasi (apply patch) source code kernel target ke tahap fungsional dasar agar selaras memuat dukungan instalasi KernelSU.  
Referensi: [Integrate for non-GKI devices](https://kernelsu.org/guide/how-to-integrate-for-non-gki.html#manually-modify-the-kernel-source)

### Remove unused packages

Membersihkan paket-paket dan dependensi utilitas Linux runner yang tidak terpakai saat mengeksekusi build untuk melonggarkan ruang (free disk space).

### AnyKernel3

#### Use custom AnyKernel3

Gunakan custom repository instalasi (packaging tool) milik kustomisasi AnyKernel3 Anda.

#### Custom AnyKernel3 Source

> Jika berbentuk base repository Git, silakan masukkan URL yang memuat akhiran ekstensi `.git`

Selain git repository, juga valid mendukung alamat direct link untuk file package installer ekstensi *.zip*.

#### AnyKernel3 Branch

Tentukan branch repositori tersebut, misal: `master` atau `main`

### Enable ccache

Mengaktifkan fitur modul memory cache (`ccache`) sehingga secara signifikan mempercepat proses iterasi kompilasi build kernelnya di lain waktu (menghemat jeda hingga ke angka rasio kecepatan 2/5).

### Need DTBO

Sistem akan otomatis mengekspor (mengunggah) file `DTBO` untuk instalasi ZIP final AnyKernel3. Beberapa versi perangkat mewajibkan adanya hal ini.

### Build Boot IMG

> Ekstensi workflow (Action).

Membangun (build) file format keluaran `boot.img` akhir, namun Anda wajib mengatur parameter `Source boot image`.

### Source Boot Image

Opsi ini membutuhkan source link (bersifat direct link) dari file `boot.img` original Anda yang telah ditest bisa booting dengan normal/work 100%. File boot image yang dipakai harus senada disesuaikan base source-nya dari *AOSP device tree* yang selaras dengan ROM perangkat yang Anda gunakan. Di mana file tersebut terkandung (Ramdisk) krusial berupa handler (init) perutean dasar dan daftar format partisi penting. Build tanpa adanya komponen tersebut hanya akan berakhir ke arah masalah bootloop system.

Contoh Format: https://raw.githubusercontent.com/xiaoleGun/KernelSU_action/main/boot/boot-wayne-from-Miku-UI-latest.img

## Terima Kasih

- [AnyKernel3](https://github.com/osm0sis/AnyKernel3)
- [AOSP](https://android.googlesource.com)
- [KernelSU](https://github.com/tiann/KernelSU)
- [xiaoxindada](https://github.com/xiaoxindada)
- [xiaoleGun](https://github.com/xiaoleGun)