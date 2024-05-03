# IAM - ONE Record Workshop

Welcome to the IAM ONE Record Workshop, in this document you will find all the instructions to run a NE:ONE Server and a NE:ONE Play instance on your personal computer.

## Key ONE Record Resources

Familiarize yourself with the key ONE Record resources:
- [Data Model and Ontology Visualizer](https://aloccid-iata.github.io/ontology_visualizer/)

- [API Specification and Security](https://iata-cargo.github.io/ONE-Record/)

- [Official ONE Record Repository](https://github.com/IATA-Cargo/ONE-Record)


## Overview of services

The following services will be created in your local environment:

| Name | Description | Base URL / Admin UI |
|-|-|-|
| [ne-one server](https://git.openlogisticsfoundation.org/wg-digitalaircargo/ne-one) | Holds the ONE Record data and implements the API specification | http://localhost:8080 |
| [ne-one view](https://git.openlogisticsfoundation.org/wg-digitalaircargo/ne-one-view) | View all logistics objects on the ne-one-server and its data | http://localhost:3000 |
| [ne-one play](https://github.com/alvastein/neoneplay) | Create, view and update linked objects | http://localhost:3001 |
| graphdb | GraphDB database as database backend for ne-one server | http://localhost:7200 |
| keycloak | Identity provider for ne-one server to authenticate ONE Record clients and to obtain tokens for outgoing requests. <br/> **Preconfigured client_id:** neone-client<br/> **Preconfigured client_secret:** lx7ThS5aYggdsMm42BP3wMrVqKm9WpNY  | http://localhost:8989 <br/> (username/password: admin/admin)|


# Step by Step Instructions


## 1. Download and install these apps

1. Download and install [Docker](https://docs.docker.com/get-docker/). Setting up an account is not required.

2. For Windows and some Linux computers: download and install [Git](https://git-scm.com/downloads). Setting up an account is not required. Git is installed by default on latest versions of Mac OSX.

3. Download, install [Postman](https://www.postman.com/downloads/) and create a free user account.


## 2. Download the repository and start all services

1. Clone this repository by running the following command on a terminal window, in a folder of your choice:
   ```bash
   git clone https://github.com/alvastein/one-record-workshop.git
   ```
2. On the terminal, switch to the directory to docker-compose:
   ```bash
   cd one-record-workshop/docker-compose
   ```
3. On the terminal, start all services with the following command:
   ```bash
   docker compose up -d
   ```
4. Wait until all containers are up and running:
   ```bash
   [+] Running 6/6
    ✔ Network docker-compose_default            Created 0.0s 
    ✔ Container docker-compose-graph-db-1       Healthy 0.0s 
    ✔ Container docker-compose-keycloak-1       Healthy 0.0s 
    ✔ Container docker-compose-ne-one-server-1  Started 0.0s 
    ✔ Container docker-compose-graph-db-setup-1 Started 0.0s
   ```
2. Try to access the ONE Record Server by  http://localhost:8080 using your favorite browser. 
   You should see a HTTP Error 401 or a blank page, because you did not authenticate yet. This confirms that the ONE Record Server is up and running.


## 3. Use Postman to authenticate and create your first objects with the API

Interacting with the NE:ONE Server, through NE:ONE Play or direct API calls from a tool like Postman, requires an access token generated by a registered Identity Provider Service (IdP). In this case a local Keycloak instance has been set up as the IdP and a Client ID has been created.

We prepared a Postman collection with a few common API calls to get you up and running, including an endpoint to get an access token. Follow these steps:
1. [Download the Postman Collection](./assets/postman/Workshop.postman_collection.json) It will open a new github page, use the download button.

![Download Postman Collection](https://github.com/alvastein/one-record-workshop/assets/168312567/1bb2c3d8-d867-4408-b8a4-6c6702113f29)

2. Open Postman and import the Collection with drag and drop.

![Import Postman Collection](https://github.com/alvastein/one-record-workshop/assets/168312567/fdf9165e-9eea-45f3-b49b-6f9cbdb885cd)

3. Create a new Environment and name it ONE Record

![Create Environment](https://github.com/alvastein/one-record-workshop/assets/168312567/abc2bfcb-1795-4f02-a641-e253358c3687)

4. Create the variables baseUrlKeycloak and baseUrlOneRecord and set their current values to localhost:8989 and localhost:8080 respectively. Click save and choose the ONE Record environment from the dropdow list.

![Create Environment Variables](https://github.com/alvastein/one-record-workshop/assets/168312567/8cb080f3-c7ec-464b-9002-240f657d1616)

5. Trigger the Token Request endpoint and copy the access_token from the response.

![Get and copy token](https://github.com/alvastein/one-record-workshop/assets/168312567/0a65be1d-b068-4f8e-8b80-e3c6c4f15910)

6. Go to the parent folder ONE Record, select the Authorization tab, select Bearer Token from the Auth Type dropdown list, and paste the access_token in the token field.

![6 Paste token in folder](https://github.com/alvastein/one-record-workshop/assets/168312567/4c25da31-3ce6-47cc-a208-6661035ba9e9)

7. Run the calls one by one to create the objects. The order is important as each call is connected to the previous one.


## 4. Add the NE:ONE server into NE:ONE Play

1. Connect to NE:ONE Play http://localhost:3001 and click on the setting button

![NE ONE Play Settings](https://github.com/alvastein/one-record-workshop/assets/168312567/acbf2874-06f0-403e-b6d5-914607df0e13)

2. Add your server with these settings
    - Organization Name: <Choose a name (any string is accepted)>
    - Protocol: http
    - Host: localhost:8080  
    - Token : Use the same token generated with the Postman Collection (go to Postman to copy it).
    - Color : pick up a random color

![Create Organization](https://github.com/alvastein/one-record-workshop/assets/168312567/04c07578-c28a-4390-9c53-10056e4be4b3)

Now you can start creating objects using NE:ONE Play. 


## 5. Create your first object and use NE:ONE Play

1. Create your first object by selecting its type and organization from the dropdown lists. Click the plus button to save

![Create Object](https://github.com/alvastein/one-record-workshop/assets/168312567/d9906005-e49e-47d0-9d97-4cbddd86feed)

2. Close the window and click anywhere on the canvas to visualize the object just created

![Object Created](https://github.com/alvastein/one-record-workshop/assets/168312567/de0f7c9c-8f6f-4b3b-9b7b-a5f6468cce4c)

Happy data sharing!
