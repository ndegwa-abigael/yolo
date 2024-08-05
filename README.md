cd # Requirements
Make sure that you have the following installed:
- [node](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-18-04) 
- npm 
- [MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/) and start the mongodb service with `sudo service mongod start`

## Navigate to the Client Folder 
 `cd client`

## Run the folllowing command to install the dependencies 
 `npm install`

## Run the folllowing to start the app
 `npm start`
 
 `cd ../backend`

 `npm install`

 `npm start`

 ### Go ahead a nd add a product (note that the price field only takes a numeric input)

 # Yolomy E-commerce

Welcome to the Yolomy E-commerce website where you get all your client needs satisfied upon the completion of the depolyment of our custom DevOps class assignment.

## Table Of Contents
- [Prerequisites](#prerequisites)
- [Requirements](#Requirements)
- [Getting Started](#getting-started)
- [Create Dockerfiles](#Dockerfiles-client dockerfiles-backend)
- [Create DockerComposeFile](#Docker Compose File)
- [Unit Testing](#unit-testing)
- [Continuous Integration (CI)](#continuous-integration-ci)
- [Communication with Slack](#communication-with-slack)
- [License](#License)

## Prerequisites
Before you begin, make sure you have the following prerequisites:

- Basic understanding of DevOps coursework and classes upto week 5
- Familiarity with version control (Git & GitHub)
- Familirity with Docker concepts: Images , volumes running microservices and containerization.

## Requirements
Make sure that you have the following installed:
- [node](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-18-04) 
- [npm](https://nodejs.org/en/download/package-manager) 
- [MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/) and start the mongodb service with `sudo service mongod start`



## Getting Started
1. Clone the repository to your local machine:

    - Clone with SSH

   ```bash
   git clone git@github.com:ndegwa-abigael/yolo.git
   ```

   - Clone with HTTPS

   ```bash
   git clone https://git@github.com:ndegwa-abigael/yolo.git
   ```
   

2. Change to the project directory:
 
   ```bash
   cd client/
   ```
    Run the folllowing command to install the dependencies 
   ```bash
   npm install
   ```
    Run the folllowing to start the app
   ```bash
   npm start
   ```
3. Open a new terminal and run the same commands in the backend folder
     ```bash
     `cd ../backend`
     `npm install`
     `npm start`
     ```
## Create Dockerfiles...
    1.Identify Components: List components (e.g., frontend, backend, database).

    2.Create Dockerfiles: For each component, create a Dockerfile with appropriate base images and configurations.
        # Base Image
        FROM node:14-alpine 
        #Container will run from the following location
        WORKDIR /usr/src/app
        #Copy package-lock.json-dependancies
        COPY package*.json ./
        #Run npm Install into the container from the image
        RUN npm install
        #Copy from local directory into what our image should contain
        COPY . .
        #Expose port: 5000 to local host:5000 after npm start command
        EXPOSE 5000
        #Run application
        CMD ["npm", "start"]

## Create Docker Compose File
    1.Networking and Volumes: Define services, networks, and volumes in docker-compose.yml.
              Networking and Volumes: Define services, networks, and volumes in docker-compose.yml.

         version: '3.8'
         services:
         frontend:
         build: ./frontend
         ports:
             - "3000:3000"
             backend:
             build: ./backend
        ports:
             - "5000:5000"
                depends_on:
             - mongo
                mongo:
             image: mongo
        ports:
             - "27017:27017"
         volumes:
             - mongo-data:/data/db
         volumes:
             mongo-data
##Build and Run Containers
1.Build the containers

        '''docker-compose build
     
2. Run the containers:

        '''docker-compose up

## Push to GitHub
1.Add and commit changes to your repository:

    '''git add .
        '''git commit -m "Containerized application"

2. Push changes to GitHub:

         '''git push origin main
 
## Document and Tag Images
1. Tag Images: Follow naming conventions for Docker image tags.
 
        '''docker build [OPTIONS] <context> [--tag <image:tag>]

 
    2. Push Images to DockerHub:
 
             '''docker push your-dockerhub-username/yolo:latest

## Screenshot and Documentation
1. Take a screenshot of the deployed image on DockerHub.
2. Include the screenshot in your explanation.md.

## Unit Testing
Go ahead and add a product (note that the price field only takes a numeric input)

## Communication with Slack
To receive notifications on Slack, follow these steps:

1. Set up a Slack Incoming Webhook. Refer to the [Slack documentation](https://github.com/marketplace/actions/slack-notify) for instructions.
   
2. Add the Slack Webhook as a secret in your GitHub repository:
   - Go to "Settings" -> "Secrets" -> "New repository secret"
   - Name: `SLACK_WEBHOOK`
   - Value: [Your Slack Webhook URL]

Now, when the CI workflow runs, it will send notifications to the configured Slack channel.



## Contributing
We encourage contributions! If you have suggestions, enhancements, or bug fixes, please [submit a pull request](https://github.com/ndegwa-abigael/pulls).


## License
This project is licensed under the [MIT License](./LICENSE).
