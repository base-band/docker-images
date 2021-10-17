# Build with
```bash
docker build -t base-band/quartus-ci-build:base .
```



# Cmds
export BB_PARENT=/home/xxxx/base-band

docker exec -it qrt bash

docker run -dit --name qrt -v ${BB_PARENT}:/src base-band/quartus-ci-build:base

docker exec -it qrt /etc/init.d/ssh start

docker exec -it qrt bash
docker stop qrt
docker rm qrt

