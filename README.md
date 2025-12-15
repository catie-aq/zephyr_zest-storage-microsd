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

- In case you need to specify a specific disk name instead of the default `"SD"`, use the second macro:
  ``````c
  ZEST_STORAGE_MICROSD_DISKNAME(1, "CUSTOM_NAME") /* Zest_Storage_microSD connected to Zest_Core first port with a custom disk-name */
  ``````

- In case you need to specify a custom spi device, instead of the default `sixtron_connector_##port##_spi`, you will need to redefine `spi_zest_storage_microsd_##port` before calling `DRIVERS_ZEST_STORAGE_MICROSD` macro, e.g.:
  ``````c
  spi_zest_storage_microsd_1: &spi1 {}; /* custom spi used by the macro */
  DRIVERS_ZEST_STORAGE_MICROSD(1, "SD") /* Zest_Storage_microSD connected to Zest_Core first port with a custom spi device and a custom disk-name */
  ``````

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
> On STM32 targets, you may need to lower the default SPI frequency defined if the shield overlay. A 10 MHz clock has been succesfully tested on the Zest_Core STM32L4ARG. Update your `sdhc_zest_storage_microsd_##1` accordingly, e.g.:
>
> ``````
> &sdhc_zest_storage_microsd_1{
> 	spi-max-frequency = <10000000>;
> };
> ``````
