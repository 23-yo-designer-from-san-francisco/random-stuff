Create an empty .img
```zsh
dd if=/dev/zero of=/Volumes/ram/windows.img bs=1m count=6000
```

Mount the img:
```zsh
hdiutil attach -noverify -nomount /Volumes/ram/windows.img
```

Get partition number:
```zsh
diskutil list | grep -A2 "disk image"
```

Create partitions:
```zsh
sudo diskutil partitionDisk disk6 GPT FAT32 BOOT 200M ExFat Windows 5.7G
```

>Copy boot files from Rufus UEFI iso to partition 1

>Copy Windows install files to partition 2
