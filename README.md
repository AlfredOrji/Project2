Kubernetes Deployment Guide

This repository contains instructions for deploying and managing a sample application using Kubernetes. The application includes a Node.js backend, an NGINX frontend, and a MongoDB database. The setup is done using Minikube for local development.

Step 1: Setup the Kubernetes Environment

1. Start Minikube:
   - Set up Minikube with sufficient resources.
   - Verify that `kubectl` is configured correctly.

2. Create a Namespace:
   
   kubectl create namespace fullstack-app

Step 2: Deployment

1. **Apply Configurations:**
   - Apply the MongoDB configurations:
     
     kubectl apply -f mongo-pv.yaml -n fullstack-app
     kubectl apply -f mongo-pvc.yaml -n fullstack-app
     kubectl apply -f mongo-secret.yaml -n fullstack-app
     kubectl apply -f mongo-deployment.yaml -n fullstack-app
     kubectl apply -f mongo-service.yaml -n fullstack-app
     

   - Apply the Node.js configurations:
     
     kubectl apply -f nodejs-configmap.yaml -n fullstack-app
     kubectl apply -f nodejs-deployment.yaml -n fullstack-app
     kubectl apply -f nodejs-service.yaml -n fullstack-app
     

   - Apply the NGINX configurations:
     
     kubectl apply -f nginx-configmap.yaml -n fullstack-app
     kubectl apply -f nginx-deployment.yaml -n fullstack-app
     kubectl apply -f nginx-service.yaml -n fullstack-app
     

Step 3: Application Management

1. Scaling:
   ```sh
   kubectl scale deployment nginx-app --replicas=4 -n fullstack-app
   kubectl scale deployment nodejs-app --replicas=4 -n fullstack-app
   ```

2. Monitoring:
   - Monitor logs:
     ```sh
     kubectl logs <pod-name> -n fullstack-app
     ```
   - Describe and inspect resources:
     ```sh
     kubectl describe pod <pod-name> -n fullstack-app
     ```

3. Port Forwarding:

   kubectl port-forward svc/nginx-svc 8080:80 -n fullstack-app
   

4. Interacting with MongoDB:
   - Connect to MongoDB using the Mongo shell for data management.

5. Rolling Updates:
   - Perform rolling updates to simulate application updates with zero downtime.

Step 4: Testing and Validation

1. Access the Application:
   - Use the NodePort service to access the frontend:
   curl http://localhost:8080

2. Verify Data Persistence:
   - Restart the MongoDB Pod and check data persistence.

3. Environment Variable Verification:
   - Ensure environment variables are correctly set from ConfigMaps.

4. Load Testing:
   - Perform load testing using Apache Benchmark:
     ab -n 1000 -c 10 http://localhost:8080
