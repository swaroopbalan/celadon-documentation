.. _release-notes:

Release Notes
#############

.. note::

    Refer to :ref:`release-naming-convention` to decode the release tags of
    the following |C| releases.

.. contents::
   :local:
   :depth: 1


Base Releases
*************

.. contents::
   :local:
   :depth: 1


CIV_00.22.02.21_A12
===================
* This is a Pre Production Binary Release for evaluation and development
  purposes . This release enables support for 12th GEN Core and it has
  been tested on Alder Lake RVP [Celadon in VM].

Intended audience
-----------------

* Open Source Community who has subscribed to celadon@lists.linuxfoundation.org

Customer support
----------------

* subscribe/unsubscribe celadon mailing list using : https://lists.linuxfoundation.org/mailman/listinfo/celadon

Introduction
------------

New in this release
-------------------

 * New features
    * Android 12 with latest AOSP release tag (android-12.0.0_r28)
    * Enabled Virgl
    * Enabled SRIOV (Single Root I/O Virtualization)
    * Switch between h/w accelerated graphics and s/w graphics
    * Enabled Virtio-gpu
    * Tearing prevention
    * Virtualized Display – KMSRO/ Zero copy
    * Switch displays between guests
    * 8k resolution support
    * HDMI Audio
    * SoF HDA mediation solution
    * Virtual TPM2.0
    * Trusty KeyMint support
    * File based Encryption
    * VP9 h/w accelerated
    * Prime buffer sharing
    * Media Codec 2.0 h/w path
    * Super image > 4G
    * bootconfig support
    * WPA3 support
    * WiFi 802.11.ax Support
    * Bluetooth Control from Android in Virtual Machine
    * ISH Enabled
    * Support Control Plant – VM Manager
    * Switch USB touch screen between guest OSes
    * Incremental FS, F2FS support

 * Includes Android 12 main features:
    * Integrated VM Manager to configure CIV replacing start_civ.sh
        * This changes launch steps for CIV - please refer to
          https://docs.01.org/celadon/getting-started/on-vm.html#use-vm-manager
    * Celadon supports Android 12 with API level 31 and FCM target level 6
    * Boot control HAL upgraded to V1.2
    * Audio HAL upgraded to V7.0
    * Browse Internet (IPv6)
    * WiFi Direct
    * WiFi Control from Android in Virtual Machine
    * Basic sanity test passed for all components *
    * Bug fixes, customizations and optimizations for x86
    * SE Policy updated for API level 31
    * AIDL libs updated
    * Health HAL is optimized to adapt the new changes for S Dessert
    * Graphics introduced scheduling plans,
    * Graphics: Surface flinger caching, GPU memory accounting, profiling and
      GPU scheduling
    * Accessibility, System UI and backup & restore features updated with minor
      modifications
    * FUSE passthrough introduced to improve IO performance
    * IncFS updated with Better Monitoring Support, virtio-9p support, fs-verity
      support
    * Enabled NNAPI updatability in Machine Learning
    * New platform features for Mainline Module
    * Incremental: new Android 12+ feature that could reduce initial downloads
      of app
    * Approximate location access and privacy related updates
    * New Storage Features like Storage management API changes, New directory
      for voice recordings, Media management access, App storage access and
      Extended file access support.
    * Memory accounting updates
    * Framework introduced changes in foreground service, Gamepad – Input device
      features, Haptic related vibrator changes
    * Media side, Audio supports BLE audio, Haptics generator, Multi-channel audio
      along with audio HAL v7.0
    * Media transcoding, media extractor related changes and improved quality in
      encoded video
    * AVIF image support, Easier blurs, color filters, and other effects
    * CameraX vendor extension support
    * Enabled NNAPI updatability in Machine Learning
    * New platform features for Mainline Module
    * Improvements to bandwidth estimation APIs in connectivity and introduced principle of 5G slicing
    * Wi-Fi privacy improvements with - Non-Persistent MAC Address Randomization
    * Bluetooth side, BT classic and BLE introduced
    * Activity Detection, CHRE, Bluesky, FLP & RTT related changes
    * Major changes in window management and introduced Display grouping and emphasis for multi-display context
    * pKVM (Protected KVM) code compatibility available, Celadon won’t support it.
    * Rich Haptic experience – Actuator effects, audio-coupled haptic, Enriched image supported notifications, rounded corner APIs etc.
    * Picture in Picture (PiP) improvements, Immersive mode improvements for gesture navigation, Rich content insertion and Recents URL sharing
    * Provide apps direct access to tombstone traces
    * Android 12 release from Google shall be referred from the below links
         * Release Notes: https://source.android.com/setup/start/android-12-release
         * Blog : https://android-developers.googleblog.com/2021/10/android-12-is-live-in-aosp.html


