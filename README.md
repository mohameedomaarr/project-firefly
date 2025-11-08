# Project Firefly: A Scalable Web Application on AWS

Welcome to **Project Firefly**! This is a highly scalable and resilient web application built with a modern Java stack and deployed on Amazon Web Services (AWS). The architecture is designed for high availability, fault tolerance, and a seamless user experience, leveraging a suite of powerful technologies for everything from data persistence to asynchronous messaging.

The live application can be viewed here: **[https://d2cg06jgk8bhdt.cloudfront.net/welcome](https://d2cg06jgk8bhdt.cloudfront.net/welcome )**

## Table of Contents

- [Project Description](#project-description)
- [Technologies Used](#technologies-used)
- [Prerequisites](#prerequisites)
- [How to Build and Run](#how-to-build-and-run)
  - [1. Database Setup](#1-database-setup)
  - [2. Configure Application Properties](#2-configure-application-properties)
  - [3. Build the Project](#3-build-the-project)
  - [4. Run the Application](#4-run-the-application)
- [Cloud Architecture Overview](#cloud-architecture-overview)

## Project Description

Project Firefly is a full-featured web application that demonstrates a robust, cloud-native architecture. The system is designed to handle a high volume of user traffic by distributing load efficiently, caching frequently accessed data, and decoupling services for better resilience. It serves as a practical example of deploying a Spring-based application in a sophisticated cloud environment.

## Technologies Used

This project integrates a variety of powerful technologies:

-   **Backend**: Spring MVC, Spring Security, Spring Data JPA
-   **Build Tool**: Maven
-   **Frontend**: JSP (JavaServer Pages)
-   **Web Server**: Apache Tomcat
-   **Database**: MySQL
-   **Caching**: Memcached
-   **Messaging Queue**: RabbitMQ
-   **Search**: Elasticsearch

## Prerequisites

Before you begin, ensure you have the following installed on your local machine:
-   JDK 11 or later
-   Maven 3.x
-   MySQL 8 Server

## How to Build and Run

Follow these steps to get the project running locally.

### 1. Database Setup

The project uses a MySQL database. A database dump is provided in the source files.

1.  Create a new database in MySQL named `accounts`:
    ```sql
    CREATE DATABASE accounts;
    ```

2.  Import the SQL dump into the newly created database. Open your terminal or command prompt and run the following command from the root of the project directory:
    ```bash
    mysql -u <your_mysql_user> -p accounts < src/main/resources/db_backup.sql
    ```
    You will be prompted to enter your MySQL password.

### 2. Configure Application Properties

You will need to update the configuration file with your local environment details (e.g., database credentials, Memcached/RabbitMQ host).

-   Locate the `application.properties` file (usually in `src/main/resources`).
-   Update the following properties to match your setup:
    ```properties
    # Example properties - update with your details
    spring.datasource.username=<your_mysql_user>
    spring.datasource.password=<your_mysql_password>

    # Update if your Memcached/RabbitMQ servers are not on localhost
    memcached.host=127.0.0.1
    rabbitmq.host=127.0.0.1
    ```

### 3. Build the Project

Use Maven to compile the source code and package it into a `.war` file.

-   Navigate to the root directory of the project in your terminal.
-   Run the Maven build command:
    ```bash
    mvn clean install
    ```
    This will generate a `target` directory containing the packaged application (e.g., `project-firefly.war`).

### 4. Run the Application

You can run the application by deploying the `.war` file to an external Tomcat server or by using an embedded server if configured.

-   **To Deploy on Tomcat**: Copy the generated `.war` file from the `target` directory to the `webapps` directory of your Tomcat installation. Start the Tomcat server, and the application will be deployed.

## Cloud Architecture Overview

The production environment for Project Firefly is deployed on AWS, leveraging the following services for scalability and resilience:

-   **Amazon Route 53**: Manages DNS routing to direct users to the application.
-   **Amazon CloudFront**: Acts as a CDN to cache content and reduce latency.
-   **Elastic Load Balancer (ELB)**: Distributes incoming traffic across multiple instances.
-   **AWS Elastic Beanstalk**: Manages the application deployment, scaling, and health monitoring on Apache Tomcat.
-   **Amazon RDS for MySQL**: Provides a managed, scalable relational database.
-   **Amazon ElastiCache for Memcached**: Used for in-memory data caching.
-   **Amazon MQ**: A managed message broker service for RabbitMQ.
-   **Amazon S3**: Stores application artifacts and other static assets.
-   **Amazon CloudWatch**: Monitors application logs and metrics.
