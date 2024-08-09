# Yolo Project Explanation

## Project Overview

The Yolo project is a full-stack e-commerce application built using Node.js, Express, and MongoDB. It features a robust API for handling various e-commerce functionalities like user management, product handling, and order processing. The application is containerized using Docker and orchestrated with Docker Compose, allowing for easy deployment and scaling.

## Key Features

-   **User Management**: Registration, login, and profile management.
-   **Product Management**: CRUD operations for products.
		- CRUD operations refer to the basic functions required to manage data in most applications. Here's what each part stands for:
            -   **Create**: Adding new products to the database.
            -   **Read**: Retrieving product information from the database (e.g., listing all products or viewing details of a specific product).
            -   **Update**: Modifying existing product information (e.g., changing price, name, or description).
            -   **Delete**: Removing a product from the database.
        These operations allow users to manage the product lifecycle in the application.
-   **Order Management**: Shopping cart, order creation, and payment processing.
-   **Authentication**: Secure user authentication using JWT.
- Secure user authentication using JWT (JSON Web Tokens) is a method to verify the identity of users. Here's how it works:
	
	1  **Login**: A user provides their credentials (e.g., username and password).
	2.  **Token Generation**: If the credentials are correct, the server generates a JWT, which contains encoded user information and a digital signature to ensure it hasn’t been tampered with.
	3.  **Token Usage**: The client stores this token (usually in local storage or cookies) and includes it in the header of future requests to access protected resources.
	4.  **Verification**: The server verifies the JWT on each request to confirm the user's identity.

	JWTs provide a stateless, secure way to handle authentication in web applications.
-   **Responsive UI**: Built with modern front-end technologies.

## Architecture

The application follows a microservices architecture, with separate services for the backend (Node.js and Express) and frontend (React.js). The backend handles API requests and data management, while the frontend provides a seamless user experience.

### Folder Structure

-   **backend/**: Contains the server-side code for API endpoints.
-   **client/**: Houses the front-end code for the user interface.
-   **docker/**: Docker configuration files for containerization.
-   **roles/**: Ansible roles for provisioning.
- **Dockerfile**: Instructions for building Docker images.
-   **docker-compose.yml**: Defines services, networks, and volumes for multi-container deployment.
-   **Vagrantfile**: Configuration for setting up a development environment with Vagrant.

## Technologies Used

-   **Backend**: Node.js, Express.js
-   **Database**: MongoDB
-   **Frontend**: React.js
-   **Containerization**: Docker, Docker Compose
-   **Orchestration**: Vagrant, Ansible
-   **Provisioning**: Vagrant File and Ansible for environment setup
-   **Deployment**: Docker Compose for multi-container deployment

## Installation and Setup

### Method 1 (Without Cloning)

1.  Create a `docker-compose.yaml` file in your local directory.
2.  Copy the contents of the provided `docker-compose.yaml` and paste them into your file.
3.  Run the application:
    
    bash
    
    Copy code
    
    `docker compose up` 
    

### Method 2 (With Cloning)

-   **Clone the repository**:
    
    bash
    
    Copy code
    
    `git clone https://github.com/ndegwa-abigael/yolo.git
    cd yolo` 
    
-   **Install dependencies** for both frontend and backend:
    
    bash
    
    Copy code
    
    `cd client && npm install && npm start
    cd ../backend && npm install && npm start` 
    
-   **Run the application** with Docker Compose:
    
    bash
    
    Copy code
    
    `docker-compose up`
    

Access the application at `http://localhost:3000`.

## How to Stop and Terminate the Application

-   Stop the application: Press `ctrl+c` in the terminal.
-   Terminate completely:
    
    bash
    
    Copy code
    
    `docker compose down` 
    
## Orchestration with Docker and Vagrant

The application is fully containerized using Docker, with services defined in `docker-compose.yml` for easy management. Vagrant is used alongside Ansible to automate the provisioning of development environments.

## Contributing

Contributions are welcome! Fork the repository and submit a pull request.

## License

This project is licensed under the MIT License.

## Contact

For any questions, please reach out to https://github.com/ndegwa-abigael


> Written with [StackEdit](https://stackedit.io/).