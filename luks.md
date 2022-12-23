Your volume is probably encrypted with LUKS, here's how to mount it:

You need:

```
sudo apt-get install cryptsetup
```

To decrypt the volume:

```
sudo cryptsetup luksOpen /dev/sda1 my_encrypted_volume
```

Now you can mount it as usual:

```
sudo mkdir /media/my_device
sudo mount /dev/mapper/my_encrypted_volume /media/my_device
```

To lock the container again, it needs to be unmounted first:

```
sudo umount /media/my_device
sudo cryptsetup luksClose my_encrypted_volume
```

To automatically put it in the /media location, use the udisks tool

```sudo udisks --mount /dev/mapper/my_encrypted_volume
```