Known issues
------------
* Unable to set and change the lock screen sometimes after couple of minutes
  of usage
* Volume control doesn't work with 3.5mm Headset button
* Unable to seek properly on recorded video
* HDMI audio is lost after adb reboot
* Limitation on Alderlake RVP--> Suspend-resume functionality is not applicable
  on ADL RVP

Where to find the release
-------------------------

* Manifest Link : https://github.com/projectceladon/manifest/blob/master/stable-build/CIV_00.22.02.21_A12.xml
* Binary Link : https://github.com/projectceladon/celadon-binary/tree/master/CIV_00.22.02.21_A12


How to install this release
---------------------------

* Steps to sync to this release

   * repo init -u https://github.com/projectceladon/manifest -b master -m stable-build/CIV_XX.XX.XX.XX_AXX.xml
   * NOTE : Manifest tag will change according to the latest release
   * repo sync -c -q -j${nproc}

* Android build commands

   * For Compilation please use Ubuntu 18.04
   * source build/envsetup.sh
   * lunch caas-userdebug
   * make flashfiles -jN

* Steps To build the host kernel for this manifest

    * Download  caas-releasefiles-userdebug.tar.gz and put it under ~/civ
    * cd ~/civ && tar zxvf caas-releasefiles-userdebug.tar.gz
    * cd patches/kernel/lts2020-chromium
    * ./build_weekly.sh
    * Deb files will be generated in
      patches/kernel/lts2019-chromium/host_kernel
    * sudo dpkg -i \*.deb
    * Update grub to wait indefinitely for kernel selection on boot

        * sudo vim /etc/default/grub
        * Comment out GRUB_TIMEOUT_STYLE=hidden
          #GRUB_TIMEOUT_STYLE=hidden
        * Uncomment the following line and modify grub timeout to -1 for
          indefinite wait or 5 for 5secs wait
          #GRUB_TIMEOUT=-1
        * Save the file
        * sudo update-grub

    * sudo reboot
    * Select compiled kernel from "Advanced options for Ubuntu"

* Flash and run steps
     * https://docs.01.org/celadon/getting-started/on-vm.html#use-vm-manager

Validation results
------------------

This build has been validated on Alder Lake RVP in the following function domains:

=============================  =======  ========
Component                      Results  Comments
=============================  =======  ========
Wi-Fi                          OK        Host wifi is switched to Android UI in QEMU using usb pass through
BT                             OK        Bluetooth is working
Audio Playback                 OK        MP3, AAC-LC, AAC-ELD, HEAAC, HEAAC-V2, VORBIS, OPUS, FLAC, PCM/WAV formats supported
Adb connect over WIFI          OK
Adb connect over Ethernet      OK
Security                       OK
Boot                           OK       Boots on QEMU 6.0.0
Ethernet                       OK
Image Flash                    OK
Web browsing                   OK
Video playback                 OK       H264/H265/MPEG2/VP8/VP9 Video Playback
USB                            OK       Keyboard , Mouse , Pen drive
Display                        OK
Touch and Gesture              OK
=============================  =======  ========


Reference configuration
-----------------------

 * Supported hardware

     * Product -  Alder Lake RVP

 * Supported software

     * AOSP Version - android-12.0.0_r28
     * NUC11PAQI7 Host Kernel - -5.10.110-cvhb
     * NUC11PAQI7 Guest kernel - -5.10.110-cvhb


Acronyms and terms
------------------

* CIV - Celadon in Virtual Machine


