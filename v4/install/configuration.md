---
title: Configuration
nav_order: 3
layout: default
parent: Installation
grand_parent: v4
---
# Configuration
Since PoracleJS requires several services we need to configure them to work together. Some sections will not apply to the Docker configuration, and they will be identified as such. We will go over a basic configuration to get PoracleJS running.

## Firewall
The firewall should only require on a select-few environments. The use-case for this would be that PoracleJS is required to be accessible on the internet. This is not required for local installations. If you are opening PoracleJS to the internet ensure you are using a reverse proxy for SSL-encrypted traffic. This has the added benefit of not exposing PoracleJS directly to the web. The other use-case would be if your environments default rule is drop. This is not the case for most installations.

PoracleJS runs on 3030/tcp by default unless a different port is selected. Ensure you open this port if its required.

## Geofence
The geofence file can be found at `./config/geofence.json`. The geofence help define custom areas. While this is not required it can help allow for multiple notification areas to be defined to pinpoint notifications. The easiest way to configure geofences is through the tool [Fence Editor](http://geo.jasparke.net/).
 * For each area click on `Create` in the top-left corner and fill out the name. This name cannot contain hypens (`-`) but can contain spaces. 
 * Fill out the field `Fence Name` and click on `Create` to begin drawing the fence
 * Click where the edges should be for the area. Once you are done with the area, ensure you click the starting location to close the fence
 * Perform these steps for all areas you wish to include. Once you have created your areas click on `Save` and `Click to Download`

This file can be uploaded to the geofence file or the contents can be updated directly to the file.

## Configuration File
Both installation methods should have a file located at `./config/local.json`. This file will need to be modified to ensure all of the services are connected together properly.

### Database
```plain
This step can be skipped for Docker installations
```
The first configuration we need to make is to the Database. This section can be found under the key `database`. Make the following changes to this section:
 * client
    * mysql - For use with MariaDB / MySQL databases
    * pg - For use with PostgreSQL databases
    * sqlite - For use with SQLite databases
 * conn
    * host - Hostname or IP of the database service. If hosting locally you can use 127.0.0.1
    * database - Name of the database during configuration. The example uses the database name `poracle`
    * user - Username of the account for the database connection. The example uses the username `poracleuser`.
    * port - Port of the database service. MariaDB and MySQLs default port is `3306`.

### Notification Service
You only need to configure the section for your notification service. See the correct section for additional information for configuring these services
 * [Discord](../config_file#discord)
 * [Telegram](../config_file#telegram)

### Geocoding
If you wish to utilize maps as part of your notifications you need to configure the section `geocoding`. More information can be found on the [Configuration File](../config_file#geocoding) page.

### Validating the file
After making changes to the file we should ensure it is valid JSON. If it is not valid JSON PoracleJS will not start. You can use [JSONLint](https://jsonlint.com/) to ensure the file is valid JSON. It will attempt to highlight any issues that would cause the file to be invalid JSON.

PoracleJS has now been configured with the required basic information to run. You may want to tinker additional settings but they can all be found on the [Configuration File](../config_file) page.