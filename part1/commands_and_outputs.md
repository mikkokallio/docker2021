# Exercise 1.1 Getting started
```
docker container ls -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
2e4f7082d86c        nginx               "/docker-entrypoint.…"   48 seconds ago      Exited (0) 13 seconds ago                       nice_liskov
790470dd6907        nginx               "/docker-entrypoint.…"   49 seconds ago      Exited (0) 3 seconds ago                        confident_zhukovsky
22575bed77fa        nginx               "/docker-entrypoint.…"   51 seconds ago      Up 50 seconds               80/tcp              stoic_goldberg
```

# Exercise 1.2 Cleanup
```
docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
```

# Exercise 1.3 Secret message
```
azureuser@docker-test:~$ docker run -d devopsdockeruh/simple-web-service:ubuntu
...
Status: Downloaded newer image for devopsdockeruh/simple-web-service:ubuntu
9ae1eb721f9d97147faf8614a606d88c681600ea360ce60f4d05e9a6718177eb
azureuser@docker-test:~$ docker exec -it 9ae bash
root@9ae1eb721f9d:/usr/src/app# tail -f ./text.log
2021-06-13 15:46:00 +0000 UTC
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
```

# Exercise 1.4 Missing dependencies
```
azureuser@docker-test:~$ sudo docker run -it -d --name website ubuntu:16.04 sh -c 'echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'
Unable to find image 'ubuntu:16.04' locally
...
Status: Downloaded newer image for ubuntu:16.04
74d7773f4b823cfb52330bc643b6d98b0881475942ec8ced00bb2766b29fab9f
azureuser@docker-test:~$ docker exec -it website bash
root@74d7773f4b82:/# apt-get update
...
Reading package lists... Done
root@74d7773f4b82:/# apt-get install curl
...
129 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...
done.
root@74d7773f4b82:/# exit
exit
azureuser@docker-test:~$ docker attach website
helsinki.fi
Searching..
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="https://www.helsinki.fi/">here</a>.</p>
</body></html>
```

# Exercise 1.5 Sizes of images
Size comparison:
```
azureuser@docker-test:~$ docker images
REPOSITORY                          TAG                 IMAGE ID            CREATED             SIZE
devopsdockeruh/simple-web-service   ubuntu              4e3362e907d5        3 months ago        83MB
devopsdockeruh/simple-web-service   alpine              fd312adc88e0        3 months ago        15.7MB
```

Curling works pretty much the same as from the Ubuntu image:
```
`azureuser@docker-test:~$ docker run -it -d --name website2 alpine sh -c 'echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'
f01a172b37331ef202ee365890eaaa6da0af0aea5a3159b57aedbce1b32480a9
azureuser@docker-test:~$ docker exec -it website2 sh
/ # apk add curl
...
OK: 8 MiB in 19 packages
/ # exit
azureuser@docker-test:~$ docker attach website2
helsinki.fi
Searching..
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="https://www.helsinki.fi/">here</a>.</p>
</body></html>
azureuser@docker-test:~$
```

# Exercise 1.6 Hello Docker Hub
```
azureuser@docker-test:~$ docker run -it devopsdockeruh/pull_exercise
Unable to find image 'devopsdockeruh/pull_exercise:latest' locally
latest: Pulling from devopsdockeruh/pull_exercise
8e402f1a9c57: Pull complete
5e2195587d10: Pull complete
6f595b2fc66d: Pull complete
165f32bf4e94: Pull complete
67c4f504c224: Pull complete
Digest: sha256:7c0635934049afb9ca0481fb6a58b16100f990a0d62c8665b9cfb5c9ada8a99f
Status: Downloaded newer image for devopsdockeruh/pull_exercise:latest
Give me the password: basics
You found the correct password. Secret message is:
"This is the secret message"
```

# Exercise 1.7 Two line Dockerfile
Commands to build and run the image:
```
azureuser@docker-test:~/twoline$ docker build . -t web-server
...
Successfully built 794f9585ff41
Successfully tagged web-server:latest
azureuser@docker-test:~/twoline$ docker run web-server
[GIN-debug] [WARNING] Creating an Engine instance with the Logger and Recovery middleware already attached.

