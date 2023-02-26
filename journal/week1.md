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

---

### Use multi-stage building for a Dockerfile build

---

### Install Docker on localmachine & run containers

---

### Pull a Container into EC2 instance with docker installed

---

### Implement a healthcheck in the V3 Docker compose file

---

### Run the dockerfile CMD as an external script