Helpful hints / related documents
---------------------------------

* If you plan to use Celadon in product, please replace all the test keys
  under device/intel/build/testkeys/ with your product key.  
* The release of this project will be signed by test keys, it's only a
  reference for our customer and we are not responsible for this. Customers
  should use their own keys to sign their release images
* Build Celadon in VM  https://01.org/projectceladon/documentation/getting-started/build-source#build-os-image
* Flash Steps : https://docs.01.org/celadon/getting-started/on-vm.html#use-vm-manager

CIV_00.22.01.04_A12
===================
* This is a Pre Production Binary Release for evaluation and development
  purposes . This release is
  supported on |NUC| Kit `NUC11PAQI7  <https://www.intel.in/content/www/in/en/products/boards-kits/nuc/kits/nuc11paqi7.html>`_ Celadon in VM.

Intended audience
-----------------

* Open Source Community who has subscribed to celadon@lists.linuxfoundation.org

Customer support
----------------

* subscribe/unsubscribe celadon mailing list using : https://lists.linuxfoundation.org/mailman/listinfo/celadon

Introduction
------------

New in this release
-------------------

 * New features
    * Android 12 with latest AOSP release tag (android-12.0.0_r26)
    * Integrated VM Manager to configure CIV replacing start_civ.sh
        * This changes launch steps for CIV - please refer https://docs.01.org/celadon/getting-started/on-vm.html#use-vm-manager

 * Includes Android 12 main features:
    * Celadon supports Android 12 with API level 31 and FCM target level 6
    * Boot control HAL upgraded to V1.2
    * Audio HAL upgraded to V7.0
    * Basic sanity test passed for all components *
    * Bug fixes, customizations and optimizations for x86
    * SE Policy updated for API level 31
    * AIDL libs updated
    * Health HAL is optimized to adapt the new changes for S Dessert
    * Graphics introduced scheduling plans,
    * Graphics: Surface flinger caching, GPU memory accounting, profiling and GPU scheduling
    * Accessibility, System UI and backup & restore features updated with minor modifications
    * FUSE passthrough introduced to improve IO performance
    * IncFS updated with Better Monitoring Support, virtio-9p support, fs-verity support
    * Enabled NNAPI updatability in Machine Learning
    * New platform features for Mainline Module
    * Incremental: new Android 12+ feature that could reduce initial downloads of app
    * Approximate location access and privacy related updates
    * New Storage Features like Storage management API changes, New directory for voice recordings, Media management access, App storage access and Extended file access support.
    * Memory accounting updates
    * Framework introduced changes in foreground service, Gamepad – Input device features, Haptic related vibrator changes
    * Media side, Audio supports BLE audio, Haptics generator, Multi-channel audio along with audio HAL v7.0
    * Media transcoding, media extractor related changes and improved quality in encoded video
    * AVIF image support, Easier blurs, color filters, and other effects
    * CameraX vendor extension support
    * Enabled NNAPI updatability in Machine Learning
    * New platform features for Mainline Module
    * Improvements to bandwidth estimation APIs in connectivity and introduced principle of 5G slicing
    * Wi-Fi privacy improvements with - Non-Persistent MAC Address Randomization
    * Bluetooth side, BLE audio introduced, NFC API/UX improved for payment enhancement.
    * Activity Detection, CHRE, Bluesky, FLP & RTT related changes
    * Major changes in window management and introduced Display grouping and emphasis for multi-display context
    * pKVM (Protected KVM) code compatibility available, Celadon won’t support it.
    * Rich Haptic experience – Actuator effects, audio-coupled haptic, Enriched image supported notifications, rounded corner APIs etc.
    * Picture in Picture (PiP) improvements, Immersive mode improvements for gesture navigation, Rich content insertion and Recents URL sharing
    * Provide apps direct access to tombstone traces
    * Android 12 release from Google shall be referred from the below links
         * Release Notes: https://source.android.com/setup/start/android-12-release
         * Blog : https://android-developers.googleblog.com/2021/10/android-12-is-live-in-aosp.html


Known issues
------------
* There are WIP features in all components for full feature completions, This release tests only basic sanity of components.

