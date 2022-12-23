just add a key to your encrypted device with pbkdf2,

```
cryptsetup luksAddKey -S 1 --pbkdf pbkdf2 /dev/sdxy
```

which assumes that the key slot 1 is free (you can find free key slots by inspecting cryptsetup `luksDump /dev/sdxy`).

Then, in your less powerful computer, unlock the device with

```
cryptsetup luksOpen -S 1 /dev/sdxy name
```

The -S 1 is essential, otherwise the more expensive key may be tried and the OOM killer triggered all the same.