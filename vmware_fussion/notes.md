http://www.vmware.com/pdf/vix180_vmrun_command.pdf
http://socalledgeek.com/blog/2012/8/23/fixed-dhcp-ip-allocation-in-vmware-fusion

IP of VM
*Needs guest tools installed
vmrun getGuestIPAddress <path to vmx>

DHCP hardcode
MAC=grep ethernet0.generatedAddress ~/Documents/Virtual\
Machines.localized/*/*.vmx | grep -v Offset

subnet=`awk '/subnet/,/\}/' "/Library/Preferences/VMware
Fusion/vmnet8/dhcpd.conf" | grep subnet | awk '{print $2}' | cut -d.
-f1,2,3`
netmask=awk '/subnet/,/\}/' "/Library/Preferences/VMware
Fusion/vmnet8/dhcpd.conf" | grep subnet | awk '{print $4}'
min=`awk '/subnet/,/\}/' "/Library/Preferences/VMware
Fusion/vmnet8/dhcpd.conf" | grep range | awk '{print $2}' | cut -d. -f4`
max=`awk '/subnet/,/\}/' "/Library/Preferences/VMware
Fusion/vmnet8/dhcpd.conf" | grep range | awk '{print $3}' | cut -d. -f4
| cut -d\; -f1`
diff=$((max-min+1));
uniqoctet=$(( min + RANDOM%diff ))

host vmnamehere {
hardware ethernet <MAC>;
fixed-address <IP>;
}

cd /Applications/VMware Fusion.app/Contents/Library
sudo ./vmnet-cli –configure
sudo ./vmnet-cli –stop
sudo ./vmnet-cli –start

Snapshot
vmrun stop ~/Documents/Virtual\ Machines.localized/VMNAME/VMNAME*.vmx
vmrun -T ws snapshot ~/Documents/Virtual\
Machines.localized/VMNAME/VMNAME*.vmx SNAPSHOT

# Shared folders
## enable
vmrun enableSharedFolders ~/Documents/Virtual\
Machines.localized/triage-beta.vmwarevm/triage-beta.vmx