Where to find the release
-------------------------

* Manifest Link : https://github.com/projectceladon/manifest/blob/master/stable-build/CIV_00.22.01.04_A12.xml
* Binary Link : https://github.com/projectceladon/celadon-binary/tree/master/CIV_00.22.01.04_A12


How to install this release
---------------------------

* Steps to sync to this release

   * repo init -u https://github.com/projectceladon/manifest -b master -m stable-build/CIV_XX.XX.XX.XX_AXX.xml
   * NOTE : Manifest tag will change according to the latest release
   * repo sync -c -q -j${nproc}

* Android build commands

   * For Compilation please use Ubuntu 18.04
   * source build/envsetup.sh
   * lunch caas-userdebug
   * make flashfiles -jN

* Steps To build the host kernel for this manifest

    * Download  caas-releasefiles-userdebug.tar.gz and put it under ~/civ
    * cd ~/civ && tar zxvf caas-releasefiles-userdebug.tar.gz
    * cd patches/kernel/lts2020-chromium
    * ./build_weekly.sh
    * Deb files will be generated in
      patches/kernel/lts2019-chromium/host_kernel
    * sudo dpkg -i \*.deb
    * Update grub to wait indefinitely for kernel selection on boot

        * sudo vim /etc/default/grub
        * Comment out GRUB_TIMEOUT_STYLE=hidden
          #GRUB_TIMEOUT_STYLE=hidden
        * Uncomment the following line and modify grub timeout to -1 for
          indefinite wait or 5 for 5secs wait
          #GRUB_TIMEOUT=-1
        * Save the file
        * sudo update-grub

    * sudo reboot
    * Select compiled kernel from "Advanced options for Ubuntu"

* Flash and run steps
     * https://docs.01.org/celadon/getting-started/on-vm.html#use-vm-manager

Validation results
------------------

This build has been validated on |NUC| Kit `NUC11PAQI7  <https://www.intel.in/content/www/in/en/products/boards-kits/nuc/kits/nuc11paqi7.html>`_  in the following function domains:

=============================  =======  ========
Component                      Results  Comments
=============================  =======  ========
Wi-Fi                          OK        Host wifi is switched to Android UI in QEMU using usb pass through
BT                             OK        Bluetooth is working
Audio Playback                 OK        MP3, AAC-LC, AAC-ELD, HEAAC, HEAAC-V2, VORBIS, OPUS, FLAC, PCM/WAV formats supported
Adb connect over WIFI          OK
Adb connect over Ethernet      OK
Display /Touch and Gesture     OK
Security                       OK
Boot                           OK       Boots on QEMU 4.2.0
Ethernet                       OK
Image Flash                    OK
Web browsing                   OK
Video playback                 OK       H264/H265/MPEG2/VP8/VP9 Video Playback
USB                            OK       Keyboard , Mouse , Pen drive

=============================  =======  ========


Reference configuration
-----------------------

 * Supported hardware

     * Product - NUC11PAQI7

 * Supported software

     * AOSP Version - android-12.0.0_r26
     * NUC11PAQI7 Host Kernel - -5.10.82-cvhb
     * NUC11PAQI7 Guest kernel - -5.10.91-cvhb


Acronyms and terms
------------------

* CIV - Celadon in Virtual Machine


Helpful hints / related documents
---------------------------------

* If you plan to use Celadon in product, please replace all the test keys
  under device/intel/build/testkeys/ with your product key.  
* The release of this project will be signed by test keys, it's only a
  reference for our customer and we are not responsible for this. Customers
  should use their own keys to sign their release images
* Build Celadon in VM  https://01.org/projectceladon/documentation/getting-started/build-source#build-os-image
* Flash Steps : https://docs.01.org/celadon/getting-started/on-vm.html#use-vm-manager


CIV_00.21.03.41_A12
===================

* We are glad to announce that the Celadon Project now supports Android 12 within 2 days of Google PV. We wish the Celadon community to start working with Android 12 and provide us feedback on what more you would like to see in the Celadon project.

