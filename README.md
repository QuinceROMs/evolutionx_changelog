Evolution X - device tree changelog
===================================

2026.04.22
----------
- KeyHandler: AlertSliderPlugin: Observe layout changes
- synced with crDroid kernel and KSU Next 3.2.0
- backported Linux Kernel 7.0 USB and FFS fixes.


2026.04.09
----------
- disabled FaceDownDetector by default to reduce battery consumption in idle
- fixed several sepolicy rules.


2026.04.04
----------
- reworked battery SOC smoothing again to follow stock OOS behavior more closely,
  eliminating visible catch-up jumps and keeping the status bar drop in cleaner 1% steps
- enabled BBRv2 with fq as the default TCP stack on SM8150
- backported the vmscan critical-process throttle bypass so direct reclaim
  no longer stalls system-critical tasks, including binder-spawned workers that inherit
  a critical `oom_score_adj`
- brought up the NXP eSE / NFC off-host stack, shipped the matching OOS eSE config
  and added the required HAL cross-lookup SELinux rules
- audio/Dolby: restored offload policy profiles, fixed profile-specific GEQ preset storage
  and restored session-scoped playback effects
- bumped vendor.oplus.hardware.subsys_interface.subsys_radio to V9
- enabled Quick Share / Mosey.


2026.03.17
----------
- synced the kernel with current crDroid changes and updated SusFS to v2.0.0
  with the latest upstream follow-up fixes
- fixed battery SOC jumps so the status bar drops smoothly in visible 1% steps
  instead of occasional 4% jumps
- overclocked the GPU to 757 MHz across SM8150 v2 DTS variants after stability testing
- backported the Qualcomm qseecom listener/app ioctl race fix
- restored reserve partition ueventd rules for current OOS blobs
- aligned OOSCam package lists with OOS 12.1 H.41, including the Telegram camera whitelist
- refreshed `camera_helper` with expressive styling, smaller resources and updated translations
- vendor: allowed `gettid` in `wfdhdcphalservice` seccomp policy to avoid Android 16
  seccomp filter failures
- hardware/oplus: refreshed translations, updated alert slider visuals, and added
  sepolicy fixes for fingerprint vendor data creation/ioctl access plus
  `ro.oplusupgrade.alpha.version` labeling.


2026.03.14
----------
- comprehensive display driver fix addressing complete system freezes
  (black screen, no touch response, only force reboot helped): hardened
  PHY resume error handling, fixed multiple deadlock paths in CMD mode
  (ppdone timeout, HBM with clocks off, VBIF halt stall), and enabled
  suspend-ULPS to avoid risky full PHY power-down on every suspend cycle
- added CVP and OmxVpp camera blobs (device and vendor, 32+64 bit).


2026.03.10
----------
- reverted unstable memory management optimizations (vmscan tuning, page_cluster)
- reverted Google Pixel 4 CPU frequency profile (capacity-dmips-mhz)
- fixed double-tap-to-wake by enabling IRQ wake support for Synaptics S3706 touch controller
- backported MADV_COLD and MADV_PAGEOUT reclaim logic for LMKD to actively reclaim
  memory from cold/idle processes (completes the process_madvise syscall backport)
- backported schedutil slower frequency ramp-down for improved battery efficiency
- added new sensor mappings for Thermal HAL and disabled excessive thermal logging
- sepolicy: silenced NNAPI HAL default_prop denial on user builds
- sepolicy: fixed sensor HAL and binder denials on user builds.


2026.03.08
----------
- reverted kgsl rw_semaphore conversion (caused priority inversion under GPU load)
- reverted zram writeback and idle page tracking (caused memory pressure spikes)
- reverted UFS BUG_ON to WARN_ON conversion (masked real hardware errors)
- capped schedutil iowait boost to thermal limit to prevent frequency overshoot
- reduced page_cluster from 3 to 0 for faster single-page swap-in
- tuned vmscan swappiness, watermark scale and dirty ratios for lower kswapd overhead
- backported NL80211_ATTR_MAX_NUM_AKM_SUITES for WPA3/SAE compatibility
- disabled carrier state during WLAN suspend to prevent phantom disconnect events
- cancelled pending WCD SPI clock work before suspend to avoid use-after-free
- sepolicy: allowed vendor_init to set exported_bluetooth_prop and vendor_system_prop
- sepolicy: allowed vendor_init to read proc_meminfo and proc_vmstat
- sepolicy: allowed hal_wifi_default diag_device and wlan firmware access
- sepolicy: added dontaudit for IMS and iorapd noise
- sepolicy: allowed system_server access to battery sysfs, CachedAppOptimizer
  cgroup, motor and ultrasound devices
