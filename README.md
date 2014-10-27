# devdb

A docker image for creating mysql databases for local dev.

## Usage

Start a new instance... 

```bash
$ docker run --name mydevdb -e MYSQL_ROOT_PASSWORD=new_password -e \
    MYSQL_DATABASE=new_db_name -d strathcom/devdb
```

Import data from production into the instance you just started...

```bash
$ docker run --link mydevdb:mysql strathcom/devdb import -u prod_user -p prod_pass \
    -h prod_host -d prod_db
```

Connect to the instance and check your data...

```bash
$ docker run -it --link mydevdb:mysql strathcom/devdb connect

mysql> show tables;
+-----------------------+
| Tables_in_new_db_name |
+-----------------------+
| ...                   |

```

Commit the container to create an image...

```bash
$ docker commit mydevdb strathcom/mydevdb
```

Then push it to docker hub so you can share it with the team...

```bash
$ docker push strathcom/mydevdb
```

## Warning

This image extends the official mysql docker image so that the data is stored
in the image rather than a volume. YOUR DATA WILL BE ERASED when the container 
is removed. 
