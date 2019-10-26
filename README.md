## Run JIRA with MySQL inside Docker container

![Logo](./assets/logo.jpg)

#### Status
<img alt="Docker Pulls" src="https://img.shields.io/docker/pulls/eduardevops/jira8-mysql" style="max-width:100%;"> <!-- <img alt="MicroBadger Size" src="https://img.shields.io/microbadger/image-size/eduardevops/jira8-mysql/latest.svg" style="max-width:100%;"> --> <a href="https://www.gnu.org/licenses/gpl-3.0/"> <img alt="Licenses" src="https://img.shields.io/badge/License-GPLv3-blue.svg" style="max-width:100%;"> </a>
<img alt="Build Status" src="https://img.shields.io/docker/cloud/build/eduardevops/jira8-mysql" style="max-width:100%;">

## Table of contents
* [Versions](#Versions)
* [Build With](#Build-With)
* [Project Tree](#Project-Tree)
* [Rename](#Rename)
* [Timeout](#Timeout)
* [How To Use](#How-To-Use)

This is a fork of ![Martin Aksel Jensen's](https://github.com/cptactionhank) project ![docker-atlassian-jira](https://github.com/cptactionhank/docker-atlassian-jira)  <br>
You may use his project if you prefer PostgreSQL.
For JIRA with MariaDB use the following project ![JIRA with MariaDB](https://github.com/eduardevops/dockerized-jira8-mariadb)

####  Versions
*	JIRA v8.5.0
*	MySQL 5.7.27

#### Build With
*	[Docker](https://www.docker.com/)
*	[Docker Compose](https://docs.docker.com/compose/install/)

-----

#### Content Tree
```less
├── .env.db
├── .env.jira
├── Dockerfile
├── assets
│   └── logo.jpg
├── backup
│   ├── db_backup.sh
│   ├── db_restore.sh
│   └── jira_backup.sh
├── conf
│   ├── apache-reverse-proxy.conf
│   ├── httpd.conf
│   └── nginx-reverse-proxy.conf
├── docker-compose-alter.yml
├── docker-compose.yml
└── docker-entrypoint.sh
```

#### Rename
All names can be, and, in most cases, should be changed.

#### Timeout
JIRA is a resource consuming system, regardless you use it inside docker or installed directly in the server.
In .env.jira file you can set MIN and MAX memory usage thresholds, however I would recommend to have at least 4GB memory.
Otherwise it may crash occasionally.
But even with above mentioned parameters you may face error 504 (time out) message, if you choose using Nginx as a reverse proxy.
To avoid it make sure to increase timeout settings in your webserver (Nginx or Apache).
-----

#### HowTo
Clone repo to your server (I would suggest use /opt directory)
```less
sudo git clone https://github.com/eduardevops/dockerized-jira8-mysql.git
```
Navigate to the project folder

```less
cd /path/to/dockerized-jira8-mysql
```
Make docker-entrypoint.sh file executable for other and run the composer

```less
chmod o+x docker-entrypoint.sh
docker-compose up -d
```

Check logs in real-time
```less
docker-compose logs -f
```
