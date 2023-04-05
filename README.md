# JohnBryceClasses_Microservices
![image](https://user-images.githubusercontent.com/60425986/230127250-37cf56d3-283d-4a29-88dd-0d1087906c56.png)

## 🤔 What is the purpose of this application?
In this application there are several Spring Framework servers, each server runs a Tomcat Apache server by default and all of them together constitute a microservice application.
The main essence of the application is communication and messaging between service-a and service-b.

## The Application Modules:
config
<br/>
service-a
<br/>
service-b
<br/>
dashboard
<br/>
gateway

## Tech Stack
Language and Frameworks:
- Java Language
- Spring Framework
- Spring Microservices

Microservices Tools
- Hystrix Dashboard
- Consul Discovery
- Ribbon Load Balancer
- Hystrix Circuit Breaker
- Spring Cloud Gateway
- FeignClient

Client-Side UI:
- Bootstrap 5
- HTML
- CSS

# Application Architecture

## Server Name 👉🏻 config
This is the main server of the microservice project, and it contains and manages the configurations of all the modules.

It connects to the main configuration file located on a remote server - in this project the main configuration file is located on GitHub.

The purpose of this server is to bring the configuration features from the remote server into the local server.

It basically constitutes the configuration file on the local server.

The information found in the remote configuration file can be updated from time to time, in such a situation, Config Server will overwrite the configuration file found on GitHub and then use the updated information locally.

The port of this server is 9999.

This server runs Discovery Client to manage communication between different servers in the application.

## Server Name 👉🏻 service-a
Service A represents a user of type admin.

The port number of this service is 8001.

There is only one instance of this service, therefore it has a fixed port number that we determined in advance.

## Server Name 👉🏻 service-b
Service B represents a customer user, in this system there are many instances of customer type.

The port number of this service is not fixed, no default port number was defined in the configuration file, the port number of each customer will be randomly generated during runtime. Every time a new customer requests access to the system, a new instance will be created, and for each instance a new random port number will be created.

## Server Name 👉🏻 dashboard
In this project I used the Hystrix Dashboard product.

The dashboard server is used as a monitoring tool.

The use of monitor tool is essential when working with microservices, it gives us indicators about the system activities, helps us maintain health checks, monitor loads, it gives us statistical data, checks circuit breaker data and how much load it has, etc.

Definition in the configuration file:
<br/><br/>
![image](https://user-images.githubusercontent.com/60425986/230128101-c55d9e2b-c345-4bd5-9810-a458793f94d3.png)

Enter to get access to the monitoring tool:
<br/><br/>
![image](https://user-images.githubusercontent.com/60425986/230128190-38473b79-3bfb-4c76-b8fe-d5a3d26197ae.png)

Using the monitor tools while running the servers:
<br/><br/>
![image](https://user-images.githubusercontent.com/60425986/230128270-d46b38a6-3852-4b89-b3c0-726cf5fc004d.png)

## Server Name 👉🏻 gateway
In this project I used the Spring Cloud Gateway product.

The API Gateway serves as a reverse proxy to accept API calls from the client application, forwarding this traffic to the appropriate service.

It acts like a Router; it holds all the endpoints and forwards to the right server to perform.

I also used FeignClient to consume RESTFul API endpoints exposed by other microservice in the system.

# How do the microservices within the project know how to communicate with each other?
Discovery
In this project I used the Consul Discovery product.

Discovery is the tool that helps servers communicate with each other.

The discovery maintains a list of all the instances that are currently available, "on the air", and it knows whether it is possible to contact them, and what their specific port is.

The discovery is listening on port 8500, it is waiting for servers to be registered.

Each one of those registered servers is named Client Discovery.

It maintains a list named Registry that contains all the available servers.

It constantly checks whether the instances registered are available, if there is a server that is unavailable or is not found for any reason, it removes it from the registry list.

# Load Balancer
In this project I used the Ribbon Load Balancer product.

Load balancing is the method of distributing network traffic equally across a pool of resources that support an application. 

It distributes the load between the servers and ensuring that all resource servers are used equally.

It works in such a way that prevents a load on a specific server.

# Circuit Breaker
In this project I used the Hystrix Circuit Breaker product.

It is designed to check whether the servers are available for use, it verifies that communication between servers can continue.

In normal condition - the microservice works and runs in a closed circuit. But if one of the servers crashed, and can no longer communicate, the circuit will open.

The circuit breaker allows microservices to communicate as usual and monitor the number of failures occurring within the defined time period. If the failure count exceeds the specified threshold value, the circuit breaker will move to the Open state. If not, it will reset the failure count and timeout period.

<br/>
Thanks for reading,
<br/>
Chelly 👩🏻‍💻












