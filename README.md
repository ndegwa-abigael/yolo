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

## Open a new terminal and run the same commands in the backend folder
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