- added Thermal HAL v3 (android.hardware.thermal-service.pixel) with progressive
  skin-therm throttling hints in powerhint.json
- fixed lockscreen charging info display units.


2026.03.06
----------
- backported binder oneway spamming detection with logging and backtrace dump
- backported BINDER_FREEZE and BINDER_GET_FROZEN_INFO ioctls with freeze race fix
- backported process_madvise() and process_mrelease() syscalls for improved memory
  reclaim by LMKD
- added MADV_COLD and MADV_PAGEOUT memory advice definitions
- renamed ION system heap to "system-uncached" for Android 16 libdmabufheap compatibility
- optimized CPU scheduler capacity values (261/871/1024) based on Google Pixel 4 DTS
  for accurate LITTLE/BIG/PRIME IPC ratios (multi-core performance improved by ~5%)
- fixed IOMMU device leak on DT parsing and context bank stale fault carryover
  from bootloader
- converted KGSL GPU memory lock from spinlock to rw_semaphore for better read
  concurrency under heavy GPU load
- fixed TSENS thermal sensor TOCTOU race condition during reinit
- capped schedutil iowait frequency boost to thermal limit to prevent thermal overshoot
- added named symlinks for thermal zones for reliable thermal-engine zone lookup
  (required by OnePlus Camera for skin temperature readings)
- added ro.opcamera.support and persist.sys.oem.region props to enable full OxygenOS
  camera functionality
- fixed OnePlusCameraHelper: added missing android:exported to BootCompletedReceiver
  so CameraMotorService and FallSensorService actually start (pop-up camera motor fix).


2026.03.04
----------
- added the latest backported kernel security patches from Qualcomm
- added ZRAM and UFS optimizations
- fixed strict length check for WMI_GTK_OFFLOAD_STATUS_EVENT to accept both legacy
  (106-byte, no BIGTK fields) and modern (146-byte, WPA3/802.11w) formats, preventing
  extraction failures on older SM8150 firmware after suspend/resume
- tuned VM and LMKD for improved memory management
- granted OnePlus Camera access to flashlight parameters
- another attempt to fix the battery readings skipping bug.


2026.03.03
----------
- fixed NCM tethering (FINALLY!)
- critical kernel and vendor security fixes, including several anti-exploit fixes
  (their list is on Google Drive in the ROM directory)
- fixed battery skipping bug in kernel (more testing needed)
- configured SQLite to operate in MEMORY mode
- BT.601 170M is now treated as sRGB in SurfaceFlinger (better colors in old apps)
- added stubs and used correct SM8150 OPFeatures values and flags to reduce Gallery logspam
- added two minor fixes related to SuSFS.


2026.02.26
----------
- shipped OnePlus Gallery
- patched Camera to fix slow-motion init error (SM8150 does not support 120Hz)
- reduced Camera thumbnail size to prevent Gallery crash
- fixed watermark
- fixed OnePlus Camera and Gallery logspam (both are quiet now)
- enabled Qualcomm's Assertive Display (AD4) (imported from OOS 11.0.9.1)
- redesigned auto-brightness curve
- added statsd daemon on zygote-start to prevent massive logspam.


2026.02.20
----------
- fixed 48MP mode
- reverted ultrasound and vi-feedback backend names.


2026.02.13
----------
- a fully functional 📷 OnePlus Camera 📷 has been added, along with, among other things:
  - stub classes for OnePlus framework dependencies
  - SELinux rules for OP Camera and VPP
  - Camera JNI and native libraries (product/lib64)
  - HIDL interface libraries for cameraMDM, engcamera, slogan,
    cammidasservice (system/lib, system/lib64, system_ext/lib64)
  - VPP and bokeh vendor blobs
  - default permissions and feature XMLs
