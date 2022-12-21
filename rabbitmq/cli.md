# CLI

Open Docker desktop. We’ll map `port 15672` for the management web app and `port 5672` for the message broker.

```docker
docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3.11-management
```

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

RabbitMQ is only interesting if we can send messages,open rabbitmq:

```docker
docker exec -it rabbitmq bash
```

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

**List queues for the default virtual host:**

```
rabbitmqctl list_queues
```

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

**List\_exchange:**

```
rabbitmqctl list_exchanges
```

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

**Make a Binding:**

```
./rabbitmqadmin --vhost="Some_Virtual_Host" declare binding source="some_exchange" destination_type="queue" destination="some_incoming_queue" routing_key="some_routing_key"
```

```
rabbitmqadmin declare binding source="amq.direct" destination_type="queue" destination="vy" routing_key="vy13"
```

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

```
rabbitmqadmin publish exchange="amq.direct" payload="123" routing_key="vy13"
```

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

```
rabbitmqadmin get queue="vy"
```

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

```
rabbitmqadmin get queue="vy" ackmode=ack_requeue_false
```

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

```
rabbitmqctl list_queues
```

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
