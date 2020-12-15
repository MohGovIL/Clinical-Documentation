#Docker - the Recommended way
We have set of docker images that compose all the repositories to whole project, for development and production version.

## Requirements
* [Docker installed](https://docs.docker.com/install/)
* Mariadb/Mysql
* Couchdb/AWS S3 for documents storage    


Every type of clinic is built from different Docker image.  

## Emnergency center

### release 1.0.0
1. pull the image from [DockerHub](https://hub.docker.com/r/israelimoh/clinikal/tags):
`docker pull israelimoh/clinikal:emergency-1.0.0`
2. Setup the container -
```shell
docker run \
        --name $INSTALLATION_NAME \
        --env DOMAIN_NAME=$DOMAIN_NAME \
        --env MYSQL_HOST=$MYSQL_HOST \
        --env MYSQL_DATABASE=$MYSQL_DATABASE \
        --env MYSQL_USER=$MYSQL_USER \
        --env MYSQL_PASS=$MYSQL_PASS \
        --env MYSQL_ROOT_USER=$MYSQL_ROOT_USER \
        --env MYSQL_ROOT_PASS=$MYSQL_ROOT_PASS \
        --env OE_USER=$OE_USER \
        --env OE_PASS=$OE_PASS \
        --env AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID \
        --env AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY \
        --env CLINIKAL_SETTING_clinikal_storage_method=$STORAGE_METHOD \
        --env CLINIKAL_SETTING_s3_region=$S3_BUCKET_REGION \
        --env CLINIKAL_SETTING_s3_bucket_name=$BUCKET_NAME \
        --env CLINIKAL_SETTING_s3_path=$S3_PATH \
        --mount source=${INSTALLATION_NAME}_sites,target=/var/www/localhost/htdocs/openemr/sites \
        --mount source=${INSTALLATION_NAME}_logs,target=/var/log \
        israelimoh/clinikal:emergency-1.0.0  
```
The following is a table explaining each required variable:

| **Variable**                           | **Description**                                                                                                                                                                                             |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DOMAIN\_NAME                           | Domain name that will be used to access application                                                                                                                                                     |                                                                                                                                             |
| MYSQL\_HOST                            | Address of database server.
| MYSQL\_DATABASE                        | A database name created during installation                                                                                                                                                        |
| MYSQL\_ROOT\_USER<br>MYSQL\_ROOT\_PASS | An existing username and password of user with root privileges                                                                                                                                              |
| MYSQL\_USER<br>MYSQL\_PASS             | In every installation there is a new database user that is created.<br>MYSQL_USER is the user.<br>MYSQL\_PASS is the password for this user. |
| OE\_USER<br>OE\_PASS                   | Username and password of the openemr user created during installation.<br>Use this for the first login into the application.                                                                                |
| CLINIKAL\_SETTING\_clinikal\_storage\_method  | 10 for AWS S3 / 1 for CouchDB                                                                                |
| CLINIKAL\_SETTING\_s3\_region<br>CLINIKAL\_SETTING\_s3\_bucket\_name<br>CLINIKAL\_SETTING\_s3\_path| optional (only for S3 storage), can be edit in the Globals settings screen.                                                                                                                                                                                                     |
| AWS\_ACCESS\_KEY\_ID                   | need to be obtained using an IAM aws user (required for S3)                                                                                                                                                                  |
| AWS\_SECRET\_ACCESS\_KEY               | need to be obtained using an IAM aws user (required for S3)                                                                                                                                                                  |

In the first running, the process will create new database in the MariaDB, each additional run will trigger the upgrade process.
A run command must receive a set of environment variables  for each container. 

**Accessing The Application**  

To access the clinikal client application, use DOMAIN_NAME.

To access the api or the  community’s openemr frontend, use backend.DOMAIN_NAME (e.g. backend.whatever.com).


## Developers tools
Using [clinikal-devops](https://github.com/israeli-moh/clinikal-devops) repository you can setup local environment base on docker for development easily.

1. Clone the repository from github.
2. **Configuration**<br>
There are 2 configuration files relevant to an installation/upgrade:<br>
sample.creds.cfg - contains credentials such as database user name and password<br>
sample.container.cfg - contains configurations for running the container<br>
Rename these files to creds.cfg and container.cfg, respectively.<br>
The following is a table explaining each configuration option in sample.container.cfg:<br>

| **Variable**                                 | **Description**                                                                                                                                                                                                                                                                               |
| -------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| INSTALLATION\_NAME                           | This will be used as the container name, database name, database username.<br>In the development environment it will also be used as the directory name containing the code-base on the host machine.<br>In the test and prod environments it will be used as a prefix of the volumes' names. |
| ENVIRONMENT                                  | leave it as 'dev'    |
| VERTICAL<br>VERTICAL\_VERSION                 | An image tag is made up of : VERTICAL-VERTICAL\_VERSION-ENVIRONMENT<br>These configuration values will determine which image will be used. <br> e.g. for emergency center emergency-1.0.0-dev                                                                                                                                                   |
| MYSQL\_HOST                                  | Address of database server.<br>In development the database is currently local, so this is set to the docker network bridge’s host machine IP.                                                                                                                                                 |
| STORAGE\_METHOD                              | leave it as 10, this means S3 will be used                                                                                                                                                                                                                                                    |
| OPENEMR\_PORT                                | Port on host machine through which openemr in the container can be accessed.<br>(You can choose any port that is currently open).                                                                                                                                                             |
| HOST\_CODEBASE\_PATH                         | In development the code-base is downloaded on the host machine. This is the absolute path on the host machine where the code-base will be downloaded.                                                                                                                                         |
| OPENEMR\_BRANCH                              | Branch of [openemr](https://github.com/openemr/openemr) repository to download                                                                                                                                                                                                                                                      |
| GENERIC\_BRANCH                              | Branch of [clinikal-backend](https://github.com/israeli-moh/clinikal-backend) repository to download                                                                                                                                                                                                                                             |
| VERTICAL\_BRANCH                             | Branch of the chosen vertical repository to download (e.g. [vertical-emergency-medicine-backend](https://github.com/israeli-moh/https://github.com/israeli-moh/vertical-emergency-medicine-backend))                                                                                                                                                                                                                                         |
| CLIENT\_APP\_BRANCH                          | Branch of the [client application](https://github.com/israeli-moh/clinikal-react) repository to download                                                                                                                                                                                                                                       |
| DEVELOPER\_NAME                              | put in your name. This will be part of the path in S3 and distinguish between different devs                                                                                                                                                                                                  |

The following is a table explaining each configuration option in sample.creds.cfg:

| **Variable**                           | **Description**                                                                                                                                                                                             |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| MYSQL\_ROOT\_USER<br>MYSQL\_ROOT\_PASS | An existing username and password of user with root privileges                                                                                                                                              |
| MYSQL\_PASS                            | In every installation there is a new database user that is created.<br>The username of this user is the INSTALLATION\_NAME value from the conatiner.cfg file.<br>MYSQL\_PASS is the password for this user. |
| OE\_USER<br>OE\_PASS                   | Username and password of the openemr user created during installation.<br>Use this for the first login into the application.                                                                                |
| AWS\_ACCESS\_KEY\_ID                   | need to be obtained using an IAM aws user                                                                                                                                                                   |
| AWS\_SECRET\_ACCESS\_KEY               | need to be obtained using an IAM aws user                                                                                                                                                                   |



**Accessing The Application**

In the development environment the clinikal client application is completely outside of the container and communicates with the server-side inside the container.

Go to HOST_CODEBASE_PATH/INSTALLATION_NAME/clinikal-react and run npm start.

To directly access the api or the  community’s openemr frontend, use localhost:OPENEMR_PORT.