- imported 32-bit QCom audio effects from OnePlus 9R
- added vi-feedback backend mapping for speaker protection.


2025.02.09
----------
- fixed Google Hotword a.k.a OK Google 🔥
- added missing 32-bit QCcom audio effect blobs
- patched volume_listener to use odm/lib/hw/audio.primary.msmnile.so path instead vendor/lib/hw/audio.primary.msmnile.so
- added missing audio backend names
- routed listen/preproc to LSM1 and isolate ultrasound
- added missing echo-reference speaker path.


2025.01.31
----------
- completed Dolby Atmos implementation. It is now FULLY OPERATIONAL.😊🥳🥰


2025.01.30
----------
- added missing TinyALSA library
- patched audio libs to load libaudioroute-v34.so
- set executable permissions and linked Dolby service against V33 libstagefright_foundation
- updated Bluetooth blobs from LA.UM.9.1.r1-13700-SMxxx0.QSSI13.0
- switched Bluetooth Audio HIDL revision to 2.1
- created standalone RRO for OplusDoze
- bumped vendor.oplus.hardware.charger to V10
- KeyHandler: Fixed alert slider scaling upon resolution changes
- many sepolicy fixes.


2025.01.22
----------
- updated kernel
- updated clang to r563880c
- added performance entries for low-latency H.264 decoder
- increased the Video Quality bpp tuning parameter value for H.264 decoder
- patched libdpps.so to load Qualcomm's libtinyxml2_1.so to prevent runtime crashes.


2025.01.19
----------
- first QPR2 build :)
- added missing audio configs from OxygenOS 12.1 H.41
- updated carrier list to LA.QSSI.16.0.r1-06700-qssi.0
- enabled smooth fade effect on edges of scrolling text
- match both UI and KeyHandler default values for alert slider
- misc vintf and sepolicy fixes.


2025.12.30
----------
- added misc vintf and sepolicy updates
- kernel compiled with Clang 21
- removed Dialer overlay (call recording is now enabled by default).


2025.12.19
----------
- overlay: fixed charging infos on keyguard
- CarrierConfigOverlay: enabled editable_enhanced_4g_lte_bool globally
- disabled AOD wallpaper.


2025.12.15
----------
- first QPR1 build :)
- KeyHandler and doze: applied Expressive theme and converted for M3E support
- fstab: enabled FBE2 and fixed up for EROFS
- updated CarrierConfig
- take a snapshot in 16-bit pixel format to save memory
- fixed screen recording lag
- disabled EGL image tracking to reduce overhead.


2025.11.17
----------
- fixed file transfer issue
- many VINTF and sepolicy updates.


2025.11.10
----------
- livedisplay: Use PWM pulse for IAntiFlicker if available
- sepolicy: Removed commonized ST NFC labels
- interfaces: Added AIDL and HIDL IDisplayPanelFeature
- many minor fixes.


2025.10.30
----------
- init: restored I/O performance by setting both the group_idle and slice_idle parameters to 0
- enabled Qualcomm TrueWireless Stereo.


2025.10.25
----------
- disabled frame pacing (due to frame drops)
- enabled ScrollOptimizer
- enabled ART speed-profile during build
- fixed more NFC denials
- minor sepolicy fixes.


2025.10.19
----------
- fixed USB tethering
- reverted several commits that caused frame drops during normal use and gameplay
- a few minor fixes.


2025.10.12
----------
- fixed crashing of android.hardware.nfc-service.nxp service
- maximum AOD refresh rate set to 60Hz
- bumped kernel BPF version override to 5.4.299
- enabled comprehensive ART optimizations including VDEX and ODEX generation for all system components to improve first-boot performance and reduce application startup latency.


2025.10.10
----------
- defined pickup sensor type
- enabled support for kernel idle timer
- tuned SurfaceFlinger timers for better power efficiency
- init: remove package cache on early boot
- compiled HWUI for performance
- enabled QTI vendor adaptations for AOSP compatibility
- improved real-time management of process priorities in the system
- disabled Qualcomm aggressive memory optimization (MemPlus)
- increased limit on the number of apps and services running in the background
- disabled the IOrapd service to free up memory and perform less intensive background I/O operations
- imported QCOM audio effects (bassboost, reverb, virt) from OnePlus 9R.
