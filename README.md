# USM_ABILLS Docker Environment

This environment provides the feature of running the usm_abills module inside the Docker container. This environment **does not contain** the module itself. You should download it additionally in your account and copy it inside the environment as described below.

1. Download last version of docker-environment to your server from https://github.com/userside/usm_abills-docker-env/releases
2. Unzip downloaded archive to folder `usm_abills-docker-env` and copy `usm_abills` folder from unzipped folder into **userside bundle** folder. You should get approximately the following bundle file structure:
  ```
  /docker
   └── userside
        ├── config
        ├── data
        ├── usm_abills
        │    ├── log
        │    ├── module
        │    └── Dockerfile
        ├── docker-compose.yml
        ├── init.sh
        ├── Makefile
        └── README.md
  ```
3. From `usm_abills-docker-env/docker-composer.yml` copy the whole service config `usm_abills:...` to service block into your docker-compose.yml. **Pay attention to the formatting!** The indents in the yaml file are very important.
  ```
  services:
    postgres:
      ...
    
    fpm:
      ...
    
    ...(other services)...

    usm_abills:
      build:
        context: ${USERSIDE_BASE_DIR}/usm_abills
      volumes:
        - ${USERSIDE_BASE_DIR}/usm_abills/module:/app
        - ${USERSIDE_BASE_DIR}/usm_abills/log:/var/log/usm_abills
        - ${USERSIDE_BASE_DIR}/config/datetime.ini:/usr/local/etc/php/conf.d/timezone.ini
        - /etc/localtime:/etc/localtime:ro
        - /etc/timezone:/etc/timezone:ro
      networks:
        - internal

  volumes:
    ...
  ```
4. Download **usm_abills** module from https://my.userside.eu/ and extract the module files to the subdirectory `usm_abills/module` folder. It should turn out as follows:
  ```
  /docker
   └── userside
        ├── config
        ├── data
        ├── usm_abills
        │    ├── log
        │    ├── module
        │    │    ├── usm_abills.conf.php-example
        │    │    └── usm_abills.php
        │    ├── cpanfile
        │    └── Dockerfile
  ```
5. Rename `usm_abills.conf.php-example` to `usm_abills.conf.php` and setup.
6. **Do not change** parameters `$logPath` and `$isSilence`!
7. Go to folder `/docker/userside` then build docker-image for service usm_abills
  ```
  sudo docker-compose build usm_abills
  ```
8. Make a test run:
  ```
  sudo docker-compose run --rm usm_abills
  ```

9. Add a line to your /etc/cron.d/userside similar to the others. For example:
  ```
  */10 * * * *    root    /usr/local/bin/docker-compose .... run --rm usm_abills > /dev/null
  ```

### Any questions?

All questions are accepted only through the ticket system of your account.