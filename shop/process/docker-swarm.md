docker swarm init

docker secret create mycert.ca mycert.ca
docker secret ls
docker secret rm secret_name

все файлы-секреты внутри контейнера открываются в /run/secrets/

docker config create my.conf my.conf
docker config ls
docker config rm secret_name

docker stack deploy stack_name -c docker-compose.yml
docker stack rm stack_name

Работа с монтируемыми разделами описана здесь
https://docs.docker.com/storage/volumes/
Есть 3 типа - это volume, bind data и tmpfs (RAM).
Предпочтительно использовать volume.

* Пример:
version: "3.9"
services:
  frontend:
    image: node:lts
    volumes:
      - myapp:/home/node/app
volumes:
  myapp:

здесь volume с именем myapp монтируется по указанному пути внутри контейнера. 
Снаружи он будет лежать в /var/lib/docker/volumes