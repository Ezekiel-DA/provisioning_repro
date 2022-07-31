# BLE provisioning issue reproduction

Build, then, from a command line with esptool.py available (version does not appear to matter?) - changing paths to your local as needed:
```
esptool.py --chip esp32s3 --port "COM4" --baud 460800 --before default_reset --after hard_reset write_flash -z --flash_mode dio --flash_freq 80m --flash_size 8MB 0x0000 C:\Users\nicol\.platformio\packages\framework-arduinoespressif32\tools\sdk\esp32s3\bin\bootloader_dio_80m.bin 0x8000 C:\Users\nicol\OneDrive\Documents\PlatformIO\Projects\provisioning_repro\.pio\build\ESP32-S3\partitions.bin 0xe000 C:\Users\nicol\.platformio\packages\framework-arduinoespressif32\tools\partitions\boot_app0.bin 0x10000 .pio\build\ESP32-S3\firmware.bin
```

This "fails": BLE provisioning works, but credentials are never saved.


This works:
```
esptool.py --chip esp32s3 --port "COM4" --baud 460800 --before default_reset --after hard_reset write_flash -z --flash_mode dio --flash_freq 80m --flash_size 8MB 0x0000 C:\Users\nicol\.platformio\packages\framework-arduinoespressif32\tools\sdk\esp32s3\bin\bootloader_qio_80m.bin 0x8000 C:\Users\nicol\OneDrive\Documents\PlatformIO\Projects\provisioning_repro\.pio\build\ESP32-S3\partitions.bin 0xe000 C:\Users\nicol\.platformio\packages\framework-arduinoespressif32\tools\partitions\boot_app0.bin 0x10000 .pio\build\ESP32-S3\firmware.bin
```

Note the difference: despite specifying `--flash_mode= dio`, we upload the *QIO* bootloader.
