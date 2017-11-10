# deploy-linux-server

## All system packages have been updated to most recent versions.
1. `sudo apt-get update`
2. `sudo apt-get upgrade`
3. `sudo apt autoremove`
4. `sudo reboot`

## Change ssh port from 22 to 2200
1. `sudo nano /etc/ssh/sshd_config`
2. Under the line: "# What ports, IPs and protocols we listen for". Modify `Port 22` to `Port 2200`.
3. Restart ssh `sudo /etc/init.d/ssh restart`

## Setting firewall on ubuntu.
1. `sudo ufw default deny incoming`
2. `sudo ufw default allow outgoing`
3. `sudo ufw allow www`
4. `sudo ufw allow 2200/tcp`
5. `sudo ufw allow 123/tcp`
6. `sudo ufw enable`
7. `sudo reboot`