* This is a Pre Production Manifest Release for evaluation and development
  purposes and it cannot be used for production purposes. This release is
  supported on |NUC| Kit `NUC11PAQI7  <https://www.intel.in/content/www/in/en/products/boards-kits/nuc/kits/nuc11paqi7.html>`_ Celadon in VM.

Intended audience
-----------------

* Open Source Community who has subscribed to celadon@lists.linuxfoundation.org

Customer support
----------------

* subscribe/unsubscribe celadon mailing list using : https://lists.linuxfoundation.org/mailman/listinfo/celadon

Introduction
------------

New in this release
-------------------

 * New features
    * Android 12 with latest AOSP manifest (android-12.0.0_r2)
    * Celadon supports Android 12 with API level 31 and FCM target level 6
    * Boot control HAL upgraded to V1.2
    * Audio HAL upgraded to V7.0
    * Basic sanity test passed for all components *
    * Bug fixes, customizations and optimizations for x86
    * SE Policy updated for API level 31
    * AIDL libs updated
    * Health HAL is optimized to adapt the new changes for S Dessert
 * Includes Android 12 main features:
    * Graphics introduced scheduling plans,
    * Graphics: Surface flinger caching, GPU memory accounting, profiling and GPU scheduling
    * Accessibility, System UI and backup & restore features updated with minor modifications
    * FUSE passthrough introduced to improve IO performance
    * IncFS updated with Better Monitoring Support, virtio-9p support, fs-verity support
    * Enabled NNAPI updatability in Machine Learning
    * New platform features for Mainline Module
    * Incremental: new Android 12+ feature that could reduce initial downloads of app
    * Approximate location access and privacy related updates
    * New Storage Features like Storage management API changes, New directory for voice recordings, Media management access, App storage access and Extended file access support.
    * Memory accounting updates
    * Framework introduced changes in foreground service, Gamepad – Input device features, Haptic related vibrator changes
    * Media side, Audio supports BLE audio, Haptics generator, Multi-channel audio along with audio HAL v7.0
    * Media transcoding, media extractor related changes and improved quality in encoded video
    * AVIF image support, Easier blurs, color filters, and other effects
    * CameraX vendor extension support
    * Enabled NNAPI updatability in Machine Learning
    * New platform features for Mainline Module
    * Improvements to bandwidth estimation APIs in connectivity and introduced principle of 5G slicing
    * Wi-Fi privacy improvements with - Non-Persistent MAC Address Randomization
    * Bluetooth side, BLE audio introduced, NFC API/UX improved for payment enhancement.
    * Activity Detection, CHRE, Bluesky, FLP & RTT related changes
    * Major changes in window management and introduced Display grouping and emphasis for multi-display context
    * pKVM (Protected KVM) code compatibility available, Celadon won’t support it.
    * Rich Haptic experience – Actuator effects, audio-coupled haptic, Enriched image supported notifications, rounded corner APIs etc.
    * Picture in Picture (PiP) improvements, Immersive mode improvements for gesture navigation, Rich content insertion and Recents URL sharing
    * Provide apps direct access to tombstone traces
    * Android 12 release from Google shall be referred from the below links
         * Release Notes: https://source.android.com/setup/start/android-12-release
         * Blog : https://android-developers.googleblog.com/2021/10/android-12-is-live-in-aosp.html


Known issues
------------
* There are WIP features in all components for full feature completions, This release tests only basic sanity of components.

Where to find the release
-------------------------

* Manifest Link : https://github.com/projectceladon/manifest/blob/master/stable-build/CIV_00.21.03.41_A12.xml

System Requirements
-------------------
* Recommended system requirements for Host:
    * CPU:  4 cores or more
    * RAM:  8 GB or more
    * Hard-Disk: 250 GB [Desired]


How to install this release
---------------------------

* Steps to sync to this release

   * repo init -u https://github.com/projectceladon/manifest -b master -m stable-build/CIV_XX.XX.XX.XX_AXX.xml
   * NOTE : Manifest tag will change according to the latest release
   * repo sync -c -q -j${nproc}

* Android build commands

   * For Compilation please use Ubuntu 18.04
   * source build/envsetup.sh
   * lunch caas-userdebug
   * make flashfiles -jN

