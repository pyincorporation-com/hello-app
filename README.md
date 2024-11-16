# Hello-App Deployment Guide

This guide walks you through deploying the "Hello App" on the Namespaxe platform. It covers the steps for deploying the application using the provided YAML configuration files. 

## Prerequisites
- A valid **namespace** in the Namespaxe platform.
- Access to the **deployment YAML**, **service YAML**, and **ingress YAML** files located at `configs/`.

## Steps to Deploy

### 1. **Deploy the Application (Deployment YAML)**
   The first step is to deploy the application using the **deployment.yaml** file. This file defines how the Hello App will be run on Kubernetes, including the container image, replica count, and resource requests.

   - **Action**: On web interface, Copy the file content and paste in text area, then click upload button.

   - **Action**: If your using local terminal with kubectl installed, Run the following command to apply the deployment configuration:
     ```bash
     kubectl apply -f configs/deployment.yaml
     ```

   - **Purpose**: This configuration creates a deployment in your namespace. The platform will automatically handle namespace assignment, so there is no need to manually edit the YAML file to reflect your namespace.

   - **Key Components of `deployment.yaml`**:
     - **replicas**: Defines the number of instances of the Hello App.
     - **containers**: Specifies the container image to use and the ports exposed.
     - **resources**: Defines CPU and memory resource requests/limits.

### 2. **Create the Service (Service YAML)**
   Once the deployment is successful, you need to expose the Hello App using a service. The **service.yaml** file defines how the app will be accessed internally or externally.

   - **Action**: On web interface, Copy the file content and paste in text area, then click upload button.

   - **Action**: If your using local terminal with kubectl installed, Apply the service configuration by running:
     ```bash
     kubectl apply -f configs/service.yaml
     ```

   - **Purpose**: This configuration defines a **Service** that allows communication with the Hello App. It exposes the app’s deployment as a stable endpoint within the Kubernetes cluster.
   
   - **Key Components of `service.yaml`**:
     - **type**: Defines how the service will be exposed (e.g., `ClusterIP`, `NodePort`, or `LoadBalancer`).
     - **ports**: Specifies which ports the service will expose.
     - **selector**: Ensures the service is linked to the correct pods created by the deployment.

### 3. **Create the Ingress (Ingress YAML)**
   The final step is to set up an ingress to route external traffic to the Hello App. The **ingress.yaml** file defines the rules for exposing your service to the outside world, typically via a URL.

   - **Action**: On web interface, Copy the file content and paste in text area, then click upload button.

   - **Action**: If your using local terminal with kubectl installed, Apply the ingress configuration:
     ```bash
     kubectl apply -f configs/ingress.yaml
     ```

   - **Purpose**: This configuration sets up an **Ingress** resource, which allows HTTP(S) traffic to reach your service based on the defined rules (such as hostnames or paths). It is often used in combination with a load balancer or reverse proxy.

   - **Key Components of `ingress.yaml`**:
     - **host**: Specifies the domain or subdomain that will route to the Hello App.
     - **paths**: Defines specific URL paths that map to the service and its exposed ports.
     - **annotations**: Custom configurations for things like SSL termination, ingress controller settings, etc.

## Conclusion
Following these steps will set up a fully functional Hello App on the Namespaxe platform. The deployment will run your application, the service will make it accessible within the cluster, and the ingress will allow external access to the app. 

If you encounter any issues, verify that each YAML file is applied correctly and that the Kubernetes resources are created as expected.
