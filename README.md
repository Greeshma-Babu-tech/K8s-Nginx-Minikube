Kubernetes Project on Minikube: Nginx Deployment
Overview
This project demonstrates how to set up a scalable and highly available Nginx web server using Kubernetes on Minikube. The setup includes a Deployment to manage the Nginx pods and a Service to expose the application.

Pre-requisites
Minikube: Ensure Minikube is installed and running on your local machine. You can follow the official Minikube installation guide to get started.

kubectl: Install kubectl to interact with your Kubernetes cluster. Follow the official kubectl installation guide for instructions.

Docker: Install Docker to build and manage container images. Follow the official Docker installation guide for instructions.

Steps to Set Up the Project
Step 1: Start Minikube
Start Minikube to create a local Kubernetes cluster:

bash
minikube start
Step 2: Create the Deployment
Create a file named nginx-deployment.yaml with the following content:

yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80
Apply the deployment:

bash
kubectl apply -f nginx-deployment.yaml
Step 3: Verify the Deployment
Check the status of the deployment and pods:

bash
kubectl get deployments
kubectl get pods
Step 4: Create the Service
Create a file named nginx-service.yaml with the following content:

yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: NodePort
Apply the service:

bash
kubectl apply -f nginx-service.yaml
Step 5: Verify the Service
Check the status of the service:

bash
kubectl get services
Note the NodePort assigned to the service.

Step 6: Access the Application
Access the Nginx application using Minikube's IP address and the assigned NodePort:

bash
minikube ip
Open a web browser and go to http://<Minikube_IP>:<NodePort> to see the Nginx welcome page.

Conclusion
By following these steps, you have successfully set up and deployed an Nginx web server on a Kubernetes cluster using Minikube. This setup demonstrates how to manage and expose applications in a Kubernetes environment.
