### Cacti® - The Complete RRDTool-based Graphing Solution (CentOS7 + Supervisor)
- [Docker Image](https://hub.docker.com/r/thedollarsign/cacti/) Version 0.8.8f  using CentOS7 and Supervisor.
- Image is using external database.
- Default Timezone : Asia/Bangkok


### Database deployment
- [million12/mariadb](https://hub.docker.com/r/million12/mariadb/) image as our database.
- Information about million12/MariaDB see our [documentation.](https://github.com/million12/docker-mariadb)

Example:

    docker run \
    -d \
    --name cacti-db \
    -p 3306:3306 \
    --env="MARIADB_USER=cacti" \
    --env="MARIADB_PASS=passwd" \
    million12/mariadb

***Remember to use the same credentials when deploying cacti image.***


### Environmental Variable
In this Image you can use environmental variables to connect into external MySQL/MariaDB database.

`DB_USER` = database user
`DB_PASS` = database password
`DB_ADDRESS` = database address (ip or domain-name)


### Cacti Deployment
Now when we have our database running we can deploy cacti image with appropriate environmental variables set.

Example:

    docker run \
    -d \
    --name cacti \
    -p 80:80 \
    --env="DB_ADDRESS=127.0.0.1" \
    --env="DB_USER=cacti" \
    --env="DB_PASS=passwd" \
    thedollarsign/cacti


### Docker compose
Using docker compose

Example:

	cacti-db:
		image: million12/mariadb
		container_name: dacti-db
		net: host
		restart: always
		privileged: true
		environment:
			- TZ=Asia/Bangkok
			- MARIADB_USER=cacti
			- MARIADB_PASS=passwd
	cacti:
		image: thedollarsign/cacti
		container_name: cacti
		net: host
		restart: always
		privileged: true
		environment:
			- TZ=Asia/Bangkok
			- DB_ADDRESS=127.0.0.1
			- DB_USER=cacti
			- DB_PASS=passwd


### Access Cacti web interface
- fist login use username nad password `admin:admin`
- [dockerhost.ip/cacti]()

---
