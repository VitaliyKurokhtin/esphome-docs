ESP32 Platform
==============

.. seo::
    :description: Configuration for the ESP32 platform for ESPHome.
    :image: esp32.svg

This component contains platform-specific options for the ESP32 platform.

.. code-block:: yaml

    # Example configuration entry
    esp32:
      board: nodemcu-32s

Configuration variables:
------------------------

- **board** (**Required**, string): The PlatformIO board ID that should
  be used. Choose the appropriate board from
  `this list <https://registry.platformio.org/packages/platforms/platformio/espressif32/boards>`__ (the icon next to the name
  can be used to copy the board ID). *This only affects pin aliases, flash size and some internal settings*, if unsure
  choose a generic board from Espressif such as ``esp32dev``.
- **framework** (*Optional*): Options for the underlying framework used by ESPHome.
  See :ref:`esp32-arduino_framework` and :ref:`esp32-espidf_framework`.
- **variant** (*Optional*, boolean): The variant of the ESP32 that is used on this board. One of ``esp32``, 
  ``esp32s2``, ``esp32s3``, ``esp32c3`` and ``esp32h2``. Defaults to the variant that is detected from the board, if
  a board that's unknown to ESPHome is used, this option is mandatory.

.. _esp32-arduino_framework:

Arduino framework
-----------------

This is the default framework for ESP32 chips at the moment.

.. code-block:: yaml

    # Example configuration entry
    esp32:
      board: nodemcu-32s
      framework:
        type: arduino
        version: 2.0.0

- **version** (*Optional*, string): The base framework version number to use, from
  `ESP32 arduino releases <https://github.com/espressif/arduino-esp32/releases>`__. Defaults to ``recommended``. Additional values are:

  - ``dev``: Use the latest commit from https://github.com/espressif/arduino-esp32, note this may break at any time
  - ``latest``: Use the latest *release* from https://github.com/espressif/arduino-esp32/releases, even if it hasn't been recommended yet.
  - ``recommended``: Use the recommended framework version.

- **source** (*Optional*, string): The PlatformIO package or repository to use for framework. This can be used to use a custom or patched version of the framework.
- **platform_version** (*Optional*, string): The version of the `platformio/espressif32 <https://github.com/platformio/platform-espressif32/releases/>`__ package to use.

.. _esp32-espidf_framework:

ESP-IDF framework
-----------------

This is an alternative base framework for ESP32 chips, and recommended for variants
of the ESP32 like ESP32S2, ESP32S3, ESP32C3 and single-core ESP32 chips.

.. code-block:: yaml

    # Example configuration entry
    esp32:
      board: esp32-c3-devkitm-1
      framework:
        type: esp-idf
        version: recommended
        # Custom sdkconfig options
        sdkconfig_options:
          CONFIG_COMPILER_OPTIMIZATION_SIZE: y
        # Advanced tweaking options
        advanced:
          ignore_efuse_mac_crc: false

- **version** (*Optional*, string): The base framework version number to use, from
  `ESP32 ESP-IDF releases <https://github.com/espressif/esp-idf/releases>`__. Defaults to ``recommended``. Additional values are:

  - ``dev``: Use the latest commit from https://github.com/espressif/esp-idf, note this may break at any time
  - ``latest``: Use the latest *release* from https://github.com/espressif/esp-idf/releases, even if it hasn't been recommended yet.
  - ``recommended``: Use the recommended framework version.

- **source** (*Optional*, string): The PlatformIO package or repository to use for the framework. This can be used to use a custom or patched version of the framework.
- **platform_version** (*Optional*, string): The version of the `platformio/espressif32 <https://github.com/platformio/platform-espressif32/releases/>`__ package to use.
- **sdkconfig_options** (*Optional*, mapping): Custom sdkconfig options to set in the ESP-IDF project.
- **advanced** (*Optional*, mapping): Advanced options for highly specific tweaks.

  - **ignore_efuse_mac_crc** (*Optional*, boolean): Can be set to ``true`` for devices on which the burnt in MAC address does not
    match the also burnt in CRC for that MAC address, resulting in an error like ``Base MAC address from BLK0 of EFUSE CRC error``.

See Also
--------

- :doc:`esphome`
- :ghedit:`Edit`
