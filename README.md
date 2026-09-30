# CST8915 Lab 2 Submission

## Demo video

The unlisted demo link will be added after the complete order-to-RabbitMQ flow is verified.

## Service repositories

- Order service: https://github.com/chuk003-cloudops/order-service
- Product service: https://github.com/chuk003-cloudops/product-service
- Store front: https://github.com/chuk003-cloudops/store-front

## Reflection

### Configuration and backing services

I updated the order service to read its RabbitMQ connection string and listening port from environment variables. The product service now reads its port from the environment and loads an optional local `.env` file. This lets the services use deployment-specific settings without hard-coding them in the source. In the Azure deployment, the order service connects to RabbitMQ through the broker VM's address and its application account.

### Environment variables

Environment variables let the same application code run in different environments with different addresses, ports, and credentials. They keep deployment settings out of source code and make it easier to change configuration without editing application logic. The store front only needs public API URLs; its browser-visible `VUE_APP_` settings must not contain secrets.

### Separate service repositories

Separate repositories give each microservice its own history, dependencies, tests, and release process. A service can be changed or deployed without requiring the other services to release at the same time. Each service can also be scaled independently based on its workload.

## Deployment notes

This submission uses four dedicated Azure VMs. The final unlisted demo will show their names, regions, sizes, and public IPs.

## Verification checklist

- [ ] The three service repositories contain the updated source, dependency manifests, lockfiles, and `.env.example` files.
- [ ] Each service runs on its own VM, and the Store Front loads products from the Product Service.
- [ ] An order through the Store Front reaches the Order Service and is published to RabbitMQ.
- [ ] `rabbitmqctl list_queues name durable messages` shows the durable `order_queue` and an increased message count after an order.
- [ ] The demo shows all four VM public IPs and the environment-based configuration without revealing credentials.
- [ ] The unlisted YouTube demo link is added above and the submission repository is public.

Do not add local `.env` files, RabbitMQ credentials, or private keys to this repository. Check items only after verifying them against the running deployment or published repository.
