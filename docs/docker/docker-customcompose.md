# Custom Docker-compose

![pic](../img/docker-compose.jpg)

## Portainer Templates

??? bug "Seafile"

    ### Seafile 
    Self-hosted onedrive.

    This can be used together with a Windows 10 application that will make seafile show up in the file explorer like onedrive does.

    ```
    version: '2.0'
    services:
      db:
        image: mariadb
        container_name: seafile-mysql
        environment:
          - MYSQL_ROOT_PASSWORD=*
          - MYSQL_LOG_CONSOLE=true
        volumes:
          - ./data/mariadb:/var/lib/mysql
        networks:
          - seafile-net

      memcached:
        image: memcached
        container_name: seafile-memcached
        entrypoint: memcached -m 256
        networks:
           - seafile-net
          
      seafile:
        image: seafileltd/seafile-mc
        container_name: seafile
        ports:
          - "8080:80"
        volumes:
          - ./data/app:/shared
        environment:
          - DB_HOST=db
          - DB_ROOT_PASSWD=*
          - TIME_ZONE=Etc/UTC
          - SEAFILE_ADMIN_EMAIL=*
          - SEAFILE_ADMIN_PASSWORD=*
          - SEAFILE_SERVER_LETSENCRYPT=false
          - SEAFILE_SERVER_HOSTNAME=*
        depends_on:
          - db
          - memcached
        networks:
          - seafile-net

    networks:
      seafile-net:
    ```

??? bug "Vaultwarden"

    ### Vaultwarden 
    Self-hosted password manager.

    This can use all of bitwardens applications on IOS, Android, Windows, Mac, Chrome, Firefox, etc.
    ```
    version: '3.4'
    services:
      vaultwarden:
        image: vaultwarden/server:latest
        environment:
          - ADMIN_TOKEN=*
          - SIGNUPS_ALLOWED=false
        volumes:
          - ./vw_data:/data
        ports:
          - 17881:80
    ```

??? bug "Flamedashboard"

    ### Flamedashboard
    Self-hosted dashboard

    This can be used for quick access to all of your self-hosted services.
    ```
    version: '2.1'
    services:
      flame:
        image: pawelmalak/flame:latest
        container_name: flame
        volumes:
          - /srv/config/flame:/app/data
        ports:
          - 5005:5005
        environment:
          - PASSWORD=*
        restart: unless-stopped
    ```

??? bug "Vikunja"

    ### Vikunja
    Self-hosted to do list manager

    ```
    version: '3'

    services:
      db:
        image: mariadb:10
        command: --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
        environment:
          MYSQL_ROOT_PASSWORD: supersecret
          MYSQL_USER: vikunja
          MYSQL_PASSWORD: secret
          MYSQL_DATABASE: vikunja
        volumes:
          - ./db:/var/lib/mysql
        restart: unless-stopped
      api:
        image: vikunja/api
        environment:
          VIKUNJA_DATABASE_HOST: db
          VIKUNJA_DATABASE_PASSWORD: secret
          VIKUNJA_DATABASE_TYPE: mysql
          VIKUNJA_DATABASE_USER: vikunja
          VIKUNJA_DATABASE_DATABASE: vikunja
          VIKUNJA_SERVICE_JWTSECRET: <a super secure random secret>
          VIKUNJA_SERVICE_FRONTENDURL: https://<your public frontend url with slash>/
        ports:
          - 3456:3456
        volumes:
          - ./files:/app/vikunja/files
        depends_on:
          - db
        restart: unless-stopped
      frontend:
        image: vikunja/frontend
        ports:
          - 4321:80
        environment:
          VIKUNJA_API_URL: http://vikunja-api-domain.tld/api/v1
        restart: unless-stopped
    ```