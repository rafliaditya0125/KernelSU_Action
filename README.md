# KernelSU Action for Beryllium (Android 13)

This action is customized and pre-configured specifically for **Poco F1 (Beryllium) running Android 13**. 

## Disclaimer
> [!WARNING]
> Because this branch is specifically configured for Android 13, **this only works and has been tested on Beryllium Android 13**. If you use a different device or Android version, please use another branch or create your own configuration in the `main` branch.

## Supported Device
- **Device:** Poco F1 (Beryllium)
- **Android Version:** 13
- **Kernel Source:** [android_kernel_xiaomi_sdm845](https://github.com/PainKiller3/android_kernel_xiaomi_sdm845.git) (Branch: `thirteen`)
- **Kernel Config:** `stock-beryllium_defconfig`
- **Compiler:** proton-clang

## Usage
Building your own KernelSU with this action is extremely simple:

1. **Fork** this repository. 
   - **Important:** When forking, do **NOT** check "Copy the main branch only", to ensure you get all the pre-configured branches.
2. Go to the **Actions** tab in your forked repository.
3. Select **Build Kernel** on the left side menu.
4. Click **Run workflow** on the right side.
   - **Important:** Make sure to select the appropriate branch for this configuration before clicking Run.
5. Wait for the compilation to finish. Once successful, the `AnyKernel3` flashable zip will be uploaded in the Action artifacts.
6. Download the zip and flash it via TWRP or your preferred custom recovery.

## Thanks
- [AnyKernel3](https://github.com/osm0sis/AnyKernel3)
- [AOSP](https://android.googlesource.com)
- [KernelSU](https://github.com/tiann/KernelSU)
- [xiaoleGun](https://github.com/xiaoleGun)
- [proton-clang](https://github.com/kdrag0n/proton-clang) (for the custom Clang compiler)
- [LineageOS](https://github.com/LineageOS) (for the GCC prebuilts)
- [PainKiller3](https://github.com/PainKiller3/android_kernel_xiaomi_sdm845) (for the Beryllium kernel source)
