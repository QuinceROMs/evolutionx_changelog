Evolution X - device tree changelog
===================================

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
