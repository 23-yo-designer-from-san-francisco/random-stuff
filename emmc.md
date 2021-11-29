[Get wear levels](https://electronics.stackexchange.com/questions/218914/how-long-until-my-emmc-is-dead)

```bash
RES=`sudo cat /sys/kernel/debug/mmc0/mmc0:0001/ext_csd`
typea="${RES:536:2}" ;
typeb="${RES:538:2}" ;
typead=`echo "ibase=16; $typea"|bc`
typebd=`echo "ibase=16; $typeb"|bc`
echo "Type A percent: $((typead * 10)) %"
echo "Type B percent: $((typebd * 10)) %"
```

Install `mmc-tools`

Get the complete output
```bash
sudo mmc extcsd read /dev/mmcblk0
```

Or just lifetime info
```bash
mmc extcsd read /dev/mmcblk0 | grep -A 1 LIFE
```
