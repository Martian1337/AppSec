# Martian's Hands-on AppSec Training Resources


# Self-Hosted Mini AppSec Range (Docker)

## **Prerequisites**

Before running the RedPlanet AppSec Training Range, please ensure the following:

- **Docker is installed and running on your system**  
  - Verify by running:  
    ```bash
    docker --version
    ```
  - Docker Engine version 20.x or newer is recommended.

- **If Docker is not yet installed, please install it following instructions relevant to your OS:**  

  - **Windows and macOS**  
    Download and install Docker Desktop from:  
    [https://docs.docker.com/desktop/install/](https://docs.docker.com/desktop/install/)

  - **Linux (Ubuntu example)**  
    Follow installation steps at:  
    [https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)

  - **Official Docker Hub Quickstart** guide (general overview):  
    [https://docs.docker.com/docker-hub/quickstart/](https://docs.docker.com/docker-hub/quickstart/)

- **System resource requirements:**  
  - Minimum **4 CPU cores**  
  - At least **6 GB of available RAM**  
  - Around **15 GB free disk space** to store images and data

- **Internet connection** is required for the first run to pull the images from Docker Hub.

- **Privilege requirements:**  
  - You must be able to run Docker containers with the `--privileged` flag as the training range uses Docker-in-Docker (DinD).  
  - This typically requires administrative or root permissions on the host system.

- **Security notice:**  
  - This training range contains intentionally vulnerable applications.  
  - It is recommended to run inside isolated lab environments and never expose directly to production networks or the public internet.


### TL;DR - One-line version to pull image and start environment
```bash
sudo docker pull martiandefense/redplanet-appsec:latest && docker run --privileged --name redplanet-appsec-instance \
  -p 8080:8080 -p 9090:9090 \
  -p 8087:3000 \
  -p 8082:8080 -p 8083:8087 -p 8084:8000 \
  -p 8888:80 -p 30080:80 \
  -p 8443:443 -p 30443:443 \
  -p 8025:8025 \
  -p 8085:80 \
  martiandefense/redplanet-appsec:latest
```

#  RedPlanet Appsec Range

A plug-and-play application security mini-range built with Docker Compose, designed for learning, teaching, and testing common web and API vulnerabilities.

## What's Included

This environment includes the following intentionally vulnerable applications and services:

| Service        | Description                                                  | Port(s)                  | URL (s)
|----------------|--------------------------------------------------------------|--------------------------| ---------------------- |
| WebGoat        | Classic OWASP insecure Java app                              | 8080, 9090               | [http://127.0.0.1:8080//WebGoat/login](http://127.0.0.1:8080/WebGoat/login) |
| Juice Shop     | Modern insecure web app with rich OWASP coverage             | 8087                     | [http://localhost:8087](http://localhost:8087)|
| DVWA           | PHP/MariaDB web application                                  | 8085                     | [http://localhost:8085](http://localhost:8085) |
| crAPI          | "Completely Ridiculous API" for API security hands-on labs   | Multiple (8082–8084, 8888, 8443) | [http://localhost:8888](http://localhost:8888) |
| MailHog        | Email testing interface for crAPI mail features              | 8025                     | [http://localhost:8025](http://localhost:8025) |
| ------         |  
| PostgreSQL     | Backend DB for crAPI                                         | Internal                 |
| MongoDB        | NoSQL DB used by crAPI                                       | Internal                 |
| mySQL          | MySQL DB for DVWA                                            | Internal                 |



## Usage

### Step1. Pull the image
```bash
docker pull martiandefense/redplanet-appsec:latest 
```
### Step 2. Start the environment

```bash
sudo docker run --privileged --name redplanet-appsec-instance \
  -p 8080:8080 -p 9090:9090 \
  -p 8087:3000 \
  -p 8082:8080 -p 8083:8087 -p 8084:8000 \
  -p 8888:80 -p 30080:80 \
  -p 8443:443 -p 30443:443 \
  -p 8025:8025 \
  -p 8085:80 \
  martiandefense/redplanet-appsec:latest
```
---
