# LoginWebinar

Standard Edition

## Description

This edition is when the postgres database service is running on a VPS/Bare Metal or other external location

If Postgres is installed as a system service on this server, certain configuration files must be created to handle the connection from postgres.host

For instructions on configuration changes for [POSTGRES](postgres.system.configuration.md)

All other services are then hosted on this one server (mainweb_app, mcpweb_app, heartbeat_srv, apiservice_srv ). 
The apiservice_srv does not require a public domain name.
The mainweb_app, heartbeat_srv must have public domain name with open ports to 80:443
The mcpweb_app is a choice, you must be able to access the service within the company lan/wlan or you can assign it a public domain name. This app can then be used by your administrator from any internet connection.


## Getting Started

### Dependencies

* Debian OS
* Docker
* NextJs
* Go Lang
* OpenSSL

### Installing

* How/where to download your program
* Modifications needed to be made to files/folders

### Downloading the Installation

* Fresh Installation of Ubuntu (24.04) or other Debian based linx server edition
* Use a tunneling service such as Cloudflare Zero-trust tunnel or Tailscale Funnel

```
cd \
sudo mkdir srv
cd srv
sudo git clone https://github.com/LoginWebinar/loginwebinar-standard.git
sudo chown ubuntu:ubuntu -R loginwebinar-standard
```

### GENERATE PUBLIC PRIVATE KEY


```
cd /srv/loginwebinar-standard/keys
openssl genrsa -out private.key 2048
openssl rsa -pubout -in private.key -out public.pem
sudo chmod 644 private.key public.pem
cd /srv/loginwebinar-standard

```

### GENERATE A 32 BTYE KEY

run the following command as copy the key into the .env file under the NEVER_CHANGE_AFTER_INSTALLATION_32_BYTE_KEY.
This key MUST never change once you start the application.

```
openssl rand -base64 32
```

## ENV FILE

after cloning need to copy the .env.example file to .env

```
cd /srv/loginwebinar-standard
cp .env.example .env
```

Now edit the .env file and set the values as needed below:
SITE_URL= https://(full qualified domain name)

HEARTBEAT_WSURL=ws://(full qualified domain name)

POSTGRES_USER   <== Must be your postgres user account>

POSTGRES_PASSWORD <== Must be the posgres user password>

SWAGGER_USERNAME  <== Any username you want to use to access the API documentation>

SWAGGER_PASSWORD  <== Any password you want to use to access the API documenation>

NEVER_CHANGE_AFTER_INSTALLATION_32_BYTE_KEY 

MAIN_COOKIE_PREFIX  <== can be anything you choose, recommend lwmanager used by the admin users>

VIEWER_COOKIE_PREFIX  <== can be anything you choose, recommand lwview  used by the viewers>

PUBLIC_PEM  <== must include the entire PEM including the begining dashes ---PUBLIC PEM--- and ending dashes  >


```
sudo nano .env
```

## SETTING UP THE SELF UPLOAD FOLDER

```
mkdir /srv/loginwebinar-standard/uploads
sudo chown -R 100:101 /srv/loginwebinar-standard/uploads
sudo chmod -R 755 /srv/loginwebinar-standard/uploads
```

## SETTING UP THE NGINX SERVICE

Make a copy of the example default.conf file

```
cd /srv/loginwebinar-standard/nginx
cp default.conf.example default.conf
```

Edit the default.conf file by adding the fully qualified domain name to the server_name option on line 11

```
sudo nano default.conf
```

go to line 11, server_name _;  replace the _ with the fully qualified domain name

Should look like:   server_name podcast.yourdomainname.com;   <== no spaces in the domain name, must end with the semi-colon>



## STARTING THE CONTAINERS

once you issue the following commands, this will start the containers
and allow them to autostart after rebooting the server

```
cd /srv/loginwebinar-standard
docker compose up -d
```



### Updates

* Run this to get any updates after the clone

```
cd /srv/loginwebinar-standard
git pull
```

* Run this to update the application, doing this will cause a down time

```
cd /srv/loginwebinar-standard
docker compose pull
docker compose down
docker compose up -d
```


## Help

Any advise for common problems or issues.

```
command to run if program contains helper info
```

## Authors

Contributors names and contact info

Rob Helmstetter


## Version History

* 0.2
    * Various bug fixes and optimizations
    * See [commit change]() or See [release history]()
* 0.1
    * Initial Release

## License

This project is licensed under the NOT Licensed - see the LICENSE.md file for details

## Acknowledgments



