# Chuleta de Docker

[![License](https://img.shields.io/aur/license/yaourt.svg)](https://raw.githubusercontent.com/zerjioang/docker-cheatsheet/master/LICENSE)

Esta es la versión en español de 'Docker cheatsheet'

## Acciones en grupo

### Parar todos los contenedores activos
```
docker stop $(docker ps -a -q)
```

### Eliminar todos los contenedores existentes
```
docker rm $(docker ps -a -q)
```

### Matar todos los contenedores activos
```
docker kill $(docker ps -q)
```

## Acciones de limpieza

### Eliminar todos los contendores que no se están ejecutando
```
docker rm -v $(docker ps -a -q -f status=exited)
```

### Eliminar todas las imagenes cacheadas localmente
```
docker rmi $(docker images -f "dangling=true" -q)
```

### Eliminar todos los volumenes de datos de docker no usados
```
docker volume rm $(docker volume ls -qf dangling=true)
```

## Otros comandos

### Obtener la IP asociada a un contendedor
```
#ps para ver el listado de contenedores activos y obtener el ID del contenedor que nos interesa

$ docker ps

CONTAINER ID        IMAGE                              COMMAND                  CREATED             STATUS              PORTS                      NAMES
727342eb31b1        apache                             "apache2-foreground"     18 minutes ago      Up 12 minutes       0.0.0.0:9090->80/tcp       _apache_1
7d08328f61b6        php7.0-fpm:jessie                  "docker-php-entrypoin"   18 minutes ago      Up 12 minutes       9000/tcp                   _php_1
ec0d4a94c9f1        mongo:3.2                          "/entrypoint.sh mongo"   18 minutes ago      Up 12 minutes       0.0.0.0:27017->27017/tcp   _mongo_1
```

```
docker inspect <container id> | grep IPA
```

```
$ docker inspect 727342eb31b1 | grep IPA

            "SecondaryIPAddresses": null,
            "IPAddress": "172.17.0.4",
                    "IPAMConfig": null,
                    "IPAddress": "172.17.0.4",
```

**172.17.0.4** es la IP asociada al contenedor de Apache.
