# Portfolio Responsive Complete
## [Watch it on youtube]
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
