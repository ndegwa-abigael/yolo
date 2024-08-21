
## Yolomy E-commerce Website: DevOps Class Assignment

This document outlines the instructions for cloning, testing, and deploying the Yolomy E-commerce website, built as a DevOps class assignment.

### Prerequisites

-   Familiarity with Git (version control) and GitHub
-   Ubuntu 22.04 LTS (or preferred OS) with comfortable command-line usage
-   VS Code for code editing and visualization
### Requirements

-   Node.js and npm installed
-   MongoDB installed and running 
	-  `sudo service mongod start`

### Getting Started

1.  **Clone the Repository:**
    
    -   **SSH:** 
	    - `git clone git@github.com:ndegwa-abigael/yolo.git`
    -   **HTTPS:**
	    -  `git clone https://github.com/ndegwa-abigael/yolo.git`
2.  **Change Directory:**
    
	    -   `cd client/`
3.  **Install Dependencies:**
    
	    -   `npm install`
4.  **Start the Frontend App:**
    
		-  `npm start`
5.  **Open a New Terminal:**
    
6.  **Navigate to Backend Folder:**
    
	    -   `cd ../backend`
7.  **Install Dependencies:**
    
	    -   `npm install`
8.  **Start the Backend App:**
    
	    -   `npm start`

### Unit Testing

-   Add a product to the app (note: price field accepts only numeric values).

### Creating Docker Images

1.  **Create Dockerfiles:**
    
	    -   In the `client` folder:
	        -   `touch Dockerfile`
	    -   In the `backend` folder:
	        -   `touch Dockerfile`
2.  **Build Docker Images:**
    
    -   Open a terminal, navigate to the folder containing the Dockerfile, and run:
        
        Bash
        
	        ```
	        docker build -t docker.io/<username>/<container_name>:<version> .
	        
	        ```
        
        -   Replace `<username>` with your Docker Hub username.
        -   Replace `<container_name>` with a descriptive name for your container (e.g., yolomy-frontend, yolomy-backend).
        -   Replace `<version>` with the version of your image (e.g., v1.0.1).
        -   The `.` at the end specifies the source directory for building the image.
3.  **Create Bridge Network (Optional):**
    
    -   If you don't have one, run:
        
        Bash
        
        ```
        docker network create –driver bridge my_network
        
        ```
        
        -   Replace `my_network` with your preferred network name.
4.  **Run Docker Containers:**
    
    -   Run the Docker container on the bridge network (if created):
        
        Bash
        
        ```
        docker run -d --name yolomy_app --network my_network -p 3000:3000 yolomy:v1.0.1
        
        ```
      
        -   Replace the options with your preferences:
            -   `-d`: Run in detached mode (background).
            -   `--name yolomy_app`: Give the container a name.
            -   `--network my_network`: Connect to the bridge network (if created).
            -   `-p 3000:3000`: Map host port 3000 to container port 3000 (default app port).
            -   `yolomy:v1.0.1`: Specify the image and tag to use.

### Docker Hub Images

1.  **Docker Login:**
    
    -   Open a terminal and run:
        
        Bash
        
        ```
        docker login
        
        ```
       
        
2.  **Check Logged-In User:**
    
    -   Run `docker info` to find your Docker Hub username under the `Username` field.
3.  **Push to Docker Hub:**
    
    -   Push the Docker image to your Docker Hub account:
        
        Bash
        
        ```
        docker push docker.io/<dockerhub_username>/<Image_name>:<version>
        
        ```
   
        -   Replace the placeholders with your information.

### Kubernetes Deployment for Yolomy E-commerce

### Prerequisites

-   A Google Cloud Platform (GCP) account with the necessary permissions.
-   The `gcloud` command-line tool installed and configured.
-   A Docker Hub account with your built Docker images.
-   Basic understanding of Kubernetes concepts (Pods, Deployments, Services, Stateful Sets, Ingress).

### Steps

#### 1. Create a GKE Cluster

-   Use the `gcloud container clusters create` command to create a GKE cluster. Choose a suitable machine type, node count, and zone for your application's requirements.
-   Example:
    
    Bash
    
    ```
    gcloud container clusters create my-cluster --zone us-central1-a
    
    ```
    
#### 2. Configure kubectl

-   Use the `gcloud container clusters get-credentials` command to configure the `kubectl` command-line tool to interact with your cluster.

#### 3. Create Kubernetes Manifests

**Backend Deployment**

YAML

	```
	apiVersion: apps/v1
	kind: Deployment
	metadata:
	  name: yolomy-backend
	spec:
	  replicas: 3 # Adjust based on your requirements
	  selector:
	    matchLabels:
	      app: yolomy-backend
	  template:
	    metadata:
	      labels:
	        app: yolomy-backend
	    spec:
	      containers:
	      - name: yolomy-backend    
	        image: your-dockerhub-username/yolomy-backend:latest
	        ports:
	        - containerPort: 3000



**Frontend Deployment**

YAML

	```
	apiVersion: apps/v1
	kind: Deployment
	metadata:
	  name: yolomy-frontend
	spec:
	  replicas: 3 # Adjust based on your requirements
	  selector:
	    matchLabels:
	      app: yolomy-frontend
	  template:
	    metadata:
	      labels:
	        app: yolomy-frontend
	    spec:
	      containers:
	      - name: yolomy-frontend
	        image: your-dockerhub-username/yolomy-frontend:latest
	        ports:
	        - containerPort: 80


