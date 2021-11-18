[Source](https://www.freecodecamp.org/news/how-make-a-windows-10-usb-using-your-mac-build-a-bootable-iso-from-your-macs-terminal/)


Erase USB Drive

```zsh
diskutil eraseDisk MS-DOS "WIN10" GPT /dev/diskX
```

Mount the ISO

```zsh
hdiutil mount <PATH_TO_ISO>
```

Copy all files excluding install.wim

```zsh
rsync -vha --progress --exclude=sources/install.wim /Volumes/CCCOMA_X64FRE_EN-US_DV9/* /Volumes/WIN10
```

Split the image

```zsh
wimlib-imagex split /Volumes/CCCOMA_X64FRE_EN-US_DV9/sources/install.wim /Volumes/WIN10/sources/install.swm 3800
```
