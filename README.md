# LoginWebinar

Standard Edition

## Description

This edition is when the postgres database service is running on a VPS/Bare Metal or other external location

If Postgres is installed as a system service on this server, certain configuration files must be created to handle the connection from postgres.host

For instructions on configuration changes for [POSTGRES](postgres.system.configuration.md)


## Getting Started

### Dependencies

* Debian OS
* Docker
* NextJs
* Go Lang
* OpenSSL

### Installing

* How/where to download your program
* Any modifications needed to be made to files/folders

### Downloading the Installation

* How to run the program
* Step-by-step bullets

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

Now edit the .env file and set the values as needed

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
Should look like:   server_name podcast.yourdomainname.com;   <== no spaces in the domain name>



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



