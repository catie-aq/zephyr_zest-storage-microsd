# Zest_Storage_microSD

Zest_Storage_microSD board enables the use of microSD card with Zephyr OS.

## Usage

1. Add the Zest_Storage_microSD shield to your workspace using the [6TRON module](https://github.com/catie-aq/zephyr_6tron-manifest.git).
2. Compile and flash application using `west` tool:
   - Shield name: `zest_storage_microsd`

## Recommended configuration

If you want to use a FatFS file system on a FAT SD card, you should add the following configuration to your `prj.conf` file:

```Kconfig
CONFIG_DISK_ACCESS=y
CONFIG_DISK_DRIVER_SDMMC=y
CONFIG_FILE_SYSTEM=y
CONFIG_FILE_SYSTEM_MKFS=y # Allow to format file system
CONFIG_FS_FATFS_MKFS=y
CONFIG_FS_FATFS_MOUNT_MKFS=y
CONFIG_FAT_FILESYSTEM_ELM=y
CONFIG_FS_FATFS_LFN=y # Long file names (more than 8 char)
```

**Note**  
On STM32 you may need to lower the default SPI frequency defined if the shield overlay.  
10 MHz clock has been succesfully tested on STM32L4ARG:  
`spi-max-frequency = <10000000>;`