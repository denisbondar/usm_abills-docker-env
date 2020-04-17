# USM_ABILLS Docker Environment

This environment provides the feature of running the usm_abills module inside the Docker container. This environment does not contain the module itself. You should download it additionally in your account and copy it inside the environment as described below.

## Building

1. Copy usm_abils folder from this folder to userside bundle folder
2. Add service setup from docker-compose.yml to bundle docker-composer.yml
3. Download usm_abils from account https://my.userside.eu and unzip two files (usm_abils.php and usm_abils.conf.php-example) into the usm_abils/module folder.
4. Rename usm_abils.conf.php-example to usm_abils.conf.php and setup it. Do not modify parameter $logPath !
5. Copy usm_abils.cron to host /etc/cron.d folder and modify as needed and change path to bundle (or standalone) docker-compose.yml
6. Restart userside docker bundle for building the docker-image
```
docker-compose stop
docker-compose up --build -d
```

## Test

To test the module, run it manually.
```
docker-compose run --rm usm_abills php usm_abills.php
```

## Any questions?

All questions are accepted only through the ticket system of your account.