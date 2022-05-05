# Sistemas Distribuidos - Tarea 2

En este repositorio tendremos el codigo y las instrucciones para ejecutar la tarea 2 de sistemas distribuidos, esta consiste en implementar un servicio api rest utilizando apache kafka como sistema de streaming de eventos, para efectos de nuestro proyecto utilizaremos nodejs y docker para lograr los objetivos.

## Dependencias

- [nodejs](https://nodejs.org/es/download/package-manager/)
- [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)
- [zookeeper](https://zookeeper.apache.org/releases.html)
- [kafka](https://kafka.apache.org/downloads)
- [docker](https://docs.docker.com/engine/install/)
- [docker-compose](https://docs.docker.com/compose/install/)
- [zookeeper (docker)](https://hub.docker.com/r/bitnami/zookeeper)
- [kafka (docker)](https://hub.docker.com/r/bitnami/kafka)


## Ejecutar

Ejecutamos con

```sh
    docker-compose up -d --build # Se recomienda quitar el tag -d para ver los logs y el --build si no se desea rebuilder.
```

## Topics

Para crear los topic de forma manual usar el siguiente comando:

```sh
docker-compose exec kafka /opt/bitnami/kafka/bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --config retention.ms=259200000 --topic auth
```

Para verificar que este creado usar:

```sh
docker-compose exec kafka /opt/bitnami/kafka/bin/kafka-topics.sh --bootstrap-server localhost:9092 --list
```

## Rutas

### :3000/login

Metodo http post que ingresa una orden, recibe un body:

Ejemplo:

```json
{
	"user": "nicolas.hidalgoc@mail.udp.cl",
	"password": "abcdefg"
}
```

Devuelve estado 200 y data agregada de estar correcto.

### :5000/blocked

Metodo http get que genera el resumen de usuarios bloqueados, devuelve estado 200 de estar correcto y un json.

Ejemplo:

```json
{
	"users-blocked": [
		"nicolas.hidalgoc@mail.udp.cl",
        "nicolas.nunez2@mail.udp.cl"
	]
}
```