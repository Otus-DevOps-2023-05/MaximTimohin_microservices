# MaximTimohin_microservices
MaximTimohin microservices repository

### Выполненено задание Ansible-2

##### Создаём инстанс
```
yc compute instance create  --name docker-host  --zone ru-central1-a  --network-interface subnet-name=default-ru-central1-a,nat-ip-version=ipv4  --create-boot-disk image-folder-id=standard-images,image-family=ubuntu-2004-lts,size=15 --preemptible --cores=2  --ssh-key ../ssh/MaxOtus.pub
```

##### Подключаем docker-machine
```
docker-machine create --driver generic  --generic-ip-address=158.160.116.248 --generic-ssh-user yc-user  --generic-ssh-key ../ssh/MaxOtus docker-host
```
##### Проверяем docker-machine

```
11:08 # docker-machine ls
NAME          ACTIVE   DRIVER    STATE     URL                          SWARM   DOCKER    ERRORS
docker-host   -        generic   Running   tcp://158.160.116.248:2376           v24.0.5
```

##### Собираем образ

```
docker build -t reddit:latest .
Building 81.7s (15/15) FINISHED
```

##### Запускаем образ

```
docker run --name reddit -d --network=host reddit:latest
3004407654c6480a6e082ae1a668a7ec11dbeaf75f8bec0d68003e04afc623b1
docker ps
CONTAINER ID   IMAGE           COMMAND       CREATED         STATUS         PORTS     NAMES
3004407654c6   reddit:latest   "/start.sh"   5 seconds ago   Up 5 seconds             reddit
```

##### Авторизуемся на docker-hub
```
docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: maxim237
Password:

Login Succeeded
```
##### Заливаем наш образ

```
11:23 # docker tag reddit:latest maxim237/otus-reddit:1.0

11:25 # docker push  maxim237/otus-reddit:1.0
The push refers to repository [docker.io/maxim237/otus-reddit]
a71ae2423ea3: Pushed
6053b298ca7a: Pushed
bb645819ed70: Pushed
dfbde7aee5ac: Pushed
0cdec5645b3a: Pushed
278de25f02a6: Pushed
03a7d893b101: Pushed
ccb6107abed2: Pushed
d71d5f9d359f: Pushed
548a79621a42: Mounted from library/ubuntu
1.0: digest: sha256:f52dfda66c66d625c42cbda0bf8d05a2a39c7adcc0165e6f965934cb269ded8f size: 2414
```


##### Monitoring1
https://hub.docker.com/r/maxim237/post
https://hub.docker.com/r/maxim237/comment
https://hub.docker.com/r/maxim237/ui
https://hub.docker.com/r/maxim237/prometheus
