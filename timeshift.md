# Instalando Timeshift nos derivados do Ubuntu
```bash
sudo add-apt-repository -y ppa:teejee2008/timeshift
sudo apt-get update
sudo apt-get install timeshift
sudo apt-get install psmisc cron
```

# Desinstalando Timeshift nos derivados do Ubuntu
```
sudo add-apt-repository ppa:teejee2008/timeshift -r -y
sudo apt remove timeshift --auto-remove
sudo rm -R /timeshift/
```

# Comandos
* timeshift --create --comments "after update" --tags D = cria ponto de restauração
* timeshift --restore = inicia sistema de retauração interativo
* timeshift --restore --snapshot "2019-01-21_19-28-43" --backup-device /dev/sda2 --target-device /dev/sda1 --skip-grub = inicia reatauração a partir de uma unidade externa
* timeshift --delete = inicia processo de deletar cabkup de modo interativo
* timeshift --delete --snapshot "2019-01-21_19-28-43" = deleta um backup especifico
* timeshift --delete-all = remove todos os backups
