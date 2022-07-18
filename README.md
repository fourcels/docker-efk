# Docker compose file for setting up a EFK service

A basic docker compose file that will set up Elasticsearch, Filebeat, and Kibana.

Collection `linux` docker container logs

1. change `ELASTIC_PASSWORD` in `.env`
    ```bash
    # Password for the 'elastic' user (at least 6 characters)
    ELASTIC_PASSWORD=changeme
    ```

1. start services
    ```bash
    $ docker compose up -d
    ```

1. generate `kibana_system` password
    ```bash
    $ docker compose exec elasticsearch /bin/bash

    elasticsearch@:~$ ./bin/elasticsearch-reset-password -u kibana_system
    ```

1. change `KIBANA_PASSWORD` in `.env` with generate `kibana_system` password
    ```bash
    # Password for the 'kibana_system' user (at least 6 characters)
    KIBANA_PASSWORD=changeme
    ```

1. restart `kibana` service
    ```bash
    $ docker compose restart kibana
    ```

1. open url `http://localhost:5601`

    `username`: `elastic`

    `password`: `ELASTIC_PASSWORD`