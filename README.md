# GKI 2.0 Custom Kernel for Nothing A001 (CMF Phone 2 Pro)

Prebuilt **GKI 2.0** kernel packaged as an **AnyKernel3** ZIP, based on [Wild Kernels](https://github.com/WildKernels/GKI_KernelSU_SUSFS) and shipping **BakaSU** root with **SUSFS** and **NoMount** support. Flash it directly on the phone with Kernel Flasher, no PC required.

| | |
|---|---|
| **Device** | CMF Phone 2 Pro (`Nothing A001`) |
| **Kernel** | `6.1.162-android14` (GKI 2.0, KMI `android14-6.1`, SPL `2026-03`) |
| **Root** | BakaSU v4.2.0-rc3 |
| **Format** | AnyKernel3 ZIP (replaces `Image` inside your stock `boot`) |

---

## Features

- **BakaSU** (KernelSU fork, formerly ReSukiSU) with built-in kernel root
- **SUSFS** — kernel-level path/mount/uname hiding
- **NoMount** — mount-less module overlay (NoMount metamodule)
- Everything else from Wild Kernels builds: Baseband Guard, DroidSpaces-OSS, extended networking (BBR, WireGuard, CAKE and more), NTSync, BTF / eBPF / FUSE-BPF, ptrace and unicode fixes

> [!NOTE]
> Edit this list to match exactly what is enabled in your build. See `BuildInfo` in each release for the full config.

---

## Disclaimer

> [!WARNING]
> Flashing a custom kernel can cause boot loops, data loss or a temporarily unusable device. Everything here is provided **as is, for testing and educational purposes**. The author is not responsible for any damage, data loss, hardware issues or failed boots. Always keep a backup and flash at your own risk.

---

## Requirements

**On the phone**
- Unlocked bootloader
- Existing root via **KernelSU** or a fork (KernelSU-Next, BakaSU, ReSukiSU, ...)
- [Kernel Flasher](https://github.com/fatalcoder524/KernelFlasher) with root access
- Stock firmware whose kernel version and security patch level match the release (see below)

**On a PC (optional, but strongly recommended as a safety net)**
- [Android Platform-Tools](https://developer.android.com/tools/releases/platform-tools) (`adb`, `fastboot`)
- Google USB drivers (Windows) and a good USB cable
- A copy of your stock `boot.img` for recovery

---

## Installation

> [!IMPORTANT]
> The kernel version and KMI in the release notes (for example `6.1.162-android14`) **must match your current firmware**. A mismatched build will not boot.

1. **Back up your current `boot`.** In Kernel Flasher, open the *Backup* tab and save `boot` to storage. Copy it off the phone as well.
2. **Download** the AnyKernel3 ZIP from [Releases](../../releases). If the downloaded archive contains another ZIP inside, extract it and use the inner one.
3. **Open Kernel Flasher**, grant root, and go to the *Flash* tab.
4. **Select the AnyKernel3 ZIP** and flash it to the **active slot**. The installer unpacks your boot image, replaces the kernel `Image` and repacks it.
5. **Reboot** when it reports success.

---

## After flashing

1. Open **BakaSU**. The home screen should show `Working` and your new kernel version.
2. Install the manager from the same release, so manager and kernel driver versions match.
3. Install the **NoMount Metamodule** (Modules → Install), then reboot.
4. Install a **SUSFS module** (e.g. [susfs4ksu-module](https://github.com/sidex15/susfs4ksu-module)) if you want SUSFS configuration.

---

## Recovery

If the device does not boot:

1. Reboot into the bootloader (power off, then hold **Power + Volume Down**).
2. Flash your stock boot back from a PC:
```bash
   fastboot flash boot boot.img
   fastboot reboot
```
   For an A/B device, flash the slot you installed to (`boot_a` or `boot_b`).

---

## Updating

Back up first, then flash the newer AnyKernel3 ZIP the same way. You do not need to restore stock `boot` between updates, but update the manager and metamodule so versions stay in sync.

---

## Credits

- [Wild Kernels](https://github.com/WildKernels/GKI_KernelSU_SUSFS)
- [BakaSU](https://github.com/Baka-SU/BakaSU)
- [SUSFS](https://gitlab.com/simonpunk/susfs4ksu)
- [NoMount](https://github.com/maxsteeel/nomount)
- [AnyKernel3](https://github.com/osm0sis/AnyKernel3)
- [Kernel Flasher](https://github.com/fatalcoder524/KernelFlasher)

## Support

Found a bug or have feedback? Open an [issue](../../issues) and include your firmware version, kernel version from the BakaSU home screen, and logs.