* Steps To build the host kernel for this manifest

    * Download  caas-releasefiles-userdebug.tar.gz and put it under ~/civ
    * cd ~/civ && tar zxvf caas-releasefiles-userdebug.tar.gz
    * cd patches/kernel/lts2019-chromium
    * ./build_weekly.sh
    * Deb files will be generated in
      patches/kernel/lts2019-chromium/host_kernel
    * sudo dpkg -i \*.deb
    * Update grub to wait indefinitely for kernel selection on boot

        * sudo vim /etc/default/grub
        * Comment out GRUB_TIMEOUT_STYLE=hidden
          #GRUB_TIMEOUT_STYLE=hidden
        * Uncomment the following line and modify grub timeout to -1 for
          indefinite wait or 5 for 5secs wait
          #GRUB_TIMEOUT=-1
        * Save the file
        * sudo update-grub

    * sudo reboot
    * Select compiled kernel from "Advanced options for Ubuntu"

* Flash and run steps

   * After Building Binary please follow below steps
   * Untar <flash-files>
   * sudo -E ./scripts/setup_host -u headless
   * sudo -E ./scripts/start_flash_usb.sh caas-flashfiles-eng.<user>.zip --display-off
   * sudo -E ./scripts/start_civ.sh -g GVT-d

Validation results
------------------

This build has been validated on |NUC| Kit `NUC11PAQI7  <https://www.intel.in/content/www/in/en/products/boards-kits/nuc/kits/nuc11paqi7.html>`_  in the following function domains:

=============================  =======  ========
Component                      Results  Comments
=============================  =======  ========
Wi-Fi                          OK        Host wifi is switched to Android UI in QEMU using usb pass through
BT                             OK        Bluetooth is working
Audio Playback                 OK        MP3, AAC-LC, AAC-ELD, HEAAC, HEAAC-V2, VORBIS, OPUS, FLAC, PCM/WAV formats supported
Adb connect over WIFI          OK
Adb connect over Ethernet      OK
Display /Touch and Gesture     OK
Security                       OK
Boot                           OK       Boots on QEMU 4.2.0
Ethernet                       OK
Image Flash                    OK
Web browsing                   OK
Video playback                 OK       H264/H265/MPEG2/VP8/VP9 Video Playback
USB                            OK       Keyboard , Mouse , Pen drive

=============================  =======  ========


Reference configuration
-----------------------

 * Supported hardware

     * Product - NUC11PAQI7


 * Supported software

     * AOSP Version - android-12.0.0_r2
     * NUC11PAQI7 Host Kernel - -5.4.142-cvhb
     * NUC11PAQI7 Guest kernel - -5.4.142-cvhb


Acronyms and terms
------------------

* CIV - Celadon in Virtual Machine


Helpful hints / related documents
---------------------------------

* If you plan to use Celadon in product, please replace all the test keys
  under device/intel/build/testkeys/ with your product key.  
* The release of this project will be signed by test keys, it's only a
  reference for our customer and we are not responsible for this. Customers
  should use their own keys to sign their release images
* Build Celadon in VM  https://01.org/projectceladon/documentation/getting-started/build-source#build-os-image
* Flash Steps : https://01.org/projectceladon/documentation/getting-started/on-vm#build-c-images-running-in-vm

CIV_01.21.03.39_A11
===================
* This is a Production Binary Release for evaluation and development
  purposes . This release is
  supported on |NUC| Kit `NUC11PAQI7  <https://www.intel.in/content/www/in/en/products/boards-kits/nuc/kits/nuc11paqi7.html>`_ Celadon in VM.

Intended audience
-----------------

* Open Source Community who has subscribed to celadon@lists.linuxfoundation.org

Customer support
----------------

* subscribe/unsubscribe celadon mailing list using : https://lists.linuxfoundation.org/mailman/listinfo/celadon

Introduction
------------

