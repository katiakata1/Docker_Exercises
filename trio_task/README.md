# Trio-task

This is a Flask application that is set up and configured to work with a database and nginx. Write a docker-compose.yaml that will bring all these services up and allow the app to run on port `80`.

## Spin up three containers (MySQL -> Flask-app -> nginx) using docker
1. Build images for Mysql. The image is called db, and the location is in db file
```
docker build -t db ./db
```
2. Run Mysql container
```
docker run -d -p 3306:3306 --name db db 
```
3. Build image for flask-app
```
docker build -t flask-app ./flask-app
```
4. Run flask-app container 
```
docker run -d -p 5000:5000 --name flask-app flask-app
```
5. Create network that connects all services and connect them
```
docker network create my-network
```
```
docker network connect my-network flask-app
```
```
docker network connect my-network db
```
6. Check if containers are running by entering localhost:5000 in the web browser or using this comman in cli:
```
curl localhost:5000
```

7. Run nginx image:
```
docker run -d --network my-network --mount type=bind,source=$(pwd)/nginx/nginx.conf,target=/etc/nginx/nginx.conf -p 80:80 --name nginx nginx:alpine
```

8. Check if everything is working by going localhost or:
```
curl localhost
```

## To remove all images:
```
docker image prune -a
```
## To stop all containers:
```
docker-compose down -rmi all
```
## Spin up containers using docker-compose:
```
docker-compose up -d
```
