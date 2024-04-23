# Setting Up a Three-Tier Application with Docker

Welcome, tech enthusiasts and Docker adventurers! Today, we embark on an exhilarating journey through the realm of containerization, where we'll Dockerize a magnificent three-tier application. Are you ready to dive into the world of Docker and witness the magic of containerization? Let's get started!

# Part 1: Elevating the Presentation Tier (Front End)

### Crafting a Stunning Frontend Experience

We kickstart our journey by crafting a mesmerizing user interface using the powerful React.js framework. Whether you're a seasoned React developer or a newcomer, fear not! We'll guide you every step of the way.

```tsql
mkdir frontend
cd frontend
npx create-react-app my-app
cd my-app
```

### Enveloping Your Frontend in a Docker Container

But why stop there? Let's encapsulate our frontend masterpiece within a Docker container to ensure seamless deployment and scalability. Behold, the Dockerfile:

```tsql
FROM node:alpine

WORKDIR /app

COPY package.json .
RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

FROM node:alpine: Specifies the base image as Node.js with Alpine Linux.

WORKDIR /app: Sets the working directory inside the container.

COPY package.json .: Copies package.json to the working directory.

RUN npm install: Installs dependencies.

COPY . .: Copies the rest of the application code to the container.

EXPOSE 3000: Exposes port 3000 for the application.

CMD ["npm", "start"]: Specifies the command to run when the container starts.


# Part 2: Orchestrating the Application Tier (Backend)

### Unleashing the Power of Node.js

Our journey continues as we unleash the mighty Node.js for our backend logic. Let your creativity flow as we construct the backbone of our application.

 ```tsql
mkdir backend
cd backend
npm init -y
npm install express pg
 ```

### Encapsulating Backend Brilliance in a Docker Container

Now, it's time to encapsulate our backend brilliance within another Docker container. Witness the power of containerization with our Dockerfile:

 ```tsql
FROM node:alpine

WORKDIR /app

COPY package.json .
RUN npm install

COPY . .

EXPOSE 4000

CMD ["node", "server.js"]


 ```
FROM node:alpine: Uses Node.js with Alpine Linux as the base image.

WORKDIR /app: Sets the working directory inside the container to /app.

COPY package.json .: Copies package.json to the working directory.

RUN npm install: Installs dependencies.

COPY . .: Copies application code to the container.

EXPOSE 4000: Exposes port 4000.

CMD ["node", "server.js"]: Specifies the command to start the application.


# Fortifying the Database Tier

### Building a Robust Data Foundation with PostgreSQL

No application is complete without a sturdy database foundation. Let's fortify our application with the robust PostgreSQL database, encapsulated within a Docker container.

Create a file named Dockerfile in the root directory of your project with the following content:
 ```tsql
FROM postgres:alpine

ENV POSTGRES_DB todo_db
ENV POSTGRES_USER admin
ENV POSTGRES_PASSWORD password
 ```

FROM postgres:alpine: Specifies the base image as PostgreSQL with Alpine Linux. Alpine Linux is a lightweight Linux distribution, making the resulting Docker image smaller.

ENV POSTGRES_DB todo_db: Sets an environment variable POSTGRES_DB to todo_db, which defines the name of the database to be created within PostgreSQL.

ENV POSTGRES_USER admin: Sets an environment variable POSTGRES_USER to admin, which specifies the username for accessing the PostgreSQL database.

ENV POSTGRES_PASSWORD password: Sets an environment variable POSTGRES_PASSWORD to password, which defines the password for the specified username to access the PostgreSQL database.


# Final Act: Orchestration with Docker Compose

### Bringing it All Together

As the curtains draw close, we orchestrate our containers effortlessly with Docker Compose. Behold, the orchestrator of our Docker symphony:

Create a file named docker-compose.yml in the root directory of your project with the following content:
```tsql
version: '3'
services:
  frontend:
    build:
      context: ./frontend
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
  backend:
    build:
      context: ./backend
      dockerfile: Dockerfile
    ports:
      - "4000:4000"
    depends_on:
      - db
  db:
    build:
      context: .
      dockerfile: Dockerfile
    environment:
      POSTGRES_DB: todo_db
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: password
```


Certainly! Here's a concise explanation of the provided Docker Compose file:

yaml
Copy code
version: '3'
services:
  frontend:
    build:
      context: ./frontend
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
  backend:
    build:
      context: ./backend
      dockerfile: Dockerfile
    ports:
      - "4000:4000"
    depends_on:
      - db
  db:
    build:
      context: .
      dockerfile: Dockerfile
    environment:
      POSTGRES_DB: todo_db
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: password
This Docker Compose file orchestrates the setup of multiple Docker containers for a three-tier application:

frontend: Defines a service for the frontend of the application. It builds the frontend Docker image using the Dockerfile located in the ./frontend directory. It also maps port 3000 on the host machine to port 3000 in the container, allowing access to the frontend application.

backend: Defines a service for the backend of the application. Similar to the frontend, it builds the backend Docker image using the Dockerfile located in the ./backend directory. It maps port 4000 on the host machine to port 4000 in the container. Additionally, it specifies that this service depends on the db service.

db: Defines a service for the database tier of the application. It builds the PostgreSQL Docker image using the Dockerfile located in the root directory (where the Docker Compose file is). It sets environment variables POSTGRES_DB, POSTGRES_USER, and POSTGRES_PASSWORD to configure the PostgreSQL database.

# The Grand Finale: Building and Running Docker Containers

```tsql
docker-compose build
docker-compose up
```

# Test and Debug: Your Journey Awaits!

Now, the stage is set, and your Dockerized three-tier application awaits your exploration. So fire up your favorite browser, explore your creation, and embark on a journey of testing and debugging. Fear not, for every challenge is an opportunity to grow!

And there you have it, fellow Docker enthusiasts! You've now Dockerized your three-tier application, unlocking a world of scalability, efficiency, and portability. As you navigate the vast seas of containerization, may your journey be filled with triumphs and discoveries.

Happy coding, and may the Docker gods smile upon you!

![Docker Logo](images/img1.jpg)