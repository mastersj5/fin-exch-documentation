# [Glossary (Terms and Concepts)](#glossary-terms-and-concepts)

This is a glossary of terms helpful when working with the Iceberg Financial Exchange or reading its docs.

`Terms are organized in a hierarchical order. This means that reading from top to bottom will allow for understanding to flow more naturally as terms are sorted from most general to more specific.`


# Table of Contents
1. [Core Terms](#core-terms)
2. [Additional Relevant Terms](#additional-relevant-terms)
3. [Technical Terminology](#technical-terminology)
    1. [Networking & Communication](#networking--communication)
    2. [Data Handling](#data-handling)
    3. [Distributed Systems](#distributed-systems)
    4. [Development & Languages](#development--languages)
    5. [Kafka](#kafka-terms)


# Core Terms

## [Firm](#firm)
- A financial institution or company authorized to trade securities on an exchange.

## [Stock](#stock)
- A share of ownership in a company, representing a claim on a portion of the company's assets and earnings.

## [Order](#order)
- An instruction to buy or sell a specific stock at a specified price or better.

## [Buy/Bid](#bid)
- (An order to purchase a stock. The highest price a buyer is willing to pay for a stock.

## [Sell/Ask (Offer)](#sell)
- An order to dispose of a stock. The lowest price a seller is willing to accept for a stock.

## [Book (Order Book)](#book-order-book)
- A centralized record of all outstanding buy and sell orders for a specific stock, organized by price level. 
- All the orders that have been placed for a stock. There is a book for every stock. Each book has two lists. A bid list (buy orders) and an offer list (sell orders) that are sorted in price time order. Bid list has highest price at the top and offer list has lowest price at the top.

## [Max Order Notional](#max-order-notional)
- The max amount a user is allowed to place on an order.

## [Max Capital](#max-capital)
- The total amount a user can spend in general (not just on orders).

## [Firm Risk](#firm-risk)
- The maximum potential loss a firm can incur on a single order due to exceeding the max order notional value while considering the max capital available.
- The firm sets a max order notional which is the total theoretical value of an order if the entire order is filled at the current market price. However, the firm also has a max capital limit which restricts the total amount of capital it is willing to risk on that order. Firm Risk ensures the firm doesn't commit more capital than intended even if the market price moves against them.

## [User Risk](#user-risk)
- The maximum potential loss a user can incur on a single order due to exceeding the max order notional value while considering the max capital available.
- Similar to Firm Risk, User Risk focuses on protecting the user from exceeding their risk tolerance. The user sets a max order notional which limits the total potential value of the order based on the current market price. The max capital further restricts the amount of capital the user is willing to risk on that order. User Risk ensures the user doesn't lose more than they intended even if the market moves against them.

## [User Position](#user-position)
- The total holdings of a particular stock by an individual user on the exchange.

### [MPID (Market Participant Identifier)](#mpid-market-participant-identifier)
- A unique code assigned to all firms and institutions participating in a financial exchange, used for identification and tracking purposes.

<br/><br/>

# Additional Relevant Terms

## [Execution](#execution)
- The completion of a buy or sell order.

## [Fill](#fill)
- A fully or partially executed order.

## [Market Order](#market-order)
- An order to buy or sell a stock at the best available current market price.

## [Limit Order](#limit-order)
- An order to buy or sell a stock at a specified price or better.

## [Quote](#quote)
-  The highest (best) bid price level and the lowest (best) offer price level form a quote.

## [Best Bid and Best Offer (BBO)](#bbo)
- The highest bid quote and lowest offer quote are known as the best bid and best offer. Collectively called the BBO.

## [Spread](#spread)
- The difference between the bid and ask prices.

## [Liquidity](#liquidity)
- The ease with which a stock can be bought or sold without significantly impacting its price.

<br/><br/>

# Technical Terminology

## Networking & Communication

### [HTTP (Hypertext Transfer Protocol)](#http-hypertext-transfer-protocol)
- The underlying protocol used for communication on the web, enabling the transfer of data between clients (like web browsers) and servers.

### [API (Application Programming Interface)](#api-application-programming-interface)
- A way for two or more computer programs or components to communicate with each other. It is a type of software interface, offering a service to other pieces of software.
- Specifically, in a financial exchange, APIs define the rules and specifications for how various software components can interact with the exchange. They provide a structured way for:
    - External Systems:
        - Third-party trading platforms to submit or cancel orders.
        - Market data providers to stream real-time price updates.
        - Risk management systems to assess a trade's risk profile.
    - Internal Microservices:
        - The Matching Engine to communicate with the Data Warehouse for updated stock information.
        - The Event Logger to record trade execution events.
- Key Purposes of APIs in a financial exchange:
    - Order Management - Allow clients and external systems to place, modify, and cancel orders securely.
    - Market Data - Distribute real-time or historical market data, including prices, order book depth, and trading volumes.
    - Risk Assessment - Provide interfaces to calculate risk metrics on potential trades before execution.
    - System Monitoring - Expose data for monitoring system health, performance, and event logging.


### [REST API](#rest-api)
- (Representational State Transfer) A standardized architectural style for designing web APIs that typically use HTTP requests to access and manipulate data.

### [Latency](#latency)
- The time it takes for a data packet to travel from one point to another on a network. In financial exchanges, low latency is crucial for fast order execution and market data updates.


## Data Handling

### [Database](#database)
- An organized collection of data, typically structured for easy storage, search, retrieval, and modification.

### [MongoDB](#mongodb)
- A non-relational database offering flexibility in data structures and scaling, sometimes used for high-volume, unstructured data in financial applications.


## Distributed Systems

### [Microservices](#microservices)
- An architectural approach that structures an application as a collection of small, independent, and loosely coupled services.

### [Event-Driven Architecture](#event-driven-architecture)
- A software design pattern centered around the production, detection, and consumption of events, promoting real-time responsiveness and scalability.

### [Kafka Platform](#kafka-platform)
- A high-throughput distributed streaming platform used for building real-time data pipelines and applications.

### [Message Queue](#message-queue)
- A component used for asynchronous communication between services, allowing services to send and receive messages without a direct connection.

### [Load Balancing](#load-balancing)
- The process of distributing workloads across multiple computing resources (servers) to optimize performance and reliability.

## Development & Languages

### [Java](#java)
- Popular programming language for financial applications. Java offers ease of development.

### [React](#react)
- A JavaScript library for building dynamic, component-based user interfaces.

### [Spring Boot](#spring-boot)
- A Java-based framework that simplifies the development of enterprise-grade web applications and microservices.

## Kafka Terms

### [Kafka](#kafka)
- An open-source platform designed for handling real-time data streams. It acts as a central hub for producers (services that publish data) and consumers (services that subscribe to and receive data).

### [Event](#event)
- In Kafka, an event represents any piece of data representing a change or happening within the system. 

### [Topic/Channel (Event Channel)](#channel-event-channel)
- This term can have slightly different meanings depending on the specific Kafka implementation or tooling being used. In general, it often refers to a logical grouping of related events. For example, a category or topic for events.

### [Subscription](#subscription)
- When a service wants to receive updates or data streams from Kafka, it subscribes to a specific topic or channel. This establishes a connection where the service receives all the events published to that channel by producers.

### How the above terms work together:
1. **Producers** publish events (data) to a specific Kafka topic or channel.
2. **Consumers** can subscribe to these channels or topics.
3. Once subscribed, the consumer receives a real-time stream of all new events published to that channel by producers.


<!--- References/Footnotes: --->

[1]: https://www.tn.gov/commerce/securities/investors/what-is-a-security.html