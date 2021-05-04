# laboratorio_bdd

Este laboratorio esta realizado con docker

## Instalar docker - Windows, Linux, Mac
https://docs.docker.com/engine/install/

## Ejecutar laboratorio

```sh
$ git clone https://github.com/Rdavid1991/laboratorio_bdd.git
$ cd laboratorio_bdd
$ docker-compose up -d
```

## Ingresar a contenedor 1

```sh
$ docker exec -it mongo1 bash
```
## Ingresar a mongo
Una vez dentro del contenedor se ejecuta el siguiente comando, este es para acceder a la base de datos
```sh
$ mongo
```
Dentro de la base de datos se ejecuta
```sh
> rs.initiate()
```
Nos retorna algo similar a esto y se preciona enter para que salte a primario, ya que el secundario no permite editar.
```
{
        "info2" : "no configuration specified. Using a default configuration for the set",
        "me" : "10e7f445145b:27017",
        "ok" : 1
}
rs0:SECONDARY>
rs0:PRIMARY>
```

## Ingresar a contenedor 2
Se accede al otro contenedor para uego extraer la IP del mismo
```sh
$ docker exec -it mongo2 bash
$ hostname -I
```
## Agregar una base de datos a otra
```sh
> rs.add('172.20.0.2:27017')
```

Un avez agregado el servidor donde se replicara nuestra base de datos nos devuelve un resultado similar a este.
```
rs0:PRIMARY> rs.add('172.20.0.2:27017')
{
        "ok" : 1,
        "$clusterTime" : {
                "clusterTime" : Timestamp(1620139799, 1),
                "signature" : {
                        "hash" : BinData(0,"AAAAAAAAAAAAAAAAAAAAAAAAAAA="),
                        "keyId" : NumberLong(0)
                }
        },
        "operationTime" : Timestamp(1620139799, 1)
}
```

Listo ya puedes crear informacion en una base de datos y ver como se replica en otra, esto es una guia basica para luego detallarla en el laboratorio.
