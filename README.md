Evolution X - device tree changelog
===================================

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
