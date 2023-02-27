# Week 1 — App Containerization

#### Table of Contents

+ [Required Homework](#required-homework)
  - [Containerize Backend and Frontend](#containerize-backend-and-frontend)
  - [Notification Endpoint for the OpenAI Document](#notification-endpoint-for-the-openai-document)
  - [Flask Backend Endpoint for Notifications](#flask-backend-endpoint-for-notifications)
  - [React Page for Notifications](#react-page-for-notifications)
  - [DynamoDB Local Container](#dynamodb-local-container)
  - [Postgres Container](#postgres-container)
      
* [Homework Challenges](#homework-challenges)
  - [Push and tag a image to DockerHub](#push-and-tag-a-image-to-dockerhub)
  - [Use multi-stage building for a Dockerfile build](#use-multi-stage-building-for-a-dockerfile-build)
  - [Install Docker on localmachine & run containers](#install-docker-on-localmachine--run-containers)
  - [Pull a Container into EC2 instance with docker installed](#pull-a-container-into-ec2-instance-with-docker-installed)
  - [Implement a healthcheck in the V3 Docker compose file](#implement-a-healthcheck-in-the-v3-docker-compose-file)
  - [Docker Best Practices](#docker-best-practices)


## Required Homework

### Containerize Backend and Frontend

#### Checked that the python works independent of Docker

```sh
cd backend-flask
export FRONTEND_URL="*"
export BACKEND_URL="*"
python3 -m flask run --host=0.0.0.0 --port=4567
cd ..
```
- Ports were successfully opened
- Port 4567 was opened via the Ports section in Gitpod

![image](https://user-images.githubusercontent.com/37842433/221377301-dfd32abb-815f-48ba-9e83-883954d28ed4.png)

- Got back json format result in the browser

![image](https://user-images.githubusercontent.com/37842433/221377331-5ecb2ba1-6ef9-47e9-b1b6-fe9302f152f3.png)



#### Docker Configuration

- Successfully created and added `Dockerfile` for each backend and frontent app as well as a `docker-compose.yml` file
- [Link to commit a7cc30c showing the configurations](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/a7cc30c9d6ba894936bb74693756dba37864258d?diff=split)


#### Running a Container

Run 
```sh
docker run --rm -p 4567:4567 -it -e FRONTEND_URL='*' -e BACKEND_URL='*' backend-flask
```

Run 
```sh
docker run -p 3000:3000 -d frontend-react-js
```

#### Multiple containers & images

- Created a `docker-compose.yml` file to allow multiple containers to be build as shown in the [link for commit a7cc30c](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/a7cc30c9d6ba894936bb74693756dba37864258d?diff=split)

- Docker Containers
```
docker ps
CONTAINER ID   IMAGE                                         COMMAND                  CREATED          STATUS                             PORTS                                       NAMES
d1736720e092   aws-bootcamp-cruddur-2023-frontend-react-js   "docker-entrypoint.s…"   29 seconds ago   Up 28 seconds (health: starting)   0.0.0.0:3000->3000/tcp, :::3000->3000/tcp   aws-bootcamp-cruddur-2023-frontend-react-js-1
5a645db7ce82   aws-bootcamp-cruddur-2023-backend-flask       "python3 -m flask ru…"   29 seconds ago   Up 28 seconds (health: starting)   0.0.0.0:4567->4567/tcp, :::4567->4567/tcp   aws-bootcamp-cruddur-2023-backend-flask-1
```

- Docker Images
```
docker images
REPOSITORY                                    TAG         IMAGE ID       CREATED          SIZE
aws-bootcamp-cruddur-2023-frontend-react-js   latest      75905433bece   9 seconds ago    1.24GB
aws-bootcamp-cruddur-2023-backend-flask       latest      0e9738e35f1c   33 minutes ago   266MB
```

#### Added `npm i` to gitpod.yml to avoid running it manually
[Link to commit b28f669 showing the changes](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/b28f6692175d3dbbb6bd8f058cee1310ff27b9c4?diff=split)

---

### Notification Endpoint for the OpenAI Document
[Link to commit b28f669 showing the changes](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/b28f6692175d3dbbb6bd8f058cee1310ff27b9c4?diff=split2)


[Link to commit 4d7c801 showing further changes](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/4d7c8016b869331f7243b1642a59f577e8177551?diff=split)

---

### Flask Backend Endpoint for Notifications
[Link to commit e0dca78 showing the changes made](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/e0dca78d60a2b78f538c7a1958251c8e51de7369?diff=split)

---

### React Page for Notifications

The backend page showing the result of browsing to `/api/activities/notifications` is shown below in a json formatted page

![image](https://user-images.githubusercontent.com/37842433/221383978-6a9ebd78-f41b-4187-abaa-97baac55f4bd.png)

---

### DynamoDB Local Container

[Link to commit ab7fcb8 showing the changes made](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/ab7fcb89084a508aaac3cb375d0f50e02a89ee61?diff=split)

- Ran the `docker-compose.yml` file to spin up the `dynamoDB` container which was on `port 8000`. Result of which is seen below

```sh
CONTAINER ID   IMAGE                                         COMMAND                  CREATED          STATUS                             PORTS                                       NAMES
3296488b5658   amazon/dynamodb-local:latest                  "java -jar DynamoDBL…"   29 seconds ago   Up 29 seconds                      0.0.0.0:8000->8000/tcp, :::8000->8000/tcp   dynamodb-local
```


- Created a table locally, added items to the table

![image](https://user-images.githubusercontent.com/37842433/221384321-c584041b-bd5b-4691-9293-fc26eeb03d76.png)



---

### Postgres Container

[Link to commit ab7fcb8 showing the changes made](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/ab7fcb89084a508aaac3cb375d0f50e02a89ee61?diff=split)

- Ran the `docker-compose.yml` file to spin up the `postgres` container which was on `port 5432` as seen below

```sh
CONTAINER ID   IMAGE                                         COMMAND                  CREATED          STATUS                             PORTS                                       NAMES
3048dcde231f   postgres:13-alpine                            "docker-entrypoint.s…"   29 seconds ago   Up 29 seconds                      0.0.0.0:5432->5432/tcp, :::5432->5432/tcp   aws-bootcamp-cruddur-2023-db-1
```


![image](https://user-images.githubusercontent.com/37842433/221384504-4f5c6bfe-51a6-4122-8ab8-eb198596a2f8.png)


- Installed Visual Studio Code extension `PostgreSQL` which is a PostgreSQL Management Tool, I was able to setup the postgres connection as seen below

![image](https://user-images.githubusercontent.com/37842433/221384580-c89ae658-a2c7-4a6f-912d-740e92b9b41c.png)

- Using the terminal, I was further able tp login to the postgress database
`psql -Upostgress -h localhost`

![image](https://user-images.githubusercontent.com/37842433/221384645-01277b27-a0e9-4751-8a5e-8da2c7ec9ff8.png)


***



## Homework Challenges

### Push and tag a image to DockerHub

Pushing and tagging of images to DockerHub can be done via several ways, a couple of which are:

- Visual Studio Code Docker Registries

![image](https://user-images.githubusercontent.com/37842433/221577567-cdaac89e-cebd-4c09-95ae-a9f2de2d3c53.png)

![image](https://user-images.githubusercontent.com/37842433/221577013-332c4073-4bdd-4cd7-a4f9-c7b3f1f0478b.png)

- Command Line using the command below

![image](https://user-images.githubusercontent.com/37842433/221577963-ed8bebf5-6258-45d3-88d7-b690b41ad947.png)


#### 1. Log in to DockerHub
```sh
docker login
```

#### 2. Tag image
```sh
docker tag frontend morpheus04/aws-bootcamp-cruddur-2023-main-frontend-react-js:latest
```
OR

![image](https://user-images.githubusercontent.com/37842433/221579077-dc0ceee1-4f4f-4220-a94e-9708c1db9f07.png)


#### 3. Push the image to DockerHub
```sh
docker push morpheus04/aws-bootcamp-cruddur-2023-main-frontend-react-js:latest
```
OR

![image](https://user-images.githubusercontent.com/37842433/221579375-2109db97-2a9b-4f4b-a3d7-ab214e2fdc50.png)


##### Log

![image](https://user-images.githubusercontent.com/37842433/221579599-e93a0aff-f657-4ceb-9966-adec97169007.png)


#### 4. Verify in DockerHub of image push

![image](https://user-images.githubusercontent.com/37842433/221579833-6048f641-44ec-44c9-94fd-66dab3d078f5.png)

OR

![image](https://user-images.githubusercontent.com/37842433/221580570-f9edbd8c-bda2-441f-9ee1-b9bb4c3344a7.png)


#### 5. Deleting the Docker Hub credentials from the ~/.docker/config.json
```sh
docker logout
```
---

### Use multi-stage building for a Dockerfile build

Docker multi-stage build is about building images by keeping the image size down. Here I used the backend Dockerfile as an example

#### Pre Application Build

Here the main build is `130MB`

```sh
$ docker images awsbootcamp2023-backend-main:latest
REPOSITORY                     TAG       IMAGE ID       CREATED          SIZE 
awsbootcamp2023-backend-main   latest    58748b8f9184   20 seconds ago   130MB 
```

#### Build Application

Here we are adding an `AS builder` to the `FROM python:3.10-slim-buster` instruction

```sh
# Build the application
FROM python:3.10-slim-buster AS builder
WORKDIR /backend-flask
COPY requirements.txt requirements.txt
RUN pip3 install --user --no-cache-dir -r requirements.txt
COPY . .
```

#### Run Application

```sh
# Run the application
FROM python:3.10-slim-buster
WORKDIR /backend-flask
COPY --from=builder ..

ENV FLASK_ENV=development

EXPOSE ${PORT}

CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]
```

#### Post Application Build

Here we will verify the original size that reduced with a slightly slimmed down size of `129MB` after post build

```sh
$ docker images awsbootcamp2023-backend-main:latest
REPOSITORY                     TAG       IMAGE ID       CREATED          SIZE 
awsbootcamp2023-backend-main   latest    3558c60414de   12 seconds ago   129MB 
```

---

### Install Docker on localmachine & run containers

#### Installed Docker Desktop on Windows

- Installed Docker Desktop on a Windows OS machine

![image](https://user-images.githubusercontent.com/37842433/221589881-0a7122c8-63ef-49b6-86fd-c058b86e63a8.png)


- Cloned the repo

- Made Changes to `docker-compose.yml` locally, These changes are identfied with the arrows

```sh
version: "3.8"
services:
  backend-flask:
    environment:
      FRONTEND_URL: "http://localhost:3000" <-----
      BACKEND_URL: "http://localhost:4567"  <-----
    build: ./backend-flask
    ports:
      - "4567:4567"
    healthcheck:
      test: wget --no-verbose --tries=1 --spider http://localhost:4567/api/activities/home  <-----
      interval: 60s
      retries: 5
      start_period: 20s
      timeout: 10s
    volumes:
      - ./backend-flask:/backend-flask
   frontend-react-js:
    environment:
      REACT_APP_BACKEND_URL: "http://localhost:4567"  <-----
    build: ./frontend-react-js 
```


- Verify Containers are running in Docker Desktop

![image](https://user-images.githubusercontent.com/37842433/221595125-a1171d9a-e31e-434e-bd02-8161172aeedc.png)


- Verify Backend running on localhost:4567

![image](https://user-images.githubusercontent.com/37842433/221595824-973f9e5f-12ef-4a76-920e-b35ed40662db.png)


- Verify Frontend running on localhost:3000

![image](https://user-images.githubusercontent.com/37842433/221595988-8dbcdc69-3fdd-47af-8b8f-23cd8691ec2e.png)

---


### Pull a Container into EC2 instance with docker installed

#### Provisioned EC2 Amazon Linux 2 instance

- AMI Images used `amazon/amzn2-ami-kernel-5.10-hvm-2.0.20230207.0-x86_64-gp2`
- Instance details seen below

![image](https://user-images.githubusercontent.com/37842433/221599961-faca7544-c626-4d30-ac52-3fc90ae883d6.png)


#### Created Security Group

- Created a Security Group (SG) and attached to EC instance
- SG was then modified by adding inbound rules for incoming traffic based on the ports as seen below

![image](https://user-images.githubusercontent.com/37842433/221598205-aa1e362c-1498-4e4c-a3b3-bb82cb56471b.png)



#### Docker Install

- As part of provisioning of the EC Instance, I added the following to the Userdata section
```sh
sudo yum update -y
sudo yum install docker-y
sudo usermod -a -G docker ec2-user
id ec2-user
newgrp docker
sudo systemctl enable docker.service
sudo systemctl start docker.service
```

- Logged into EC Linux instance via SSH remote tool
- Installed docker-compose
```sh
sudo yum install python3-pip
sudo pip3 install docker-compose
```
- Verified docker was up and running
`sudo systemctl status docker.service`


#### Cloning the Docker Cruddur application

- Login into Docker
```
docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: *REDACTED*
Password: *REDACTED*
WARNING! Your password will be stored unencrypted in /home/gitpod/.docker/config.json.
```
**WARNING! Your password will be stored unencrypted in /home/ec2-user/.docker/config.json.** this looks like a potential problem. Remember to do `docker logout` in the end to remove the credentials from the `config.json`. Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store


#### Pull DockerHub container
`docker pull morpheus04/aws-bootcamp-cruddur-2023-main-backend-flask`

##### Log
```sh
Using default tag: latest
latest: Pulling from morpheus04/aws-bootcamp-cruddur-2023-main-backend-flask
29cd48154c03: Pull complete
2c59e55cfd71: Pull complete
3b4b58298de0: Pull complete
6239e464c1ab: Pull complete
047dd5665bb1: Pull complete
73099005ce62: Pull complete
b9daf3e099ed: Pull complete
9dfca1ca04ce: Pull complete
8fc247f86e63: Pull complete
Digest: sha256:eb8ef47f24e7aaed809e3c1d05c0bf88b6da44e50d9cf487ecd5607544ad54bb
Status: Downloaded newer image for morpheus04/aws-bootcamp-cruddur-2023-main-backend-flask:latest
docker.io/morpheus04/aws-bootcamp-cruddur-2023-main-backend-flask:latest
```


#### Run Pulled Backend container
```sh
[ec2-user@ip-172-31-48-128 ~]$sudo docker run -d -p 4567:4567 morpheus04/aws-bootcamp-cruddur-2023-main-backend-flask
2dae366a28e8552e186a946a927830a7557a7027b98a258bdd2c78cd35c734c3
```

#### Verify Container is running
```sh
[ec2-user@ip-172-31-48-128 ~]$ sudo netstat -tulpn | grep LISTEN
tcp        0      0 127.0.0.1:40817         0.0.0.0:*               LISTEN      2956/containerd
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      3154/sshd
tcp        0      0 0.0.0.0:4567            0.0.0.0:*               LISTEN      7759/docker-proxy
tcp        0      0 0.0.0.0:3000            0.0.0.0:*               LISTEN      7929/docker-proxy
tcp6       0      0 :::80                   :::*                    LISTEN      2952/httpd
tcp6       0      0 :::22                   :::*                    LISTEN      3154/sshd
tcp6       0      0 :::4567                 :::*                    LISTEN      7764/docker-proxy
tcp6       0      0 :::3000                 :::*                    LISTEN      7934/docker-proxy
```

![image](https://user-images.githubusercontent.com/37842433/221623434-7042686b-d2e2-4f5d-982c-7e9f7ae56d90.png)


#### Logout of DockerHub
`docker logout`

---

### Implement a healthcheck in the V3 Docker compose file

- Added healthchecks to docker-compose.yml

[link to commit 3d051d3](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/3d051d3ca3f545d9b2a84a2acf33fd38a39b9e73?diff=split)

```sh
version: "3.8"
services:
  backend-flask:
    environment:
      FRONTEND_URL: "https://3000-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
      FRONTEND_URL: "https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
    build: ./backend-flask
    ports:
      - "4567:4567"
    healthcheck:
      test: curl --fail https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}/api/activities/home
      interval: 60s
      retries: 5
      start_period: 20s
      timeout: 10s
    volumes:
      - ./backend-flask:/backend-flask
  frontend-react-js:
    environment:
      REACT_APP_BACKEND_URL: "http://localhost:4567"
    build: ./frontend-react-js
    ports:
      - "3000:3000"
    healthcheck:
      test: wget --no-verbose --tries=1 --spider https://3000-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST} || exit 1
      interval: 60s
      retries: 5
      start_period: 20s
      timeout: 10s
    volumes:
      - ./frontend-react-js:/frontend-react-js
```

:bulb: **Tip:** I had to add curl * wget in the Dockerfiles for the healthcheck so they are installed into the container before it starts up.
```dockerfile
RUN apt-get update -y
RUN apt-get install -y gcc
RUN apt-get install -y wget
RUN apt-get install -y curl
```


#### Verify Healthchecks

##### Healthy Containers
```sh
ee7fd2051447   aws-bootcamp-cruddur-2023-frontend-react-js   "docker-entrypoint.s…"   6 minutes ago   Up 31 seconds (healthy)   0.0.0.0:3000->3000/tcp, :::3000->3000/tcp   aws-bootcamp-cruddur-2023-frontend-react-js-1
f9216c6b5c01   postgres:13-alpine                            "docker-entrypoint.s…"   6 minutes ago   Up About a minute               0.0.0.0:5432->5432/tcp, :::5432->5432/tcp   aws-bootcamp-cruddur-2023-db-1
579870d8275e   amazon/dynamodb-local:latest                  "java -jar DynamoDBL…"   6 minutes ago   Up About a minute               0.0.0.0:8000->8000/tcp, :::8000->8000/tcp   dynamodb-local
fa66627a696c   aws-bootcamp-cruddur-2023-backend-flask       "python3 -m flask ru…"   6 minutes ago   Up 31 seconds (healthy)   0.0.0.0:4567->4567/tcp, :::4567->4567/tcp   aws-bootcamp-cruddur-2023-backend-flask-1
```


##### Unhealthy Containers
```sh
ee7fd2051447   aws-bootcamp-cruddur-2023-frontend-react-js   "docker-entrypoint.s…"   6 minutes ago   Up About a minute (unhealthy)   0.0.0.0:3000->3000/tcp, :::3000->3000/tcp   aws-bootcamp-cruddur-2023-frontend-react-js-1
fa66627a696c   aws-bootcamp-cruddur-2023-backend-flask       "python3 -m flask ru…"   6 minutes ago   Up About a minute (unhealthy)   0.0.0.0:4567->4567/tcp, :::4567->4567/tcp   aws-bootcamp-cruddur-2023-backend-flask-1
```

![image](https://user-images.githubusercontent.com/37842433/221629105-d1353fd6-355a-4831-ad3f-68eaece2a4de.png)

---

### Docker Best Practices

- Use multi-stage builds

The use of `AS builder` added to the `FROM python:3.10-slim-buster`
```sh
# Build the application
FROM python:3.10-slim-buster AS builder
WORKDIR /backend-flask
COPY requirements.txt requirements.txt
RUN pip3 install --user --no-cache-dir -r requirements.txt
COPY . .
```

- Run Statements

The use of `RUN` command to `apt-get` to e.g. install necessary packages in `Dockerfiles` in my example for the healthchecks

```
# Install curl to allow health check to work
RUN apt-get update -y
RUN apt-get install -y gcc
RUN apt-get install -y wget
RUN apt-get install -y curl
```

