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
```

Exercise 1.6
```
```

Exercise 1.7
```
```

Exercise 1.8
```
```