New in this release
-------------------

 * New features
    * Power Management - Suspend/Resume - Stability
    * Intel Sensor Hub
    * Config WLAN
    * Audio HDA Mediation
    * Compliance production targets achieved

 * Existing features
    * This release uses start_civ.sh to launch Link -https://docs.01.org/celadon/getting-started/on-vm.html?highlight=start_civ#use-start-civ-sh
    * AAC-LC, AAC-ELD, HEAAC, HEAAC-V2, VORBIS, OPUS, FLAC, PCM/WAV formats
    * Power Management - Suspend/Resume
    * Local Video Playback with Widevine DRM - Level 3
    * External USB Camera
    * API Level 30 & FCM target Level 5
    * Other Changes that came as part of API level Up

      * AIDL for Power and Light HALs
      * Audio & Audio effects HAL 6.0
      * Health HAL 2.1
      * Boot HAL upgraded to 1.1

    * Upgraded Mainline modules
    * Soft restart
    * Updatable APEX
    * Config store HAL deprecated
    * Graphics Memory Allocator (Gralloc) 4.0
    * HWC 2.4 support for Display
    * Trusty Hardware Seed binding
    * Power Management - Suspend,Resume
    * Android\* key Input Manager Framework is implemented for Power &
      Volume buttons
    * Integrated Sensor Hub Enablement for Android Supported Sensors
    * Android Thermal HAL and Thermal Manager Service
    * BZIP2 performance improvements
    * Bluetooth Control from Android in VM
    * HDMI Audio Output Support
    * Virtio-gpu Support
    * SDHCI mediation enabled and supported SD card

      * CIV launch script for SD Card: sudo -E ./scripts/start_civ.sh -d GVT-d -b /dev/mmcblk0p1 --passthrough-pci-usb

    * Graphics GVT-d support
    * HDMI and DP display support
    * Mass Storage USB 2.0 and 3.x devices is supported
    * Adb over WIFI and Ethernet is supported
    * Audio playback over USB Headset, 3.5mm and HDMI are supported
    * Setting Proxy for Wireless Network
    * Wi-Fi 802.11 a/b/g/n/ac/ax and Bluetooth 4.2
    * Ethernet works fine with Ethernet to USB converter
    * Wifi Control from Android in VM using usb passthrough
    * To passthrough USB host controller in NUC11PAQI7, run the CIV launch
      script like this: sudo E ./scripts/start_civ.sh -g GVT-d --passthrough-pci-usb
    * Power Management - Shutdown and Reboot
    * Android Time keeping with Host OS
    * Product Information to Guest OS
    * ODM partition for vendor customizations
    * Only logitech C922 pro stream webcam is supported for all camera
      related testing
    * HW Video Codecs support on celadon

        **Decoder**

            * AVC High profile @ Level 5.1 (4k@30fps)
            * HEVC Main and Main 10 profile @ Level 5 (4k@30fps)(Main 10
              with BT2020 and ST2084 information is not supported)
            * VP9 profile 0 @ Level 5 (4k@30fps)
            * Vp8 8 bits 1080p@60fps

        **Encoder**

            * AVC High profile @ level 4.1 (1080P@30fps)
            * HEVC Main profile @ Level 4 (1080P@30fps)

    * Audio decoders supported: MP3, AAC-LC, AAC-ELD, HEAAC, HEAAC-V2,
      VORBIS, OPUS, MIDI, FLAC, PCM/WAV
    * Generic storage HAL supported
    * SATA emulation is supported
    * 9pfs based file transfer
    * Security SELinux enforcing, Trusty TEE, File Based Encryption, Trusty,
      Keymaster 3.0

         * User guide:

            * SELinux Configuration and Rules
            * How to Enable or Disable Trusty for Debugging

 * Changes to existing features
    * Dynamic routing to HDMI audio devices

 * Unsupported or discontinued features


Known issues
------------

* Android UI Flicker when booted with eDP Display
* Blank screen is displayed while video playback
  [Configuration : GLrenderer-Virtio] & [GLrenderer-Softpipe]
* Camera Preview Flickers while using MultiCamera application
* IPV6 network does not work for usb2ethernet converter in recovery mode
* Modification of  time zone when "Use network-provided time" should be disabled


Where to find the release
-------------------------

