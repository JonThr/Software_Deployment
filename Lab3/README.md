# Lab 3

## Part 1

This guide demonstrates how to use Docker-Compose to set up and run WordPress and MySQL images. Before starting, make sure you have [Docker-Compose installed](https://docs.docker.com/compose/install/).

<details>
  <summary>Click to expand!</summary>
  
### Define the project

1.  Create an empty project directory.

    This project directory contains a `docker-compose.yml` file.

    >**Tip**: You can use either a `.yml` or `.yaml` extension for
    this file. They both work.

3.  Change into your project directory.

    For example, if you named your directory `Teil1`:

    ```console
    $ cd Teil1
    ```

4.  Create a `docker-compose.yml` file that starts
    `WordPress` and a `MySQL` instance:

```yaml
services:
  db:
    image: mysql:8.0.27
    command: '--default-authentication-plugin=mysql_native_password'
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      - MYSQL_ROOT_PASSWORD=somewordpress
      - MYSQL_DATABASE=wordpress
      - MYSQL_USER=wordpress
      - MYSQL_PASSWORD=wordpress
    expose:
      - 3306
      - 33060
  wordpress:
    image: wordpress:latest
    depends_on:
      - db
    ports:
      - 8000:80
    restart: always
    environment:
      - WORDPRESS_DB_HOST=db:3306
      - WORDPRESS_DB_USER=wordpress
      - WORDPRESS_DB_PASSWORD=wordpress
      - WORDPRESS_DB_NAME=wordpress
volumes:
  db_data:
```

   > **Note**: The docker volume `db_data` persists updates made by WordPress
   to the database.


### Build the project

Now, run `docker compose up -d` from your project directory.


### Bring up WordPress in a web browser

At this point, WordPress should be running on port `8000` of your Docker Host,
and now you can open [http://localhost:8000](http://localhost:8000) in a web
browser.

> **Note**: If you get the error response from daemon: Ports are not available: exposing port TCP 0.0.0.0:80 -> 0.0.0.0:0: listen tcp 0.0.0.0:80: bind: An attempt was made to access a socket in a way forbidden by its access permissions then change the ports in the docker-compose.yml file.

### Shutdown and cleanup

The command `docker compose down` removes the
containers and default network, but preserves your WordPress database.

The command `docker compose down --volumes` removes the containers, default
network, and the WordPress database.

## Usefull Links

* [Quickstart: Compose and WordPress](https://github.com/docker/awesome-compose/tree/master/official-documentation-samples/wordpress)
* [Install Docker Compose](https://www.youtube.com/watch?v=Vxf3qtk1qIA)
* [Wordpress & Docker](https://gist.github.com/bradtraversy/faa8de544c62eef3f31de406982f1d42)
</details>

## Expierence
### Part 1
After using `docker compose up -d` I got an error response from daemon: Ports are not available: exposing port TCP 0.0.0.0:80 -> 0.0.0.0:0: listen tcp 0.0.0.0:80: bind: An attempt was made to access a socket in a way forbidden by its access permissions. The solution was to change the ports in the `docker-compose.yml` file.


