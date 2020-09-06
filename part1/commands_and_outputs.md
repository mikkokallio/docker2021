Exercise 1.1
```
docker container ls -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
2e4f7082d86c        nginx               "/docker-entrypoint.…"   48 seconds ago      Exited (0) 13 seconds ago                       nice_liskov
790470dd6907        nginx               "/docker-entrypoint.…"   49 seconds ago      Exited (0) 3 seconds ago                        confident_zhukovsky
22575bed77fa        nginx               "/docker-entrypoint.…"   51 seconds ago      Up 50 seconds               80/tcp              stoic_goldberg
```

Exercise 1.2
```
docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
```

Exercise 1.3
```
docker@boot2docker:~$ docker run -it devopsdockeruh/pull_exercise
Unable to find image 'devopsdockeruh/pull_exercise:latest' locally
latest: Pulling from devopsdockeruh/pull_exercise
8e402f1a9c57: Pull complete                                                                                                                                                                                                                  5e2195587d10: Pull complete                                                                                                                                                                                                                  6f595b2fc66d: Pull complete                                                                                                                                                                                                                  165f32bf4e94: Pull complete                                                                                                                                                                                                                  67c4f504c224: Pull complete                                                                                                                                                                                                                  Digest: sha256:7c0635934049afb9ca0481fb6a58b16100f990a0d62c8665b9cfb5c9ada8a99f
Status: Downloaded newer image for devopsdockeruh/pull_exercise:latest
Give me the password: basics
You found the correct password. Secret message is:
"This is the secret message"
```

Exercise 1.4
```
docker@boot2docker:~$ docker run -d devopsdockeruh/exec_bash_exercise
b6690cad977681736de9ce91477b36b353039a95c0bc5dcd48877e8d31ab02f6
docker@boot2docker:~$ docker exec -it b66 bash
root@b6690cad9776:/usr/app# tail -f ./logs.txt
"Docker is easy"
```

Exercise 1.5
```
docker@boot2docker:~$ docker run -it -d --name website ubuntu:16.04 sh -c 'echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'
b1b2f3b3a3659b15e5a4a6a3bea695381292d60d71ef7a4aab8ca4563dc2ec1f
docker@boot2docker:~$ docker exec -it website bash
root@b1b2f3b3a365:/# apt-get update
Get:1 http://security.ubuntu.com/ubuntu xenial-security InRelease [109 kB]
...
Get:18 http://archive.ubuntu.com/ubuntu xenial-backports/universe amd64 Packages [9084 B]
Fetched 16.6 MB in 16s (1033 kB/s)
Reading package lists... Done
root@b1b2f3b3a365:/# apt-get install curl
Reading package lists... Done
...
After this operation, 19.0 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu xenial/main amd64 libffi6 amd64 3.2.1-4 [17.8 kB]
...
done.
root@b1b2f3b3a365:/# exit
exit
docker@boot2docker:~$ docker attach website
helsinki.fi
Searching..
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://www.helsinki.fi/">here</a>.</p>
</body></html>
docker@boot2docker:~$
```

Exercise 1.6
```
docker@boot2docker:~/docker2020/part1/overwrite$ docker build -t docker-clock .
Sending build context to Docker daemon  2.048kB
Step 1/2 : FROM devopsdockeruh/overwrite_cmd_exercise
 ---> 3d2b622b1849
Step 2/2 : CMD ["-c"]
 ---> Running in 7cba9ffe8fd3
Removing intermediate container 7cba9ffe8fd3
 ---> a121f1f011bb
Successfully built a121f1f011bb
Successfully tagged docker-clock:latest
docker@boot2docker:~/docker2020/part1/overwrite$ docker run docker-clock
1
2
```

Exercise 1.7
```
```

Exercise 1.8
```
```

Exercise 1.9
```
```

Exercise 1.10
```
```

Exercise 1.11
```
```

Exercise 1.12
```
```

Exercise 1.13
```
```

Exercise 1.14
```
```

Exercise 1.15
```
```