**MongoDB StatefulSet**

YAML

	```
	apiVersion: apps/v1
	kind: StatefulSet
	metadata:
	  name: yolomy-mongodb
	spec:
	  serviceName: yolomy-mongodb
	  replicas: 3 # Adjust based on your requirements
	  selector:
	    matchLabels:
	      app: yolomy-mongodb
	  template:
	    metadata:
	      labels:
	        app: yolomy-mongodb
	    spec:
	      containers:
	      - name: yolomy-mongodb
	        image: mongo:latest
	        ports:
	        - containerPort: 27017
	      volumeMounts:
	      - name: data
	        mountPath: /data/db
	  volumeClaimTemplates:
	  - metadata:
	      name: data
	    spec:
	      accessModes:     [ "ReadWriteOnce" ]
	      resources:
	        requests:
	          storage:     1Gi

	```

**Service for Backend**

YAML

	```
	apiVersion: v1
	kind: Service
	metadata:
	  name: yolomy-backend-service
	spec:
	  selector:
	    app: yolomy-backend
	  ports:
	  - protocol: TCP
	    port: 3000
	    targetPort: 3000

	```

**Service for Frontend**

YAML

	```
	apiVersion: v1
	kind: Service
	metadata:
	  name: yolomy-frontend-service
	spec:
	  selector:
	    app: yolomy-frontend
	  ports:
	  - protocol: TCP
	    port: 80
	    targetPort: 80

	```


**Ingress (Optional)**

Create an Ingress resource to expose your services externally.

#### 4. Apply Manifests

-   Apply the YAML files to your cluster:
   
    Bash
    
    ```
    kubectl apply -f backend-deployment.yaml
    kubectl apply -f frontend-deployment.yaml
    kubectl apply -f mongodb-statefulset.yaml
    kubectl apply -f backend-service.yaml
    kubectl apply -f frontend-service.yaml
    # kubectl apply -f ingress.yaml (if applicable)
    
	    ```

#### 5. Verify Deployment

-   Use `kubectl get pods`, `kubectl get deployments`, and `kubectl get services` to verify the deployment status.

### Environment Variables

Environment variables are a common way to pass configuration information to your application. 

**Steps:**

1.  **Define Environment Variables in Your Deployment Manifest:**
    
    YAML
    
    ```
    env:
    - name: DATABASE_URL
      valueFrom:
        configMapKeyRef:
          name: my-configmap
          key: DATABASE_URL
    
    ```
  
2.  **Create a ConfigMap:**
    
    Bash
    
    ```
    kubectl create configmap my-configmap --from-literal=DATABASE_URL=your_database_url
    
    ```
   

### ConfigMaps and Secrets

ConfigMaps are used for non-sensitive configuration data, while Secrets are for sensitive information like passwords, API keys, and tokens.

**Steps:**

1.  **Create a Secret:**
    
    Bash
    
    ```
    kubectl create secret generic my-secret --from-literal=DATABASE_PASSWORD=your_password
    
    ```
   
2.  **Access Secret in Deployment:**
    
    YAML
    
    ```
    envFrom:
    - secretRef:
        name: my-secret
    
    ```
  

### Persistent Volumes

Persistent Volumes (PVs) and Persistent Volume Claims (PVCs) ensure data persistence across pod restarts or failures.

**Steps:**

1.  **Create a Persistent Volume:**  
		YAML

```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv-volume
spec:
  capacity:
    storage: 1Gi
  accessModes:
  - ReadWriteOnce
  persistentVolumeReclaimer:    1.  medium.com medium.com Recycle
  storageClassName: manual # Choose a storage class if available
```
  
3.  **Create a Persistent Volume Claim:**
    
    YAML
    
    ```
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: my-pvc
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage:    1.  stackoverflow.com stackoverflow.com 1Gi
    
    ```
   
4.  **Mount PVC in Pod:**
    
    YAML
    
    ```
    volumeMounts:
    - name: my-persistent-storage
      mountPath: /data
    volumes:
    - name: my-persistent-storage
      persistentVolumeClaim:
        claimName:    1.  github.com  MIT github.com my-pvc
    
    ```
   
### Load Balancing

Kubernetes offers multiple service types for load balancing.

-   **NodePort:** Exposes service on a static port on each node.
-   **LoadBalancer:** Creates a load balancer in the cloud provider.
-   **Ingress:** Provides HTTP/HTTPS load balancing.

**Example:**

YAML

```
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: LoadBalancer # or NodePort, Ingress
  selector:
    app: my-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080

```

### Monitoring and Logging

Kubernetes provides basic monitoring, but for comprehensive monitoring and logging, use tools like Prometheus, Grafana, and Elasticsearch (ELK Stack).

### Security

-   **Network Policies:** Define network traffic rules between pods.
-   **RBAC:** Control access to Kubernetes resources.
-   **Pod Security Policies (PSP):** Enforce security constraints for pods (deprecated in Kubernetes 1.25).
-   **Secret Management:** Use Secrets for sensitive information.
-   **Image Scanning:** Scan container images for vulnerabilities.
-   **Regular Updates:** Keep Kubernetes components and applications up to date with security patches.

**Example Network Policy:**

YAML

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-ingress
spec:
  podSelector:
    matchLabels:
      app: my-app
  policyTypes:
  - Ingress
  ingress:
  - from:
    - ipBlock:
        cidr: 0.0.0.0/0
```

