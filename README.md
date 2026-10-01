# CST8915 Lab 2: Refactor the Algonquin Pet Store - Part 1

- **Student Name**: Ellie Zheng
- **Student ID**: 041078727
- **Course**: CST8915 Full-stack Cloud-native Development
- **Semester**: Fall 2026

---

## Demo Video

🎥 [Watch Demo Video](https://youtu.be/L9m8J5KPHY8)

---

## Links to the Three Service Repositories

- [`order-service`](https://github.com/Ellie-Zheng/cst8915-lab2-order-service)
- [`product-service`](https://github.com/Ellie-Zheng/cst8915-lab2-product-service)
- [`store-front`](https://github.com/Ellie-Zheng/cst8915-lab2-store-front)

---

## Reflection Questions

### What changes did you make to the `order-service` and `product-service` to comply with the Configurations and Backing Services factors of the 12-Factor App methodology?

To comply with Factor 3 (Config), I externalized execution ports and RabbitMQ connection credentials for both `order-service` and `product-service` using environment variables. Local environments load these via `dotenv` from `.env` files, which are strictly gitignored to prevent sensitive credential leaks.
To comply with Factor 4 (Backing Services), RabbitMQ is treated as an attached resource running on an independent VM, so the `order-service` connects to it through a dedicated application account (`orderapp`) rather than relying on a local broker like lab 1.

### Why is it important to use environment variables instead of hard-coding configurations in your application?

Environment variables allow the same source code to run with different ports and service addresses without changing the code for each deployment. They also help keep credentials, such as the RabbitMQ password, out of public repositories. In this lab, I could configure each service for its own VM while keeping those deployment-specific values separate from the code.

### Why is it important to have separate repositories for each microservice? How does this help maintain independence and scalability of each service?

Separate repositories give each service its own code, dependencies, and change history. This lets me update and deploy one service without making unrelated changes to the others. It also supports scaling each service according to its own workload. For example, when the original Order Service VM ran too slowly, I replaced it with a larger VM without having to resize the other services’ VMs.
