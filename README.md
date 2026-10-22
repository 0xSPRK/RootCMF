# GKI 2.0 Custom Kernel Infrastructure

This repository provides customized GKI (Generic Kernel Image) 2.0 kernel builds for Android devices, integrating advanced kernel-level security control and stealth mechanisms.

---

## Technical Stack

*   **BakaSU (ReSukiSU)** — Next-generation kernel-space root solution implementation. Operating entirely within kernel-space to enforce strict isolation from userspace detection APIs. Features advanced runtime redundancy fallbacks to eliminate initialization failures.
*   **SUSFS (Suspended File System)** — High-efficiency subsystem designed to isolate and virtualize paths, node structures, and execution points, removing traces of modification from telemetry trackers.
*   **NoMount (ZeroMount)** — Modern architectural model enabling containerless system modifications. Avoids generic overlayfs dependencies to improve detection resistance.
*   **Extended Attributes** — Native `TMPFS XATTR` and `POSIX ACLs` support enabled to host complex system metamodules without breaking file system integrity.

---

## Supported Devices

*   **CMF Phone 2 Pro** (Codename: `Nothing A001`) — Target platform tracking the latest Vendor Boot / Image configurations.

---

## Disclaimer

```text
Modifying core system partitions and compiling custom kernels carries inherent risks of data corruption or temporary bricking. The developer accepts no responsibility for device instability, failure to boot, hardware issues, or lost alarms. Proceed exclusively under your own technical verification.
```

---

## Installation Guide

Follow these guidelines precisely to ensure a proper patch cycle. Modern targets feature complex slot and boot structures (e.g., `init_boot` layouts) that require runtime-driven injection via localized ramdisk patchers.

### Prerequisites

#### Host Machine (PC/Laptop)
*   Configured **Android Platform-Tools** environment variables.
*   Latest **Google USB Drivers** installed for stable interface bridging.
*   High-quality **USB-A to Type-C** cable connection.

#### Target Hardware (Phone)
*   The device must already operate under an established root environment via baseline **KernelSU** or its variants (e.g., *KernelSU-Next*).

### Deployment Procedure

1. **Verify Compilation Target:** Download the latest deployment archive from the repository Releases section. **CRITICAL WARNING:** Ensure that the architecture string and patch-level version specified in the release field (e.g., `Kernel Version: 6.1.162-android14`) match your current stock system configuration exactly. Cross-matching misaligned versions will result in boot failure. Production trees track the newest production-tier firmware updates.
2. **Launch Flashing Environment:** Open the **Kernel Flasher** interface on your phone.
3. **Load AnyKernel3 Payload:** Navigate to the local storage path, locate the matching downloaded AnyKernel3 ZIP package, and select it.
4. **Execute Script:** Trigger the flashing sequence. The engine will unpack the localized boot structure, perform live kernel image replacement, and re-pack the boot sequence safely.
5. **System Initialisation:** Once the prompt displays execution success, select **Reboot** or power-cycle the smartphone manually.

If the structural version checking was successful and the payload has been applied cleanly, the deployment is complete.

---

## Project Context

*   **Developer Space:** [@0xSPRK](https://github.com)
*   **Target Core Repository:** [GKI_KernelSU_SUSFS](https://github.com/GKI_KernelSU_SUSFS)

For architectural feedback or error reporting, initialize a formal tracking ticket under the Issues workspace.