* Manifest Link : https://github.com/projectceladon/manifest/blob/master/stable-build/CIV_01.21.03.39_A11.xml
* Binary Link : https://github.com/projectceladon/celadon-binary/tree/master/CIV_00.21.03.39_A11

System Requirements
-------------------
* Recommended system requirements for Host:
    * CPU:  4 cores or more
    * RAM:  8 GB or more
    * Hard-Disk: 250 GB [Desired]

How to install this release
---------------------------

* Steps to sync to this release

   * repo init -u https://github.com/projectceladon/manifest -b master -m stable-build/CIV_XX.XX.XX.XX_AXX.xml
   * NOTE : Manifest tag will change according to the latest release
   * repo sync -c -q -j${nproc}

* Android build commands

   * For Compilation please use Ubuntu 18.04
   * source build/envsetup.sh
   * lunch caas-userdebug
   * make flashfiles -jN

* Steps To build the host kernel for this manifest

    * Download  caas-releasefiles-userdebug.tar.gz and put it under ~/civ
    * cd ~/civ && tar zxvf caas-releasefiles-userdebug.tar.gz
    * cd patches/kernel/lts2019-chromium
    * ./build_weekly.sh
    * Deb files will be generated in
      patches/kernel/lts2019-chromium/host_kernel
    * sudo dpkg -i \*.deb
    * Update grub to wait indefinitely for kernel selection on boot

        * sudo vim /etc/default/grub
        * Comment out GRUB_TIMEOUT_STYLE=hidden
          #GRUB_TIMEOUT_STYLE=hidden
        * Uncomment the following line and modify grub timeout to -1 for
          indefinite wait or 5 for 5secs wait
          #GRUB_TIMEOUT=-1
        * Save the file
        * sudo update-grub

    * sudo reboot
    * Select compiled kernel from "Advanced options for Ubuntu"

* Flash and run steps

   * Download flash-files [https://github.com/projectceladon/celadon-binary]
   * Untar <flash-files>
   * sudo -E ./scripts/setup_host -u headless
   * sudo -E ./scripts/start_flash_usb.sh caas-flashfiles-eng.<user>.zip --display-off
   * sudo -E ./scripts/start_civ.sh -g GVT-d

Validation results
------------------

|C| build has been validated on |NUC| Kit `NUC11PAQI7  <https://www.intel.in/content/www/in/en/products/boards-kits/nuc/kits/nuc11paqi7.html>`_  in the following function domains:

=============================  =======  ========
Component                      Results  Comments
=============================  =======  ========
Wi-Fi                          OK        Host wifi is switched to Android UI in QEMU using usb pass through
BT                             OK        Bluetooth is working
Audio Playback                 OK        MP3, AAC-LC, AAC-ELD, HEAAC, HEAAC-V2, VORBIS, OPUS, FLAC, PCM/WAV formats supported
Adb connect over WIFI          OK
Adb connect over Ethernet      OK
Display /Touch and Gesture     OK
Security                       OK
Boot                           OK       Boots on QEMU 4.2.0
Ethernet                       OK
Image Flash                    OK
Web browsing                   OK
Video playback                 OK       H264/H265/MPEG2/VP8/VP9 Video Playback
USB                            OK       Keyboard , Mouse , Pen drive

=============================  =======  ========


Reference configuration
-----------------------

 * Supported hardware

     * Product - NUC11PAQI7


 * Supported software

     * AOSP Version - android-11.0.0_r39
     * NUC11PAQI7 Host Kernel - -5.4.142-cvhb
     * NUC11PAQI7 Guest kernel - -5.4.142-cvhb


Acronyms and terms
------------------

* CIV - Celadon in Virtual Machine


Helpful hints / related documents
---------------------------------

* If you plan to use Celadon in product, please replace all the test keys
  under device/intel/build/testkeys/ with your product key.  
* The release of this project will be signed by test keys, it's only a
  reference for our customer and we are not responsible for this. Customers
  should use their own keys to sign their release images
* Build Celadon in VM  https://01.org/projectceladon/documentation/getting-started/build-source#build-os-image
* Flash Steps : https://01.org/projectceladon/documentation/getting-started/on-vm#build-c-images-running-in-vm

