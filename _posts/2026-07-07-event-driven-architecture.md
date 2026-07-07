---
layout: post
title: Event-Driven Architecture with Kafka
date: 2026-07-07 10:00:00 +0530
categories: [Architecture]
tags: [Kafka, Events, Microservices]
description: Building scalable event-driven systems using Kafka.
---

# Event-Driven Architecture with Kafka

This article walks through a simple event-driven architecture and provides
sample code and diagrams.

---

## System Overview

The following diagram shows the overall architecture.

![Architecture Overview](/assets/images/event-driven/overview.png)

---

## Message Flow

A typical request flows through the system as follows.

![Sequence Diagram](/assets/images/event-driven/sequence-diagram.svg)

1. Client submits an order.
2. Order Service validates the request.
3. An `OrderCreated` event is published.
4. Inventory and Billing services consume the event.
5. Notifications are sent.

---

## Example Event

```json
{
  "eventType": "OrderCreated",
  "orderId": "ORD-1001",
  "customerId": "C12345",
  "total": 249.99
}
```

---

## Sample Project

You can download the complete sample application here.

- [Sample Project ZIP](/assets/downloads/event-driven/sample-project.zip)
- [Architecture Document (PDF)](/assets/downloads/event-driven/architecture.pdf)
- [JSON Event Schema](/assets/downloads/event-driven/event-schema.json)

---

## Deployment Diagram

![Deployment](/assets/images/event-driven/deployment.png)

---

## Comparison

| Approach | Advantages | Disadvantages |
|----------|------------|---------------|
| REST | Simple | Tight coupling |
| Events | Loosely coupled | More operational complexity |

---

## External Resources

Useful references:

- [Apache Kafka](https://kafka.apache.org/)
- [CloudEvents Specification](https://cloudevents.io/)
- [Martin Fowler - Event Sourcing](https://martinfowler.com/eaaDev/EventSourcing.html)

---

## Source Code

```java
public class OrderPublisher {

    public void publish(Order order) {
        Event event = Event.from(order);
        kafkaTemplate.send("orders", event);
    }

}
```

---

## Summary

Event-driven systems provide:

- Loose coupling
- Better scalability
- Independent deployments
- Asynchronous communication

However, they also introduce challenges such as eventual consistency,
observability, and operational complexity.
