# Apps (ExpressJS)

## Prerequisite
### Download source code
You can fork on my github [here](https://github.com/IDN-Training/simple-apps)

and you download source code to local (development) and server (deployment)
```
git clone https://github.com/idndevops/simple-apps.git
```
### Download package nodejs
Install nodejs versi 18.x
```
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - && sudo apt-get install -y nodejs
```

## Database Installation
### Install package 
Install mariadb server
```
apt install mariadb-server
```
### Create database, user, and password
Create with mariadb syntax
```
create database training;
grant all privileges on training.* to 'peserta'@'localhost' identified by 'password';
grant all privileges on training.* to 'peserta'@'%' identified by 'password';
flush privileges;
quit;
```
### Import table to database
Import table to database from backup file
```
mysql -u peserta -p training < database/training.sql
mysql -u peserta -p training -e "show tables;"
```

## Running Application
Install dependecies apps
```
npm install
```

Running apps
```
npm start
```

## Access Application
You can access on endpoint url
```
http://ip_server:3000
```
