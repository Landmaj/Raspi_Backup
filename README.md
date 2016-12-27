# Backup script for Raspberry Pi
This script does an image backup of the Pi SD card using dd. This version was heavily modified from the original (link in credits). I removed an option to gzip backup image in favor of a second script (not mine, link in credits) which reduces img file to its minimum possible size. This method is faster and allows to restore backup to smaller sd card.

I also added email notification after successful (or failed) backup. It requires installed and configured ssmtp.

## Installation
- Clone this repo into the folder where you keep your housekeeping scripts.
- Modify the DIR variable to point to your destination
- (optional) Modify RESIZE_LOCATION variable to point to .resizeimage.pl script
- Update services stop and start sections to reflect your installated services
- Make executable. ```chmod +x backup.sh```
- Update crontab to run it each week

___Example (based on my setup using DietPi and NAS)___

1. Create directory /mnt/backup and edit /etc/fstab to mount an NFS share to this location
2. Copy ```.raspibackup.sh``` and ```.resizeimage.pl``` to ```/mnt/backup``` and run ```chmod +x /mnt/backup/.raspibackup.sh```
3. Create ```/etc/cron.weekly/backup``` with following content:
```
#!/bin/bash
/mnt/backup/.raspibackup.sh
```
4. Make it executable - ```chmod +x /etc/cron.weekly/backup```
5. And see if it work ```bash /etc/cron.weekly/backup```


## CREDITS
This script started from
   <http://raspberrypi.stackexchange.com/questions/5427/can-a-raspberry-pi-be-used-to-create-a-backup-of-itself>
 which in turn started from
   <http://www.raspberrypi.org/phpBB3/viewtopic.php?p=136912>
Resize scripts comes from
  https://www.raspberrypi.org/forums/viewtopic.php?f=91&t=58069