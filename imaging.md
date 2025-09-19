# Imaging

## ISO Files

* `sha256sum /path/to/your/iso.iso` or `md5sum /path/to/your/iso.iso` to verify the hash of the downloaded iso
* `sudo umount /dev/sdX1` to unmount the partition and then run `sudo dd if=/path/to/file.iso of=/dev/sdX bs=4M status=progress oflag=sync` to image an ISO onto a flash drive
* `stat -c '%s' /path/to/your/iso.iso` to get the size (XXXXXXXXXX) of the ISO file
* `sudo head -c XXXXXXXXXX /dev/sdX | sha256sum` to get the hash of the first XXXXXXXXXX bytes to see if the data was written correctly to the disc