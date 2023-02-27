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
  - [Run the dockerfile CMD as an external script]()


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

![image](https://user-images.githubusercontent.com/37842433/221599149-71c8df91-71ee-4bca-9a07-0ed5b9195317.png)


#### Created Security Group

- Created a Security Group (SG) and attached to EC instance
- SG was then modified by adding inbound rules as seen below

![image](https://user-images.githubusercontent.com/37842433/221598205-aa1e362c-1498-4e4c-a3b3-bb82cb56471b.png)


---

### Implement a healthcheck in the V3 Docker compose file

---

### Run the dockerfile CMD as an external script
