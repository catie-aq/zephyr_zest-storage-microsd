# Zest_Storage_microSD

Zest_Storage_microSD board enables the use of microSD card with Zephyr OS.

## Usage

1. Add the Zest_Storage_microSD shield to your workspace using the [6TRON module](https://github.com/catie-aq/zephyr_6tron-manifest.git).
2. Compile and flash application using `west` tool:
   - Shield name: `zest_storage_microsd`

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