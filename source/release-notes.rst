.. _release-notes:

Release Notes
#############

.. note::
    
    Refer to :ref:`release-naming-convention` to decode the release tags of
    the following |C| releases.

.. contents::
   :local:
   :depth: 1

Stable Releases
***************

This is a Production Release for evaluation and development purposes
addressing Retail, Education, Workload consolidation and Marine segments.

.. contents::
   :local:
   :depth: 1

CIV_02.22.04.50_A12
===================

Intended audience
-----------------

* Celadon Open Source Community who has subscribed to celadon@lists.linuxfoundation.org

Customer support
----------------

* subscribe/unsubscribe celadon mailing list using :
  https://lists.linuxfoundation.org/mailman/listinfo/celadon

Introduction
------------

Feature Details
~~~~~~~~~~~~~~~

Celadon upstreamed fixes in this release:

* First stable release from Celadon_IoT for Android 12
* This release supports Alder Lake-S (ADL-S)
* IoT configuration supports SRIOV mode with 99.97% conformance on
  Alder Lake (ADL)
  platform with production ready
* Vm-Manager support to launch Android


Release Constraint list
-----------------------

* VP9 hardware codec is not enabled in the current release due to hardware constraint
* Sensor support is not enabled in current release due to hardware constraint.
* The current QEMU release doesn’t support RGBA8888 color format which impact RGBA8888 usage on Android guest os application
* USB accessory mode is not supported in the current release.
* MAC randomization feature is not supported in the current release.
* Partner modules aren’t integrated within the current GMS package.
* NN API is not supported in the current release.
* Hardware doesn’t have inbuilt cameras, only usb external camera is supported.

Known issues
------------
* Ethernet tethering option in Settings menu is active even when no USB Ethernet Adaptor connected
* System touch can’t accurately point the location
* With UserData CheckPoint feature enabled, device reboots after 1st time boot while flashing is done
* Windows freeform feature has been partially backported from Android T

Open Issue List
---------------
* :sup:`#`\16019209010	VtsHalMediaC2V1_0TargetVideoDecTest module
* 16017487117	x86_64 CtsMediaTestCases failures
* 16017342135	STS CtsSecurityTestCases failing
* 16018517871	CtsMediaV2TestCases failures related to HEVC profilelevel
* 16017974748	Failures are observed with x86_64 CtsDeqpTestCases module

Where to find the release
-------------------------

* Manifest Link: https://github.com/projectceladon/manifest/blob/master/stable-build/CIV_02.22.04.50_A12.xml
* :sup:`#`\PRs fixing this issue in repo : https://github.com/projectceladon/vendor-intel-utils-vertical-iot/pulls?q=is%3Apr+is%3Amerged
  [PR#9, PR#10, PR#11, PR#16, PR#17, PR#19]
* Below validation results are with release manifest + cherrypicked PR's

Host Kernel Release configuration
---------------------------------

* linux-intel-lts kernel
        * Branch: https://github.com/intel/linux-intel-lts
        * SHA ID: https://github.com/intel/linux-intel-lts/releases/tag/lts-v5.15.71-adl-linux-221121T044440Z
* kernel-config
        * Config-File: https://github.com/projectceladon/vendor-intel-utils-vertical-iot/blob/main/x86_64_defconfig

Reference configuration
-----------------------

* Supported hardware
    =======================   =======
    Platform                  Product
    -----------------------   -------
    Alder Lake(ADL)           | ADL RVP DDR5 C1 CPU 12th Gen Intel(R) Core(TM) i9-12900E
    Network Interface Card    | Intel® Wireless-AC 9260 5th Generation Intel802.11ac, Dual Band, 2x2Wi-Fi + Bluetooth®5.1
    =======================   =======

* Supported software
        * Android CIV Guest:
                =======================   =======
                Platform                  Product
                -----------------------   -------
                Android                   | Android 12
                Kernel                    | 5.10.145 (lts-v5.10.145-civ-android-221027T031053Z)
                AOSP                      | android-12.0.0_r28
                =======================   =======

        * Ubuntu Host:
                =======================   =======
                Platform                  Product
                -----------------------   -------
                Qemu                      | version 7.1.0
                Ubuntu                    | 22.04 LTS (Jammy Jellyfish)
                Kernel_IoTG               | 5.15.71 (lts-v5.15.71-adl-linux-221121T044440Z)
		=======================   =======

Validation results
------------------

Stable Releases (IoT) are validated with SR-IOV mode on an Alder Lake (ADL)
platform in the following function domains. Validation cycles are performed on
a GMS user-signed, widevine-enabled image, as required by google certification
requirements.

Below validation results are with Alder Lake-S (ADL-S) RVP platform.

.. figure:: stable-release_iot/images/Q422-2-A12_Validation_Result.png
    :width: 500px

.. note::

   \*CTS on GSI failures are a subset of CTS failures, so the overall failures
   count is 39.
