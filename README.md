# ramdrive-nud
Handle with care!

**Make backups of your wallet files.**

You have backups?


Then you might continue :)


- **First you need to create a directory for the ramdrive at "/ramdrive":**

$sudo mkdir /ramdrive

- **Now you make a ramdrive of that folder, by editing /etc/fstab.**

Open /etc/fstab and append the "tmpfs... " line:

$sudo nano /etc/fstab

$tmpfs /ramdisk tmpfs defaults,noatime,nosuid,nodev,noexec,mode=1777,size=16M 0 0


- **Then you need to move your wallet files (you have backup?):**

$mv ~/.nu/walletB.dat ~/.nu/walletB.dat.ramdrive

$mv ~/.nu/walletS.dat ~/.nu/walletS.dat.ramdrive


- **Optionally you can enter two lines to your crontab,

which make a backup of you wallet files each 4 hours:**

$crontab -e

00 0,4,8,12,16,20 * * * [path-to-ramdrive-nud]/backup-wallet-nsr-tmpfs

00 0,4,8,12,16,18 * * * [path-to-ramdrive-nud]/backup-wallet-nbt-tmpfs

