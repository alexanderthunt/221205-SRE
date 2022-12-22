# Planetarium

The Planetarium is a web service that allows users to add planets and associated moons to a central database to map the night sky. Users must register an account to participate, and those who do will be able to associate themselves with the planets and moons they add to the database. In the previous Sprint, you implemented the repository and service layer of the application, implemented logging, and created a bash script solution to measure the SLIs of the application.

In this sprint you will be converting this application into a Spring Boot application and adding on new observability tools in order to prepare for monitoring more SLIs. You will also be using Docker to containerize the application and the associated monitoring tools for ease of deployment. This is a critical step that must be completed before the main goal for this application can be achieved: deployment to Kubernetes.

## Key Terminology
- **Project**
  - A software application built for some company/entity
  - Examples
    - Employee paid time off Scheduler
    - Helicopter Navigation System
    - To-Do task manager
- **Sprint**
    - a term used to describe a short period of development work, typically no more than a few weeks of time
- **Minimum Viable Product**
    - a phrase used to describe a project that has the minimum number of features and functionality applied to make the sprint considered successful

## Development Requirements
The application currently utilizes Javalin and JDBC: you will be converting the app to use Spring Boot with the **Spring Data**, **Spring Web**, and **Spring Actuator** modules.
- All repository, service, and API layer features must be recreated in Spring Boot
    - your application should connect to the same database you used from P0
    - you will NOT need a ConnectionUtil class for P1
- After converting the project over to Spring Boot, you will need to containerize the project and save the image on Docker Hub
    - any updates to the project/image need to be saved to Docker Hub

- After containerizing the application you will need to implement/add the following technologies to your application deployment via a docker compose file:
    - Micrometer
    - Promtail
    - Loki
    - Prometheus
    - Grafana
-

## SRE Requirements
In the previous Sprint you used bash to calculate your SLIs: this time around you will be making use of some new tools. The following technologies must be implemented/deployed alongside the containerized planetarium app to achieve mvp requirements:
- Micrometer
- Promtail
- Loki
- Prometheus
- Grafana

### Service Level Objects
- 99.8% of requests should complete successfully within 200 milliseconds

### Service Level Indicators
- Latency
    - you should track how long it takes for the Planetarium app to handle requests made to the system
- Error Rate
    - you should track the percentage of how many http requests return a non-500 status code

### Service Level Indicator Exposure
Micrometer will expose the relevant data in your Spring application, and Prometheus will scrape the data from Micrometer. You will make use of Grafana to visualize and track your SLIs.

# MVP Requirements Rundown
- Development
    - All repository, service, and API layer methods should be implemented in a Spring Boot application
    - A docker image of your application should be created and saved in Docker Hub
    - A docker compose file should be created to handle deploying your containerized application and auxilary software
- SRE
    - Logs generated by the Planetarium should be persisted in a volume outside of the running container
    - Your application should expose metrics concerning http requests made and latency times via Micrometer
    - Promtail should push your application logs to loki
    - Prometheus should be able to scrape your SLI metrics exposed by Micrometer
    - You should be able to view your metrics over time provided by Prometheus and your logs within Loki by utilizing Grafana
- Presentation date is 1/5/2023

# Stretch Goal
Stretch goals are things to work on ONLY when all MVP requirements have been accomplished: listed below are optional features you can add to the project to enhance it further:
    - Add Alerting by using AlertManager and Prometheus