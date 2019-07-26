<!-- ## Dockerized JIRA v8.3 and MySQL v5.7 -->

<img alt="Docker Pulls" src="https://img.shields.io/docker/pulls/eduardevops/jira8.3-mysql.svg" style="max-width:100%;"> <img alt="MicroBadger Size" src="https://img.shields.io/microbadger/image-size/eduardevops/jira8.3-mysql/latest.svg" style="max-width:100%;">
-----

![Logo](./assets/logo.jpg)

------

# INFO!!!
####  Still working on this. All necessary comments will be provided at the very end
####  Don't use this

This is a work of  ![This Project](https://github.com/cptactionhank/docker-atlassian-jira)

![Martin Aksel Jensen](https://github.com/cptactionhank) did a great job

------
## First things first
Before you can use this repo make sure you have [Docker](https://www.docker.com/) and [Docker Compose](https://docs.docker.com/compose/install/) installed

## Versions
*	JIRA v8.3.0
*	MySQL v5.7.27

-----
## NGINX
Depending on your server sepcs JIRA configuration (and its work in general) can be very slow, which can cause nginx to stop working with error 504. To avoid this add proxy timeout settings to your nginx.conf or increase value of proxy_read_timeout in your reverse proxy setting

#### nginx.conf

```bash
  proxy_connect_timeout       600;
  proxy_send_timeout          600;
  proxy_read_timeout          600;
  send_timeout                600;
```
-----

------
## Content

### Tree

```bash
.
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

### Description

Name | Description
------------------- | -------------
.env.db             | MySQL Database root password. As well as new Database user and password
.env.jira           | Jira container environments
Dockerfile          | As it says, Dockerfile from which image will be build
docker-compose.yml  | Main file of the project that builds and links containers


------

-----
#### ToDo
All names and parameters can be, and in most cases should be edited.

-----

#### Run
Clone repo to your server (I would suggest use /opt directory)
```bash
sudo git clone https://github.com/eduardevops/dockerized-jira8.3-mysql.git
```

Make sure your user is a member of Docker group
```sh
usermod -aG docker <username>
```
Navigate to the project folder
```sh
cd /path/to/dockerized-jira8.3-mysql
```
Make ```bash docker-entrypoint.sh ``` file executable for others and run the composer
```sh
chmod o+x docker-entrypoint.sh
docker-compose up -d
```

------
Check logs in real-time
```sh
docker-compose logs -f
```


-----
#### Check SSL

##### If you want to make sure that SSL is enabled for MySQL
You can use one of 2 options
1.  Get inside the container
    ```bash
    docker container exec -it jira-db bash
    ```
    Connect to MySQL
    ```bash
    mysql -u root -p
    ```
    Use the password you set earlier on .env.db file

2.  Uncomment 'ports' section in 'docker-compose.yml' file
    Example
    ```yaml
    ...
    ports:
      - 33060:3306
    ...
    ```
Once connected to MySQL console, run
```sql
USE jira_db;
SELECT @@character_set_database, @@collation_database;
```
![Show](./assets/Show.jpg)

Or
```sql
STATUS;
```
![Show](./assets/Status.jpg)

-----
