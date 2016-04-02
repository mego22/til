# Install
sudo apt-get install -y avahi-daemon netatalk hfsplus hfsutils hfsprogs

# Setup
1. Format drive.
1. Get UUID of device: `sudo blkid <DEVICE>
1. Add entry to `/etc/fstab` for USB drive.
  `UUID=<UUID> /mnt/<DIR> ext4 nofail,auto,noatime,rw,user    0   0`
1. Mount USB drive.
1. Copy in `/etc/netatalk/afpd.conf`, `/etc/netatalk/AppleVolumes.default` and `/etc/avahi/services/afpd.service`
1. Start services: `service avahi-daemon start; service netatalk start`
1. Enable serivces on boot: `update-rc.d netatalk defaults, update-rc.d avahi-daemon defaults`

### /etc/netatalk/AppleVolumes.default
```
# Netatalk defaults applied to shares
:DEFAULT: options:upriv,usedots cnidscheme:dbd
dbpath:/var/dbd/AppleDB/$v allowed_hosts:10.0.0.0/24

# User's home directory available as user's username
~/ "$u"

# Time Machine volume
/mnt/<MOUNT> "<NAME>" allow:<USER> options:usedots,upriv,tm
```

### /etc/netatalk/afpd.conf
```
# AFPd Logging
- -setuplog "AFPDaemon log_info /var/log/netatalk/afpd.log" \
  -setuplog "UAMSDaemon log_info /var/log/netatalk/uams.log" \

"<NAME>" -tcp -noddp -nosavepassword -nosetpassword -nodebug
-nouservolfirst -nouservol -closevol \
  -mimicmodel AirPort \
  -ipaddr <IP> \
  -port 548 \
  -unixcodepage utf8 \
  -volnamelen 255 \
  -uampath /usr/lib/netatalk \
  -uamlist uams_dhx2_passwd.so,uams_guest.so \
  -defaultvol /etc/netatalk/AppleVolumes.default \
  -systemvol /etc/netatalk/AppleVolumes.system \
  -sleep 168 -setuplog "Default log_info /var/log/netatalk/netatalk.log"
```

### /etc/avahi/services/afpd.service
```
<?xml version="1.0" standalone='no'?><!--*-nxml-*-->
<!DOCTYPE service-group SYSTEM "avahi-service.dtd">
<service-group>
    <name replace-wildcards="yes">%h</name>
    <service>
        <type>_afpovertcp._tcp</type>
        <port>548</port>
    </service>
    <service>
        <type>_device-info._tcp</type>
        <port>0</port>
        <txt-record>model=TimeCapsule</txt-record>
    </service>
</service-group>
```

## Refernce
http://www.xdracco.net/time-machine-backup-volume-on-ubuntu-server/#codesyntax_4
