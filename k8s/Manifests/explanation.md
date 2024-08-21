
# Using Google Cloud GKE to Deploy the Yolomy eCommerce Website
This document explains the reasoning behind the technology choices made for deploying the Yolomy E-commerce application on Google Kubernetes Engine (GKE).

### Technology Choices

-   **Kubernetes:** Kubernetes is chosen as the container orchestration platform due to its several advantages:
    
    -   **Scalability:** Kubernetes allows easy scaling of applications by automatically provisioning and managing additional pods based on resource needs.
    -   **High Availability:** Kubernetes ensures high availability by automatically restarting failed pods and replicating them across nodes.
    -   **Self-Healing:** It facilitates self-healing by automatically scheduling pods on healthy nodes if a node fails.
    -   **Load Balancing:** Kubernetes offers built-in load balancing mechanisms to distribute traffic across multiple pods.
    -   **Declarative Management:** Applications are defined declaratively using manifests (YAML files), simplifying configuration and management.
-   **Docker:** Docker containers are chosen to package the application components (backend and frontend) for the following reasons:
    
    -   **Isolation:** Containers provide isolation between applications, preventing conflicts and ensuring consistent behavior.
    -   **Portability:** Docker containers are portable across different environments as long as they have a Docker runtime installed.
    -   **Reproducibility:** Docker images guarantee a consistent environment for the application across deployments.
-   **StatefulSets (Optional):** For the database (MongoDB), using a StatefulSet is recommended for the following benefits:
    
    -   **Persistent Storage:** StatefulSets ensure persistent storage for the database data by leveraging Persistent Volumes (PVs) and Persistent Volume Claims (PVCs).
    -   **Ordered Deployment:** StatefulSets guarantee a specific order of deployment for pods, which is crucial for ensuring the database pod comes online before application pods.
    -   **Pod Identity:** StatefulSets maintain a unique identity for each pod, allowing applications to connect to the same database instance consistently.
-   **Persistent Volumes (Optional):** Persistent Volumes (PVs) and Persistent Volume Claims (PVCs) are recommended for storing database data, providing:
    
    -   **Data Persistence:** Data persists across pod restarts or failures, ensuring data availability.
    -   **Decoupling:** Applications decouple from the underlying storage infrastructure, simplifying management.
-   **Ingress (Optional):** An Ingress resource is a good option for exposing the application externally, offering:
    
    -   **Load Balancing:** Ingress routes incoming traffic to backend services using load balancing techniques.
    -   **HTTPS Termination:** Ingress can handle SSL/TLS termination at the cluster level, simplifying application configuration.
    **Once you've successfully deployed the Yolomy application on Google Kubernetes Engine (GKE), you can access it using the following methods:**

### 1. **Using the LoadBalancer Service:**

-   If you've configured a LoadBalancer service for your application, you can access it directly using the external IP address provided by Google Cloud.
-   To find the external IP, use the `kubectl get services` command and look for the `EXTERNAL-IP` column.
-   Open your web browser and enter the external IP address in the URL bar.

### 2. **Using NodePort Service:**

-   If you've used a NodePort service, you'll need to access the application through a specific port on one of the GKE cluster nodes.
-   Use the `kubectl get services` command to find the NodePort for your service.
-   To access the application, open your web browser and enter the following URL:
    -   `http://<node-ip>:<node-port>`
    -   Replace `<node-ip>` with the public IP address of a GKE cluster node and `<node-port>` with the NodePort value.

### 3. **Using Ingress:**

-   If you've configured an Ingress resource, you can access the application using the domain name or subdomain associated with the Ingress.
-   To find the domain name or subdomain, use the `kubectl get ingress` command.
-   Open your web browser and enter the domain name or subdomain in the URL bar.



### Justification

These technology choices offer a robust, scalable, and manageable platform for deploying the Yolomy E-commerce application on GKE. Kubernetes provides the orchestration layer, while Docker ensures containerized application delivery. StatefulSets and Persistent Volumes (optional) ensure database persistence and availability. Finally, an Ingress resource (optional) offers a clean approach for external exposure and load balancing.

