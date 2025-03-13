# Zest_Storage_microSD

Zest_Storage_microSD board support for Zephyr OS.

## Usage

:pushpin: This shield defines:

- a SDHC controller: `sdhc_zest_storage_microsd_<port>`

:triangular_ruler: To use this shield:

- Update your device tree by adding the `ZEST_STORAGE_MICROSD(port)` macro to the `app.overlay` file.\
  Replace `port` with the number of the Zest_Core port to which the shield is connected, e.g.:

  ```c
  ZEST_STORAGE_MICROSD(1) /* Zest_Storage_microSD connected to Zest_Core first port */
  ```

- Activate support for the shield by adding `--shield zest_storage_microsd` to the west command.

## Recommended configuration

To use a FatFs file system on a SD card, add the following configuration to your `prj.conf` file:

```Kconfig
CONFIG_DISK_ACCESS=y
CONFIG_FILE_SYSTEM=y
CONFIG_FAT_FILESYSTEM_ELM=y # Use the ELM FAT file system implementation

CONFIG_FILE_SYSTEM_MKFS=y # Optional, enables formatting a storage device
CONFIG_FS_FATFS_MKFS=y # Optional, adds FatFs formatting
CONFIG_FS_FATFS_MOUNT_MKFS=y # Optional, adds auto-formatting if mounting fails

CONFIG_FS_FATFS_LFN=y # Optional, allows longer filenames (different from 8.3 format)
```

> [!NOTE]
> On STM32 targets, you may need to lower the default SPI frequency defined if the shield overlay. A 10 MHz clock has been succesfully tested on the Zest_Core STM32L4ARG.
> `spi-max-frequency = <10000000>;`
