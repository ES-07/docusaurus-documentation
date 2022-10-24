---
sidebar_label: 'Project Presentation'
sidebar_position: 1
---

# Human Detection in CCTV Systems

## Group Assignment Project


This project will tackle the development of a software solution for a security company named
SecCom. SecCom is a company that ensures critical buildings are not broken into, through the
installation and operation of CCTV cameras on-premises.
Although, SecCom is still not foresting the technological advancements in the security
monitoring field, having several people monitoring the cameras of the most critical buildings.
The goal of your team is to help SecCom with their transition to the digital world, creating an
automatic system that can identify intruders without human-intervention and act accordingly.
With their digital transition, SecCom will also install several light and sound alarms on the spaces
they are protecting and wishes for them to be automatically activated every time an intruder is
detected. Besides this, SecCom also expects that your team develops a top-to-bottom solution they
can use manage the cameras and alarms installed on-premises and to manage all their clients and
buildings monitored.

**Main Goals:**

- The CCTV cameras will be continuously recording video and sending frames to the “Human Detection Module” in order to evaluate if there is a human on-premises or not;
- If the “Human Detection Module” detects a human in 3 consecutive frames, shouldbe  assumed that there is an intruder on-site;
- In case an intruder is detected, the software solution should persist the camera recording. To do so, the solution will have to query the camera and request a portion of the recording, starting 3 minutes before the intrusion and ending 3 minutes after the intrusion is detected.
- The video clip should be stored in a file archival solution;
- If an intrusion is detected, the light and sound alarms should be automatically triggered;
- The solution should provide a portal to manage all buildings being monitored, register new cameras and alarms and manage them;
- The solution should also provide a client-targeted portal to obtain data from the cameras and alarms, manage how the client wishes to receive intrusion notifications, and check all events triggered in the client’s building;
- The access to these portals should be mediated through an Identity Provider mechanism, for user authentication and authorization. Use RBAC and a widely known protocol for authentication and authorization;
- The previous web-portals and the IDP should be accessible through an API Gateway;

## Architecture

![Architecture](../static/img/architecture.png)

### **Cameras**

Responsible for sending the video frames to the message queue so it can be consumed by the Human Detection Module. It should receive requests from the Intrusion Management API to send the video clips of a detected intrusion.

Technologies used: Python

### **Message Broker**

The message queue is responsible for asynchronous communication between some microservices in this project.
Exchanges between the Cameras and HDM, HDM and Intrusion Management API, Intrusion Management API and Cameras.

Technologies used: RabbitMQ

### **Human Detection Module**

This module analyzes the frames sent by the security cameras, to detect if there are humans on-site or not. It receives the camera frames from the message broker and uses machine learning to detect intrusions. When an intrusion is detected, the human detection module publishes a message to the message broker so it can be consumed by the intrusion API. This module also has a Redis in-memory database responsible for temporary storage of each frame (number of the frame, number of detected humans, timestamp, camera identifier, etc.).

The HDM is automatically scalable on demand using AWS Elastic Container Service, meaning the resources are scaled to handle the required capacity.

Technologies used: Python, Redis

### **Intrusion Management API**

This API will be used to act whenever an intrusion is detected. It will get the intrusion video clips from the cameras, activate the alarms, and trigger a new notification in the Notifications API. The requested video clips of the intrusions are stored in a AWS S3 database. 

Technologies used: FastAPI, Docker, AWS S3

### **Sites Management API**

This API should be used to track all properties being monitored, along with all the logic regarding the “owners” of each property. It should make available endpoints for the creation/update/deletion of new properties, creation/update/deletion of new property owners, creation/update/deletion of new cameras/sensors and the creation of new intrusions (timestamp, number of detected humans, building/camera identifier, etc.).

This microservice contains a centralized relational database in PostgreSQL responsible for storing all the information of the entities described above in the endpoints last paragraph.

Technologies used: FastAPI, Docker, PostgreSQL

### **Notifications API**

This API is responsible for informing the property owners and the police whenever an intrusion is detected, which is sent by the Intrusion Management API. The notification can be done via *email* or via telephone message. 

Technologies used: FastAPI, Docker

### **Management Web UI**

Via this graphical interface, the platform’s admins should be able to see all properties being monitored, the intrusions that took place, a list of each property cameras and sensors (also their health), and all data regarding the platform’s clients. Basically, this UI is used to manage and supervise the entire platform.

Technologies used: Angular, Docker

### **Client's Web UI**

This UI is solely offered to the owners of the properties. Through it, the property owners should be able to see a listing of all cameras, sensors, intrusion events and other information related to their buildings. Besides this, the property owners should be able to update their information through this UI.

Technologies used: Angular, Docker

### **Service Discovery**

Every time a new camera or sensor is added to a property, the camera/sensor should register itself in the Service Registry, listing how it can be accessed. New devices information should be stored in the Sites Management API centralized database.

Technologies used: AWS Cloud Map

### **IDP**

The IDP provides authentication and authorization mechanisms for all the aforementioned APIs and UIs. A non-authenticated user should not be able to perform operations in the entire platform.

Technologies used: Keycloak

### **Logs Monitor**

All system logs should be centralized in this entity.

Technologies used: ELK Stack

### **Metrics Monitor**

All system metrics should be centralized in this entity.

Technologies used: Prometheus + Grafana

Group 007<br/> 
Software Engineering