[GIN-debug] [WARNING] Running in "debug" mode. Switch to "release" mode in production.
 - using env:   export GIN_MODE=release
 - using code:  gin.SetMode(gin.ReleaseMode)

[GIN-debug] GET    /*path                    --> server.Start.func1 (3 handlers)
[GIN-debug] Listening and serving HTTP on :8080
```

Dockerfile:
```
FROM devopsdockeruh/simple-web-service:alpine
CMD ["server"]
```

# Exercise 1.8 Image for script
```
azureuser@docker-test:~/script$ docker build -t curler .
...
Successfully built 5c1a1fd8a208
Successfully tagged curler:latest
azureuser@docker-test:~/script$ docker run -it curler
Input website:
helsinki.fi
Searching..
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="https://www.helsinki.fi/">here</a>.</p>
</body></html>
```

```
FROM ubuntu:18.04 

COPY script.sh . 

RUN apt-get update && apt-get install -y curl
RUN chmod +x ./script.sh
ENTRYPOINT ./script.sh
```

# Exercise 1.9 Volumes
```
azureuser@docker-test:~/mount$ touch text.log
azureuser@docker-test:~/mount$ docker run -v $(pwd)/text.log:/usr/src/app/text.log devopsdockeruh/simple-web-service
Starting log output
Wrote text to /usr/src/app/text.log
Wrote text to /usr/src/app/text.log
Wrote text to /usr/src/app/text.log
^Cazureuser@docker-test:~/mount$ cat text.log
2021-06-13 19:14:56 +0000 UTC
2021-06-13 19:14:58 +0000 UTC
2021-06-13 19:15:00 +0000 UTC
```

# Exercise 1.10 Ports open
```
azureuser@docker-test:~$ docker run -p 3000:8080 -d web-server
f2000352d97cba6a052e2165ff89dbc0695e6c3946ddb59a1d1406dde58ca3d3
azureuser@docker-test:~$ docker port f20
8080/tcp -> 0.0.0.0:3000
```
Connecting to http://137.135.212.14:3000/ (Azure VM) in browser:
```
message	"You connected to the following path: /"
path	"/"
```

# Exercise 1.11 Spring
Got a button in browser that printed "Success".
```
FROM openjdk:8
COPY . /usr/src/myapp
WORKDIR /usr/src/myapp
RUN ./mvnw package 
CMD ["java","-jar","./target/docker-example-1.1.3.jar"]
EXPOSE 8080 
```

```
sudo docker build -t java .
sudo docker run -p 8080:8080 java

```

# Exercise 1.12 Hello, frontend!
Dockerfile
```
FROM node:current-slim
WORKDIR /app
#ENV API_URL=http://137.135.212.14:8000/
ENV PATH /app/node_modules/.bin:$PATH
COPY package.json ./
COPY package-lock.json ./
RUN npm ci
RUN npm install react-scripts@3.4.1 -g
RUN npm install -g serve
COPY . ./
RUN npm run build
EXPOSE 5000
CMD [ "serve", "-s", "-l", "5000", "build" ]
```

Ran it with `docker run -p 5000:5000 front:prod` and was greeted with `Exercise 1.12: Congratulations! You configured your ports correctly!`.

# Exercise 1.13 Hello, backend!
Dockerfile
```
FROM golang:1.16.7-alpine3.14

RUN mkdir /app
COPY . /app
WORKDIR /app

RUN go build
CMD ["/app/server"]
```

Command:
```
docker run -p 8080:8080 -e GIN_MODE=release backend
```

# Exercise 1.14 Environment
The following updates to Dockerfiles were required (otherwise the files remained as above).

Frontend: Changed `npm run build` to `RUN REACT_APP_BACKEND_URL=http://168.61.93.220:8080 npm run build`.
Backend: Added `ENV REQUEST_ORIGIN=http://168.61.93.220:5000`.

Commands
```
docker run -d -p 5000:5000 frontend
docker run -d -p 8080:8080 -e GIN_MODE=release backend
```

Result was `Exercise 1.14: Success! Great job!`.

# Exercise 1.15: Homework
```
```

# Exercise 1.16: Heroku
