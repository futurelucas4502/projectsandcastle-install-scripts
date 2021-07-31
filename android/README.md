# Project Sandcastle - Android build

## Disclaimer
These are modified versions of the scripts found on the Project Sandcastle website and a script from the pongoOS repo I do not take credit for these nor am I associated with the development of either project.

If you would prefer to use the original copies the things changed are as follows:
* Removed `load-linux.mac`
* Added load_linux.py from [here](https://github.com/checkra1n/pongoOS/blob/master/scripts/load_linux.py)
* Edited isetup removing all references to binpack e.g. remove the shebang and change things like `/binpack/usr/local/bin/wget` to just `wget`.
* Edited `start_mac.sh` changing the 3rd line from the bottom from `./load-linux.mac Android.lzma dtbpack` to `./load_linux.py -k Android.lzma -d dtbpack`.
* Then just follow the instructions below


## Install instructions :
Caution - This will create a new volume on APFS. This should not hurt your ability to boot iOS. But if you are not willing to restore your device. Do not try this as it's still beta.

Firstly if needed change the passwords and port in `setup_mac.sh` to the correct ssh password and port for your device.

Next make sure you are using python3 and pip install pyusb.

### MAC:
Connect your iPhone to your computer by USB.
You must have checkra1n installed in Applications to run this.
Use checkra1n to jailbreak your device and boot into iOS.
Open a terminal window and run `./setup_mac.sh` - This is a one time setup and doesn’t need to be repeated for the same device.
Once setup is complete you can put your device into DFU mode and run `./start_mac.sh` to boot Android.


### Linux:
Connect your iPhone to your computer by USB.
Use checkra1n to jailbreak your device and boot into iOS.
Copy the isetup file to `/tmp/setup.sh` on the iPhone via scp or other means.
Run `chmod 755 /tmp/setup.sh && /tmp/setup.sh` on the iPhone via ssh or NewTerm 2
Once setup is complete run `./load_linux.py -k Android.lzma -d dtbpack` in a terminal on the computer.


## Removing it (*THIS DOES NOT WORK*):
If you wish to remove the Android NAND image and reclaim the space you can login via SSH to your checkra1ned device and mount the final volume and remove the nand file. To do this run ls /dev/disk0s1s* and find the last volume. You can verify its the right volume by running /System/Library/Filesystems/apfs.fs/apfs.util -p VOLUME_HERE and if it says Android, that's the correct one. Once you have the volume path you can then run 
mkdir -p /tmp/mnt 
mount -t apfs VOLUME_HERE /tmp/mnt 
rm -rf /tmp/mnt/nand
umount /tmp/mnt
sync

And that will reclaim the space for you.

