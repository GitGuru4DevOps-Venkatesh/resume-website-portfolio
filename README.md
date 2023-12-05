# Portfolio Responsive Resume
## [Watch it on youtube--->    ]
### Portfolio Responsive Website Resume

- Responsive Personal Portfolio Website HTML CSS & JavaScript.
- Contains animations when scrolling.
- Smooth scrolling in each section.
- Developed first website to run with the AWS server using Dockerfile.
- Compatible with all mobile devices and with a beautiful and pleasant user interface.

💙 Join the channel to see more videos like this. [DigitalConnectsHub.](https://www.youtube.com/@TheDigitalConnectsHub.blogspot))

**How to use this as website using Docker in AWS-Instance**
**Follow the below steps**

The image you sent shows a screenshot of a GitHub repository called `responsive-portfolio`. The repository contains the following files:

* assets/
* README.md
* index.html
* preview.png

To deploy these files using Docker, you will need to create a Dockerfile. The Dockerfile is a text file that contains instructions for building a Docker image. The following is a simple Dockerfile for deploying a static website:

```dockerfile
FROM nginx:latest

COPY . /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

This Dockerfile copies all of the files from the current directory into the `/usr/share/nginx/html` directory in the Docker image. It then exposes port 80, which is the port that Nginx uses to serve web pages. Finally, it sets the command for the container to `nginx -g daemon off;`. This command tells Nginx to run in the foreground mode so that it does not exit when the container stops.

To build the Docker image, run the following command:

```
docker build -t responsive-portfolio .
```

This will build a Docker image with the tag `responsive-portfolio`.

To deploy the Docker image, run the following command:

```
docker run -d -p 80:80 responsive-portfolio
```

This will start a Docker container running the Nginx image. The `-d` flag tells Docker to run the container in the background mode. The `-p 80:80` flag maps port 80 on the host machine to port 80 in the Docker container.

Once the container is running, you can access the website at `http://localhost:80`.

You can also use Docker Compose to deploy your application. Docker Compose is a tool that allows you to define and manage multiple Docker containers in a single configuration file. The following is a simple Docker Compose file for deploying the `responsive-portfolio` application:

```yaml
version: "3.9"

services:
  web:
    build: .
    image: responsive-portfolio
    ports:
      - "80:80"
```

This Docker Compose file defines a single service called `web`. The `build` directive tells Docker Compose to build the Docker image from the current directory. The `image` directive tells Docker Compose to use the `responsive-portfolio` Docker image. The `ports` directive maps port 80 on the host machine to port 80 in the Docker container.

To deploy the application using Docker Compose, run the following command:

```
docker-compose up -d
```

This will start the Docker Compose stack and deploy the `web` service.

Once the stack is running, you can access the website at `http://localhost:80`.

Which method you choose to deploy your application will depend on your specific needs. If you are only deploying a single container, then you can use the `docker run` command. If you are deploying multiple containers, or if you want to use a more advanced deployment configuration, then you can use Docker Compose.

------------------------------------------------------------------End of the above project steps--------------------------------------------------------

Let's go through the process assuming you want to set up and deploy this project on a server using Docker and Kubernetes. Keep in mind that the provided steps are generic, and you may need to adapt them based on the specific requirements and structure of the repository.

Certainly, let's break it down into clear steps for setting up Docker and Kubernetes on an AWS Ubuntu server:

### 1. **AWS Setup:**

   - Launch an EC2 instance with Ubuntu.
   - Configure security groups to allow SSH (port 22) and any other ports your application needs.

### 2. **Connect to your Instance:**

   ```bash
   ssh -i your-key.pem ubuntu@your-instance-ip
   ```

### 3. **Install Docker:**

   ```bash
   sudo apt update
   sudo apt install docker.io
   sudo systemctl start docker
   sudo systemctl enable docker
   ```

### 4. **Install Kubernetes:**

   ```bash
   sudo apt-get update && sudo apt-get install -y apt-transport-https curl
   curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
   sudo apt-get update
   sudo apt-get install -y kubeadm kubelet kubectl
   ```

### 5. **Initialize Kubernetes Cluster:**

   ```bash
   sudo kubeadm init --pod-network-cidr=192.168.0.0/16
   ```

   Follow the instructions provided by the `kubeadm init` command.

### 6. **Set Up kubectl for Your User:**

   ```bash
   mkdir -p $HOME/.kube
   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   sudo chown $(id -u):$(id -g) $HOME/.kube/config
   ```

### 7. **Install Pod Network (Calico):**

   ```bash
   kubectl apply -f https://docs.projectcalico.org/v3.18/manifests/calico.yaml
   ```

### 8. **(Optional) Join Worker Nodes:**

   If you have additional nodes, use the `kubeadm join` command provided after the `kubeadm init` on the master node.

### 9. **Deploy Your Application:**

   Create and apply Kubernetes manifests (YAML files) for your application.Wait for the external IP to be assigned:

   ```bash
   kubectl get svc -o wide
   ```

   Access your application using the external IP.

### 11. **Additional Considerations:**

### Prerequisites:

1. Ensure you have Docker and Kubernetes installed on your server (follow the steps mentioned in the previous responses).
2. Make sure your AWS instance is running and accessible.

### Steps:

1. **Clone the Repository:**

    ```bash
    git clone https://github.com/GitGuru4DevOps-Venkatesh/resume-website-portfolio.git
    ```

2. **Navigate to the Project:**

    ```bash
    cd resume-website-portfolio
    ```

3. **Build and Run the Docker Container Locally (Optional):**

    - Review the Dockerfile in the project to understand the build process.
    - Build the Docker image:

        ```bash
        docker build -t resume-website .
        ```

    - Run the Docker container locally:

        ```bash
        docker run -p 8080:80 resume-website
        ```

    Access the website locally at http://localhost:8080.

4. **Prepare Kubernetes Manifests:**

    - Create Kubernetes manifests for your application. This involves defining Deployments, Services, and possibly ConfigMaps or Secrets.
    - Here's a basic example:

        ```yaml
        # deployment.yaml
        apiVersion: apps/v1
        kind: Deployment
        metadata:
          name: resume-website
        spec:
          replicas: 1
          selector:
            matchLabels:
              app: resume-website
          template:
            metadata:
              labels:
                app: resume-website
            spec:
              containers:
                - name: resume-website
                  image: your-docker-username/resume-website:latest
                  ports:
                    - containerPort: 80
        ```

        ```yaml
        # service.yaml
        apiVersion: v1
        kind: Service
        metadata:
          name: resume-website
        spec:
          selector:
            app: resume-website
          ports:
            - protocol: TCP
              port: 80
              targetPort: 80
          type: LoadBalancer
        ```

5. **Deploy to Kubernetes:**

    Apply the Kubernetes manifests:

    ```bash
    kubectl apply -f deployment.yaml
    kubectl apply -f service.yaml
    ```

6. **Access the Website:**

    Get the external IP of the service:

    ```bash
    kubectl get svc resume-website
    ```

    Access the website using the external IP.

7. **Additional Considerations:**

    - Configure any environment-specific settings (e.g., database connection strings) either through ConfigMaps or environment variables.
    - Implement persistent storage if needed.
  If any issue:
Great! If your website is already running in Docker on your AWS EC2 instance, the next steps involve setting up Kubernetes to manage and orchestrate your containers. Here's a summary of the steps you need to follow:

### Prerequisites:
- Docker is installed and your website is running in a Docker container.
- AWS EC2 instance is running and accessible.
- SSH access to your EC2 instance.

### Steps:

1. **Install Kubernetes:**
    ```bash
    sudo apt-get update && sudo apt-get install -y apt-transport-https curl
    curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
    echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
    sudo apt-get update
    sudo apt-get install -y kubeadm kubelet kubectl
    ```

2. **Initialize Kubernetes Cluster:**
    ```bash
    sudo kubeadm init --pod-network-cidr=192.168.0.0/16
    ```

    Follow the instructions provided by the `kubeadm init` command.

3. **Set Up `kubectl` for Your User:**
    ```bash
    mkdir -p $HOME/.kube
    sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
    sudo chown $(id -u):$(id -g) $HOME/.kube/config
    ```

4. **Install Pod Network (Calico):**
    ```bash
    kubectl apply -f https://docs.projectcalico.org/v3.18/manifests/calico.yaml
    ```

5. **Deploy Your Application:**
    - Clone your GitHub repository:
        ```bash
        git clone https://github.com/GitGuru4DevOps-Venkatesh/resume-website-portfolio.git
        cd resume-website-portfolio
        ```

    - Create Kubernetes manifests (YAML files) for your application. An example is provided in your previous message.

    - Apply the Kubernetes manifests:
        ```bash
        kubectl apply -f deployment.yaml
        kubectl apply -f service.yaml
        ```

    - Check the status and wait for the external IP to be assigned:
        ```bash
        kubectl get svc -o wide
        ```

6. **Access Your Application:**
    Once an external IP is assigned to your service, access your application using that IP.

### Troubleshooting Tips:
- If there are issues with the Kubernetes components, check the logs:
    ```bash
    journalctl -xeu kubelet
    ```

- If the external IP is not getting assigned, check for any events:
    ```bash
    kubectl get events
    ```

Make sure to replace placeholder values in the example YAML files (like `your-docker-username`, `latest`, etc.) with your actual values.

If you encounter any issues or have specific error messages, feel free to share them, and I'll assist you further.

It looks like your Kubernetes cluster is up and running, and the `kubectl get svc` command shows the `kubernetes` service, which is the default service created by Kubernetes. However, it seems that you are missing the service for your application (`resume-website`).

Let's troubleshoot the issue and make sure your service is correctly deployed:

1. **Check Deployments:**
   Verify that your deployment is running:

   ```bash
   kubectl get deployments
   ```

   Ensure that you see your `resume-website` deployment and that the desired and current replicas are both 1.

2. **Check Pods:**
   Verify that your pods are running:

   ```bash
   kubectl get pods
   ```

   Ensure that you see your `resume-website` pod and that it's in the "Running" state.

3. **Check Services:**
   Verify that your service is created:

   ```bash
   kubectl get services
   ```

   Ensure that you see your `resume-website` service and that it has an external IP.

4. **Check Service Details:**
   Get more details about your service, including the external IP:

   ```bash
   kubectl get svc resume-website -o wide
   ```

   Verify that the service has been assigned an external IP. If not, it might still be pending. Wait a few minutes and check again.

5. **Check Events:**
   Check for any events related to your service or deployment:

   ```bash
   kubectl get events
   ```

   Look for any error messages or events that might indicate issues.

If the external IP is still not assigned to your service, it's possible that there are issues with the networking configuration or the cloud provider's load balancer setup. Verify that your AWS instance's security group allows traffic on the required ports.

If you encounter any specific error messages or issues during these steps, please share them, and I'll do my best to assist you further.

Remember, these are general steps, and your project structure might require additional configurations or modifications. Review the documentation and source code of the project for any specific setup instructions or dependencies. If you encounter any issues or have specific questions about the project, feel free to ask!
