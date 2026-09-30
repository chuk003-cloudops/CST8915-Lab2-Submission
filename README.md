# CST8915 Lab 2 Submission

## Demo video

[Watch the unlisted CST8915 Lab 2 demo](https://youtu.be/23epkCsw2ns)

The demo records the Azure virtual machines and service configuration, places a storefront order, and verifies that the durable RabbitMQ order queue increments.

## Service repositories

- Order service: https://github.com/chuk003-cloudops/order-service
- Product service: https://github.com/chuk003-cloudops/product-service
- Store front: https://github.com/chuk003-cloudops/store-front

## Reflection

### Configuration and backing services

The Order Service reads its RabbitMQ connection string and listening port from environment variables. The Product Service reads its port from the environment and loads an optional local .env file. Deployment-specific settings stay outside the application code. In the Azure deployment, the Order Service connects to RabbitMQ through a dedicated application account. No credentials are committed to these repositories.

### Environment variables

Environment variables let the same application code run in different environments with different addresses, ports, and credentials. They keep deployment settings out of source code and make it easier to change configuration without editing application logic. The Store Front uses public API URLs; browser-visible VUE_APP_ settings must not contain secrets.

### Separate service repositories

Separate repositories give each microservice its own history, dependencies, tests, and release process. A service can be changed or deployed without requiring the other services to release at the same time. Each service can also be scaled independently based on its workload.

## Deployment notes

The demo uses four dedicated Azure VMs for the Order Service, Product Service, RabbitMQ, and Store Front. The video shows the VM names and public IP addresses, service configuration, a successful storefront order, and the resulting queue count. The VMs were stopped and deallocated after verification to avoid ongoing compute charges; start them in Azure before reproducing the live demo.

## Verification evidence

- [x] The three service repositories contain the refactored source, dependency manifests, lockfiles, and .env.example files.
- [x] Each service was verified on its own VM, and the Store Front loaded products from the Product Service.
- [x] An order through the Store Front reached the Order Service and was published to RabbitMQ.
- [x] rabbitmqctl list_queues name durable messages showed the durable order_queue and an increased message count after an order.
- [x] The unlisted video shows all four VM names and public IPs plus environment-based configuration without revealing credentials.
- [x] This public submission repository includes the unlisted video link.

Do not add local .env files, RabbitMQ credentials, or private keys to this repository.
