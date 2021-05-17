# serverless-dhf-sample

## Details

### MarkLogic

1. Create `docker-compose.yml` in ml directory
    ```
    version: '3.6'
    services:
    generic-ml:
        image: store/marklogicdb/marklogic-server:10.0-6.1-dev-centos
        container_name: generic-ml
        domainname: .
        environment:
        - MARKLOGIC_INIT=true
        - MARKLOGIC_ADMIN_USERNAME=admin
        - MARKLOGIC_ADMIN_PASSWORD=ADMINPASSWORDHERE
        - TZ=America/Chicago
        ports:
        - 5423:5432
        - 7997-8013:7997-8013
        networks:
        - external_net
        - internal_net
        volumes:
        - 'marklogic:/var/opt/MarkLogic'
        - './data:/mnt/data'
    volumes:
    marklogic:
    networks:
    external_net: {}
    internal_net:
        internal: true
    ```
2. `gradle wrapper --gradle-version 6.4`
3. Create `build.gradle` in ml directory
    ```
    plugins {
        id 'net.saliman.properties' version '1.4.6'
        id 'com.marklogic.ml-data-hub' version '5.4.2'
    }
    ```
4. `./gradlew hubInit`
5. Create `gradle-local.properties` (see `gradle-local.properties.sample`)
6. `./gradlew mlDeploy`
7. Download Hub Central CE, login with flow-developer
8. 