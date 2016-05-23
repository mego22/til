## Set Locale
```
sudo sed "s/# en_US.UTF-8/en_US.UTF-8/g; s/en_GB.UTF-8/# en_GB.UTF-8/g" /etc/locale.gen
sudo locale-gen
```

## Add Repo
```
sudo apt-get update
sudo apt-get install git apt-transport-https -y --force-yes
wget -O - https://dev2day.de/pms/dev2day-pms.gpg.key | sudo apt-key add -
echo "deb https://dev2day.de/pms/ jessie main" | sudo tee /etc/apt/sources.list.d/pms.list
sudo apt-get update
```

## Install Plex
```
sudo apt-get install plexmediaserver -y
```

## Start Plex
```
sudo service plexmediaserver start
```

## Install Channels
```
for CHANNEL in NBC ABC CBS FOX TheCW PBS Vimcasts
  git clone https://github.com/plexinc-plugins/${CHANNEL}.bundle.git /var/lib/plexmediaserver/Library/Application\ Support/Plex\ Media\Server/Plug-ins/${CHANNEL}.bundle
done
```
