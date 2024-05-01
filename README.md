# IAM - ONE Record Workshop

Welcome to the IAM ONE Record Workshop, in this document you will find all the instructions to run a NE:ONE Server and a NE:ONE Play instance on your personal computer.

## Resources
- [ONE Record Data Model](https://github.com/alvastein/one-record-workshop/blob/main/assets/1R%20Data%20Model%20-%20December%202023%20-%203.0.0.pdf)
- [ONE Record API Specification](https://iata-cargo.github.io/ONE-Record/)
- [Ontology web version](https://onerecord.iata.org/ns/cargo/index-en.html)
- [Ontology TTL file](https://github.com/IATA-Cargo/ONE-Record/blob/master/2023-12-standard/Data-Model/IATA-1R-DM-Ontology.ttl) for a better ontology navigation open this file with a tool like Protegé.
- [Official ONE Record Repository](https://github.com/IATA-Cargo/ONE-Record)

## Prerequisites

- Download and install [Docker](https://docs.docker.com/get-docker/). Setting up an account is not required.
- For Windows and some Linux computers: download and install [Git](https://git-scm.com/downloads). Setting up an account is not required. Git is installed by default on latest versions of Mac OSX.
- Download, install [Postman](https://www.postman.com/downloads/) and create a free user account.
- Optional: use a tool like [Protegé](https://protege.stanford.edu/download/protege/4.3/installanywhere/Web_Installers/) to navigate the ontology TTL file.

## Step by step guide

1) Clone this repository by running the following command on a terminal window, in a folder of your choice:
   ```bash
   git clone https://github.com/alvastein/one-record-workshop.git
   ```
2) On the terminal, switch to the directory to docker-compose:
   ```bash
   cd one-record-workshop/docker-compose
   ```
3) On the terminal, start all services with the following command:
   ```bash
   docker compose up -d
   ```
4) Wait until all containers are up and running:
   ```bash
   [+] Running 6/6
    ✔ Network docker-compose_default            Created 0.0s 
    ✔ Container docker-compose-graph-db-1       Healthy 0.0s 
    ✔ Container docker-compose-keycloak-1       Healthy 0.0s 
    ✔ Container docker-compose-ne-one-server-1  Started 0.0s 
    ✔ Container docker-compose-graph-db-setup-1 Started 0.0s
   ```
5) Try to access the ONE Record Server by  http://localhost:8080 using your favorite browser. 
   You should see a HTTP Error 401 or a blank page, because you did not authenticate yet. This confirms that the ONE Record Server is up and running.

# Overview of services

| Name | Description | Base URL / Admin UI |
|-|-|-|
| [ne-one server](https://git.openlogisticsfoundation.org/wg-digitalaircargo/ne-one) | Holds the ONE Record data and implements the API specification | http://localhost:8080 |
| [ne-one view](https://git.openlogisticsfoundation.org/wg-digitalaircargo/ne-one-view) | View all logistics objects on the ne-one-server and its data | http://localhost:3000 |
| [ne-one play](https://github.com/alvastein/neoneplay) | Create, view and update linked objects | http://localhost:3001 |
| graphdb | GraphDB database as database backend for ne-one server | http://localhost:7200 |
| keycloak | Identity provider for ne-one server to authenticate ONE Record clients and to obtain tokens for outgoing requests. <br/> **Preconfigured client_id:** neone-client<br/> **Preconfigured client_secret:** lx7ThS5aYggdsMm42BP3wMrVqKm9WpNY  | http://localhost:8989 <br/> (username/password: admin/admin)|

## Add NE:ONE server into NE:ONE Play

1. Connect to NE:ONE Play http://localhost:3001 

2. Click on the setting button in the top-right corner (cog icon)

3. Add your server following this instruction:

    - Organization Name: <Choose a name (any string is accepted)>
    - Protocol: http
    - Host: localhost:8080  
    - Token : <Use the postman collection to generate a token and copy it here (follow the previous paragraph)>
    - Color : pick up a random color

    ![Image17](./assets/image/neone_setup.PNG)

4. Now you can start using NE:ONE Play.

## Postman Collection

You can add and edit objects directly in NE:ONE Play. You can also trigger the API endpoints with a tool like Postman, and then see the objects in NE:ONE Play.
We prepared a Postman collection with a few common API calls to get you up and running. You will need to install Postman or a compatible software in order to use it.

1. [Download the Postman Collection here.](./assets/postman/Hackathon.postman_collection.json) It will open a new github page, use the download button to get the file

2. [Download the Postman Environment here](./assets/postman/Hackathon.postman_environment.json). It will open a new github page, use the download button to get the file

3. Import the Environment in Postman

![Image9](./assets/image/image9.PNG)

4. Import the Collection in Postman

![Image8](./assets/image/image8.PNG)

5. In the Environments tab, select Workshop environment and set the baseUrlKeyCloak to http://localhost:8989.

![Image10](./assets/image/image10.PNG)

6. Set the baseUrlBooker,baseUrlDestinationAgent and baseUrlOriginAgent to http://localhost:8080.
  Select 

![Image14](./assets/image/image14.PNG)

7. Select Collections on the right menu and open the Workshop collection already imported

8. Use the Token Request call to generate an access token

![Image16](./assets/image/image16.PNG)

9. Copy the access token (it might be a long string, please copy the full content) in the Authorization tab of the Get ServerInformation and run the call

![Image15](./assets/image/image15.PNG)

10. If everything is setup correctly, you will see the server information of the AWS server

11. Copy the access token in Authentication tab of the Example Workflow folder

Happy data sharing!
