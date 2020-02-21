# README

## Get the Passenger + Nginx running for Rails application

1. Install our PGP key and add HTTPS support for APT
```sh
sudo apt-get install -y dirmngr gnupg
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 561F9B9CAC40B2F7
sudo apt-get install -y apt-transport-https ca-certificates
```

2. Add our APT repository
```sh
sudo sh -c 'echo deb https://oss-binaries.phusionpassenger.com/apt/passenger bionic main > /etc/apt/sources.list.d/passenger.list'
sudo apt-get update
```

3. Install Passenger + Nginx module
```sh
sudo apt-get install -y libnginx-mod-http-passenger
```

4. Restart the server (NOTE: stop apache server first with sudo service nginx apache stop) and get all required dependencies 
```sh
sudo service nginx restart
apt-get update && apt-get install passenger nginx-extras nginx
```


5. After installation, please validate the install by running
```sh
sudo /usr/bin/passenger-config validate-install
sudo apt-get update
```

6. Please run passenger-config about ruby-command to find out which Ruby interpreter you are using
```sh
passenger-config about ruby-command
```


7. ADD server{} under http{} through `sudo nano /etc/nginx/nginx.conf`
```sh
server {
	  listen 80;
	  server_name demo-pm.com;
	  passenger_enabled on;
	  passenger_app_env production;
	  root /home/emorphis/Projects/Rails/process_monitoring/public;
	}
```

8. Regularly update/upgrade via `sudo apt-get update`

9. Change `/etc/hosts` as per the DNS domain name