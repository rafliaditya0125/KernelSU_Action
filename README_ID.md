# KernelSU Action khusus Beryllium (Android 13)

Action ini telah dikonfigurasi secara spesifik untuk **Poco F1 (Beryllium) yang menggunakan Android 13**.

## Disclaimer
> [!WARNING]
> Karena branch ini dikhususkan untuk Android 13, **action ini hanya work dan tested di Beryllium Android 13**. Jika Anda menggunakan perangkat yang berbeda atau versi Android yang berbeda, silakan coba branch lain atau buat konfigurasi Anda sendiri di branch `main`.

## Perangkat yang Didukung (Supported Device)
- **Device:** Poco F1 (Beryllium)
- **Android Version:** 13
- **Kernel Source:** [android_kernel_xiaomi_sdm845](https://github.com/PainKiller3/android_kernel_xiaomi_sdm845.git) (Branch: `thirteen`)
- **Kernel Config:** `stock-beryllium_defconfig`
- **Compiler:** proton-clang

## Cara Penggunaan (Usage)
Melakukan build dengan action ini sangat simpel, cukup fork lalu build:

1. **Fork** repositori ini.
   - **Penting:** Saat melakukan fork, **jangan centang** opsi "Copy the main branch only" (hanya salin branch main) agar Anda mendapatkan branch ini juga dan bisa langsung build.
2. Buka tab **Actions** di repositori hasil fork Anda.
3. Pilih **Build Kernel** di menu sebelah kiri.
4. Klik drop-down **Run workflow**.
   - **Penting:** Di bagian pemilihan branch, pastikan untuk memilih branch yang sesuai dengan konfigurasi (Android 13) sebelum menjalankan.
5. Tunggu proses kompilasi selesai. Jika berhasil, file zip `AnyKernel3` akan otomatis diunggah di bagian artifacts dalam run tersebut.
6. Unduh file zip tersebut dan pasang (flash) melalui TWRP atau custom recovery lainnya.

## Ucapan Terima Kasih (Thanks)
- [AnyKernel3](https://github.com/osm0sis/AnyKernel3)
- [AOSP](https://android.googlesource.com)
- [KernelSU](https://github.com/tiann/KernelSU)
- [xiaoleGun](https://github.com/xiaoleGun)
- [proton-clang](https://github.com/kdrag0n/proton-clang) (untuk custom compiler Clang)
- [LineageOS](https://github.com/LineageOS) (untuk GCC prebuilts)
- [PainKiller3](https://github.com/PainKiller3/android_kernel_xiaomi_sdm845) (untuk kernel source Beryllium)
