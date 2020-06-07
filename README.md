# Docker-Microservices-Nameko

## REPO

### Services

- gateway: Exposing HTTP API to be used by external clients, Web or Mobile Apps

- products: create/store/manage product info and exposing Remote Procedure Call (RPC) API that can be consumed by other services. This service uses Redis as database.

- oders: create/store/manage oder info and also exposing RPC API which is consumed by other services.

## Nameko

- [Nameko is a framework for building microservices in Python.](https://nameko.readthedocs.io/en/stable/what_is_nameko.html)
- Out of the box you can build a service that can respond to RPC messages, dispatch events on certain actions, and listen to events from other services. It could also have HTTP interfaces for clients that can’t speak AMQP, and a websocket interface for, say, Javascript clients.

## DBeaver

- Download and install [DBeaver](https://dbeaver.io) as GUI configuration to the PostgresSQL database via port 5432

## Docker

- [Download and Install Docker](https://www.docker.com)
- Run the .yml file to build the containers as environment

```
docker-compose up

```

## CRUD

- Create Product

```sh
$ curl -XPOST -d '{"id": "product_1", "title": "Generator", "capacity": 1000, "maximum_speed": 5, "in_stock": 10}' 'http://localhost:8003/products'

```

- Read Product

```sh
$ curl 'http://localhost:8003/products/product_1'
```

- Create Order

```sh
$ curl -XPOST -d '{"order_details": [{"product_id": "product_1", "price": "100000.99", "quantity": 1}]}' 'http://localhost:8003/orders'

{"id": 1}
```

- Read Order

```sh
$ curl 'http://localhost:8003/orders/1'
```

## Testing

Ensure RabbitMQ, PostgreSQL and Redis are running and `config.yaml` files for each service are configured correctly.

`$ make coverage`

## FELK

- FELK stands for Filebeat,Elasticsearch, Logstash, Kibana

### Filebeat

- In the file filebeat.yml, there are codes for reading .log files and instant docker inputs
- The docker inputs are live-running containers except running ELK containers since they have been supported by Kibana
- The filebeat.autodiscover mode can identify all running containers
  Ports used for config. :

* 5044: Logstash
* 9200: Elasticsearch
* 5601: Kibana

### Kibana

- Type the localhost:5061 in the browser to go as an entry point to Kibana interface.
- For default the id and password corresponding to "elastic" and "password".
- Remember to change reload in Kibana from default "last 15 minutes" to "Year to date" to observe the whole example .log data
