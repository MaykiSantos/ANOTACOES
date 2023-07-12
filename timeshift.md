# Instalando Timeshift nos derivados do Ubuntu
```bash
sudo add-apt-repository -y ppa:teejee2008/timeshift
sudo apt-get update
sudo apt-get install timeshift
apt-get install psmisc cron
```

# Desinstalando Timeshift nos derivados do Ubuntu
```
sudo add-apt-repository ppa:teejee2008/timeshift -r -y
sudo apt remove timeshift --auto-remove
sudo rm -R /timeshift/
```

# Comandos
timeshift --restore #interativo
timeshift --restore --snapshot "2019-01-21_19-28-43" --backup-device /dev/sda2 --target-device /dev/sda1 --skip-grub
timeshift --delete #interativo
timeshift --delete --snapshot "2019-01-21_19-28-43"
timeshift --delete-all #completely remove all snapshots
