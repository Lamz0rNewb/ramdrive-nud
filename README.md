# ramdrive-nud
# Handle with care!

**Make backups of your wallet files.**

**You have backups?**

**Then you might continue :)**

**Run at own risk!**


# Initialize

- **First you need to create a directory for the ramdrive at "/ramdisk":**

`sudo mkdir /ramdisk`


- **Now you make a ramdrive of that folder, by editing /etc/fstab.** Open /etc/fstab and append the "tmpfs... " line:

`sudo nano /etc/fstab`

`tmpfs /ramdisk tmpfs defaults,noatime,nosuid,nodev,noexec,mode=1777,size=16M 0 0`

The entry in /etc/fstab requires a system restart to become active. If you don't want to restart now, you can mount the ramdisk manually:

`sudo mount -t tmpfs -o size=16M tmpfs /ramdisk/`


- **Then you need to move your wallet files (you have backup?):**

`mv ~/.nu/walletB.dat ~/.nu/walletB.dat.ramdisk`

`mv ~/.nu/walletS.dat ~/.nu/walletS.dat.ramdisk`


- **Optionally you can enter two lines to your crontab, which make a backup of you wallet files each 4 hours:**

`crontab -e`

`00 0,4,8,12,16,20 * * * [path-to-"ramdrive-nud"]/backup-wallet-nsr-tmpfs`

`00 0,4,8,12,16,18 * * * [path-to-"ramdrive-nud"]/backup-wallet-nbt-tmpfs`


# Run nud with wallets on ramdrive

You can start nud with wallets on ramdrive with `ramnud-run` and stop it with `ramnud-stop`. `nud stop` RPC still works, but the ramnud-stop script makes writes a backup of the wallet files to ~/.nu/ and is the preferred way to work with this ramdrive edition.

**Regarding the backup-wallet-nbt-tmpfs/backup-wallet-nsr-tmpfs scripts**: Make sure to have `nud` on a location like "/bin/", because crontab has only limited knowledge of environmental variables. The backup might not work if crontab ca't execute nud.
