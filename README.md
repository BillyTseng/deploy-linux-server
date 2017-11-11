# deploy-linux-server

1. The IP address and SSH port.
  * `18.216.188.87:2200`
2. The complete URL to the hosted web application.
  * http://ec2-18-216-188-87.us-east-2.compute.amazonaws.com/
3. A list of third-party resources.
  * https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
  * http://flask.pocoo.org/docs/0.12/deploying/mod_wsgi/

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

## Give grader access.
1. `sudo adduser grader`
2. `sudo nano /etc/sudoers.d/grader`,
Add `grader ALL=(ALL) NOPASSWD:ALL` in `/etc/sudoers.d/grader`
3. Create a public key on localhost.
4. Type following command as root to allow grader login into instance.
  * `cd /home/grader`
  * `sudo mkdir .ssh`
  * `sudo nano .ssh/authorized_keys`
5. copy public key and paste to `.ssh/authorized_keys`
6. Login as grader and change the owner of public key to grader.
  * `sudo chown grader:grader .ssh`
  * `sudo chown grader:grader .ssh/authorized_keys`
  * `chmod 644 .ssh/authorized_keys`
  * `chmod 700 .ssh`

## Configure the local timezone to UTC.
* `sudo timedatectl set-timezone Etc/UTC`

## Install and configure Apache to serve a Python mod_wsgi application.
* `sudo apt-get install apache2`
* `sudo apt-get install libapache2-mod-wsgi`

## Install python packges
* `sudo apt-get -qqy install python python-pip`
* `pip install --upgrade pip`
* `sudo pip install flask packaging oauth2client redis passlib flask-httpauth`
* `sudo pip install sqlalchemy flask-sqlalchemy psycopg2 bleach requests`

## Set up catalog web application.
1. Follow [tutorial](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps) to set up flaskapp.
2. Clone catalog app to `/var/www/FlaskApp/FlaskApp`
3. `sudo a2dissite 000-default.conf`
4. `sudo service apache2 restart`
