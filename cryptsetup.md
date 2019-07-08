# cryptsetup

## Encrypted External Drives

Tested using Ubuntu 16.04

Assumes a drive path of `/dev/sdf`; and a drive label of `DriveName`

Partition & erase drive:

```
sudo fdisk /dev/sdf

```

Encrypt drive:

```
sudo apt install cryptsetup
sudo cryptsetup --verify-passphrase luksFormat /dev/sdf1 -c aes -s 256 -h sha256
```

Open encrypted partition:

```
sudo cryptsetup luksOpen /dev/sdf1 DriveName
```

Erase partiton:

```
sudo mkfs.ext4 /dev/mapper/DriveName -L DriveName
```

(Optional if using `ext4` filesystem) Get rid of reserved space on drive:

```
sudo tune2fs -m 0 /dev/mapper/DriveName
```

Finally, eject drive and re-mount.
