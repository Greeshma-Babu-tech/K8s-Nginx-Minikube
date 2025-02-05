<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>
  <h1>Kubernetes Project on Minikube: Nginx Deployment</h1>
  <p>This project demonstrates how to set up a scalable and highly available Nginx web server using Kubernetes on Minikube. The setup includes a Deployment to manage the Nginx pods and a Service to expose the application.</p>
  
  <h2>Pre-requisites</h2>
  <ul>
    <li><strong>Minikube</strong>: Ensure Minikube is installed and running on your local machine. You can follow the official <a href="https://minikube.sigs.k8s.io/docs/start/">Minikube installation guide</a> to get started.</li>
    <li><strong>kubectl</strong>: Install <code>kubectl</code> to interact with your Kubernetes cluster. Follow the official <a href="https://kubernetes.io/docs/tasks/tools/install-kubectl/">kubectl installation guide</a> for instructions.</li>
    <li><strong>Docker</strong>: Install Docker to build and manage container images. Follow the official <a href="https://docs.docker.com/get-docker/">Docker installation guide</a> for instructions.</li>
  </ul>

  <h2>Steps to Set Up the Project</h2>
  
  <h3>Step 1: Start Minikube</h3>
  <p>Start Minikube to create a local Kubernetes cluster:</p>
  <pre><code>minikube start</code></pre>

  <h3>Step 2: Create the Deployment</h3>
  <p>Create a file named <code>nginx-deployment.yaml</code> with the following content:</p>
  <pre><code>
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
  </code></pre>
  <p>Apply the deployment:</p>
  <pre><code>kubectl apply -f nginx-deployment.yaml</code></pre>

  <h3>Step 3: Verify the Deployment</h3>
  <p>Check the status of the deployment and pods:</p>
  <pre><code>
  kubectl get deployments
  kubectl get pods
  </code></pre>

  <h3>Step 4: Create the Service</h3>
  <p>Create a file named <code>nginx-service.yaml</code> with the following content:</p>
  <pre><code>
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
  </code></pre>
  <p>Apply the service:</p>
  <pre><code>kubectl apply -f nginx-service.yaml</code></pre>

  <h3>Step 5: Verify the Service</h3>
  <p>Check the status of the service:</p>
  <pre><code>kubectl get services</code></pre>
  <p>Note the <code>NodePort</code> assigned to the service.</p>

  <h3>Step 6: Access the Application</h3>
  <p>Access the Nginx application using Minikube's IP address and the assigned NodePort:</p>
  <pre><code>minikube ip</code></pre>
  <p>Open a web browser and go to <code>http://&lt;Minikube_IP&gt;:&lt;NodePort&gt;</code> to see the Nginx welcome page.</p>

  <p>By following these steps, you have successfully set up and deployed an Nginx web server on a Kubernetes cluster using Minikube. This setup demonstrates how to manage and expose applications in a Kubernetes environment.</p>
</body>
</html>
