# Duo Task

This is a basic Flask application that serves a simple static website that returns the machine's hostname.

It is directly accessible on port `5000`.

Set the environment variable `YOUR_NAME` to your name to have the app display your name in its welcome message. Otherwise, it will refer to you as "friend".

The `nginx.conf` file can be used to configure an NGINX container to run as a reverse proxy to the Flask app container, effectively making the Flask application accessible on port `80`. You will need to know how to configure networks in Docker in order to achieve this.

## Use docker run to spin up two containers
</br>
 1. Create network 

```
docker network create my-network
```
2. Build image from Dockerfile

```
docker build -t flask-app .
```
3. Run the container + attach network to it

```
sudo docker run -d --network my-network --name flask-app flask-app
```
4. Run Nginx 

```
sudo docker run -d --network my-network --mount type=bind,source=$(pwd)/nginx.conf,target=/etc/nginx/nginx.conf -p 80:80 --name nginx nginx:alpine
```

5. Go to localhost:<port> or use:
```
curl localhost:80
```
