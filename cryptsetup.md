# cryptsetup

## Encrypted External Drives

Tested using Ubuntu 16.04

Partition & erase drive:

```
sudo fdisk /dev/sdf

```

Encrypt drive:

```
sudo apt install cryptsetup
sudo cryptsetup --verify-passphrase luksFormat /dev/sdf1 -c aes -s 256 -h sha256
sudo cryptsetup luksOpen /dev/sdf1 /mnt/DriveName
sudo cryptsetup luksOpen /dev/sdf1 DriveName
```
