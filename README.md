Certainly! Here's an updated README file for deploying NGINX as a reverse proxy using Docker:

```
# NGINX Reverse Proxy Deployment with Docker

This repository provides instructions for deploying an NGINX reverse proxy using Docker to route traffic to multiple application containers on an Azure container instance.

## Prerequisites

- Docker: Make sure you have Docker installed on your local machine or the target deployment environment.

## Getting Started

1. Clone this repository to your local machine or the target deployment environment:

   ```bash
   git clone https://github.com/goldenamir/nginx_docker/
   ```

2. Navigate to the cloned repository:

   ```bash
   cd nginx_docker
   ```

3. Customize the NGINX configuration:

   - Open the `nginx.conf` file and modify it to suit your reverse proxy requirements.
   - Add appropriate `proxy_pass` directives for each application container based on your desired routing rules.

4. Build the NGINX Docker image:

   ```bash
   docker build -t nginx-reverse-proxy .
   ```

5. Start the NGINX reverse proxy container:

   ```bash
   docker run -d -p 80:80 --name nginx-proxy nginx-reverse-proxy
   ```

   This command will start the NGINX reverse proxy container and map port 80 of the container to port 80 on the host machine.

6. Update DNS or domain settings:

   - Point the desired subdomains or domains to the public IP of your Azure container instance.
   - Ensure that the DNS or domain settings are properly configured to route traffic to the NGINX reverse proxy.

## NGINX Configuration

The NGINX configuration file `nginx.conf` is located in this repository. You can modify it based on your specific needs. Here's a basic example configuration file:

```nginx
worker_processes auto;
events {}

http {
    server {
        listen 80;
        server_name example.com;

        location /app1 {
            proxy_pass http://app1-container:8001;  # Forward traffic to Docker container for app1
        }

        location /app2 {
            proxy_pass http://app2-container:8002;  # Forward traffic to Docker container for app2
        }

        # Add more location blocks as needed for additional applications
    }
}
```

In the configuration example above, `example.com` is the domain or subdomain pointing to your Azure container instance. Adjust the `proxy_pass` directives and locations to match your application containers' URLs and ports.

## Notes

- Make sure to have the necessary application container images available and running. Replace `app1-container` and `app2-container` in the NGINX configuration with the correct container names or addresses for your application containers.

- Ensure that the NGINX configuration file (`nginx.conf`) is present in the same directory as your Dockerfile before building the NGINX image.

- It is recommended to secure your deployment with appropriate security measures, such as SSL/TLS encryption and authentication, depending on your specific use case.

## Support

If you encounter any issues or have questions, please feel free to reach out to the maintainers of this repository.

Happy coding!
```
