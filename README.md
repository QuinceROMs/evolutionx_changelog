Evolution X - device tree changelog
===================================

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
