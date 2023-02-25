# Week 1 — App Containerization

#### Table of Contents

+ [Required Homework](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/journal/week1.md#required-homework)
  - Containerize Backend and Frontend
  - Notification Endpoint for the OpenAI Document
  - Flask Backend Endpoint for Notifications
  - React Page for Notifications
  - DynamoDB Local Container
  - Postgres Container
      
* [Homework Challenges](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/journal/week1.md#homework-challenges)
  - Push and tag a image to DockerHub
  - Use multi-stage building for a Dockerfile build
  - Install Docker on localmachine & run containers
  - Pull a Container into EC2 instance with docker installed
  - Implement a healthcheck in the V3 Docker compose file
  - Run the dockerfile CMD as an external script


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
- [Link to commit a7cc30 showing the configurations](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/a7cc30c9d6ba894936bb74693756dba37864258d?diff=split)


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

- Created a `docker-compose.yml` file to allow multiple containers to be build as shown in the [link for commit a7cc30](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/a7cc30c9d6ba894936bb74693756dba37864258d?diff=split)

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
[Link to commit b28f66 showing the changes](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/b28f6692175d3dbbb6bd8f058cee1310ff27b9c4?diff=split)

---

### Notification Endpoint for the OpenAI Document

---

### Flask Backend Endpoint for Notifications

---

### React Page for Notifications

---

### DynamoDB Local Container

---

### Postgres Container

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
