# Setup latest image on microSD card
## Get disk number
diskutil list

## Set variables
* NUMBER=<disk number>
* RASPBIAN=`ls <PATH TO IMAGE>`

## Unmount
```
diskutil unmountDisk /dev/disk${NUMBER}
sudo dd bs=1m if=${RASPBIAN} of=/dev/rdisk${NUMBER}
```

# After Pi online
## Resize root partition
`sudo raspi-config`

## Set current over USB to 1.2A (default is 600mA)
`sudo sh -c "echo max_usb_current=1 >> /boot/config.txt`

## Use vi on CLI
`sudo sh -c "echo \"set -o vi\" >> /etc/profile"`

## Alias for ll
`sudo sh -c "echo \"alias ll='ls -l'\" >> /etc/bash.bashrc"`
