# Martian's Hands-on AppSec Training Resources


# 1. RedPlanet Appsec Range - Self-Hosted Mini AppSec Range (Docker)

A plug-and-play application security mini-range built with Docker Compose, designed for learning, teaching, and testing common web and API vulnerabilities.

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

  - **Convenience script works on most Linux systems**  
    ```bash
    curl -fsSL https://get.docker.com -o get-docker.sh && sudo sh ./get-docker.sh
    ```

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
sudo docker pull martiandefense/redplanet-appsec:latest && sudo docker run -v /var/run/docker.sock:/var/run/docker.sock martiandefense/redplanet-appsec:latest
```


## What's Included

This environment includes the following intentionally vulnerable applications and services:

| Service        | Description                                                  | Port(s)                  | URL (s)
|----------------|--------------------------------------------------------------|--------------------------| ---------------------- |
| WebGoat        | Classic OWASP insecure Java app                              | 8080, 9090               | [http://localhost:8080/WebGoat/login](http://localhost:8080/WebGoat/login) |
| Juice Shop     | Modern insecure web app with rich OWASP coverage             | 8087                     | http://localhost:8087|
| crAPI          | "Completely Ridiculous API" for API security hands-on labs   | Multiple (8082–8084, 8888, 8443) | http://localhost:8888 |
| MailHog        | Email testing interface for crAPI mail features              | 8025                     | http://localhost:8025 |
| Metasploitable2 | Intentionally vulnerable VM. Active services are DNS,Tomcat and HTTP | Multiple (8081, 53) | http://localhost:8081, http://localhost:8081/dvwa, http://localhost:8081/mutillidae/ |
| Jenkins | CI/CD automation | 8082 | http://localhost:8082/ | http://localhost:8929/ |
| GitLab | Git repository manager | 8929 | http://localhost:8929/ |
| SonarQube | Code quality and security metrics | 9000 | http://localhost:9000/ |
| ------         |
| Trivy | Vulnerability scanner | N/A | CLI Tool|
| Gitleaks | Secret scanning tool | N/A | Typically integrated into CI/CD pipelines |
| PostgreSQL     | Backend DB for crAPI                                         | Internal                 |
| MongoDB        | NoSQL DB used by crAPI                                       | Internal                 |



## Usage

### Step1. Pull the image
```bash
docker pull martiandefense/redplanet-appsec:latest 
```
### Step 2. Start the environment

```bash
sudo docker run -v /var/run/docker.sock:/var/run/docker.sock martiandefense/redplanet-appsec:latest
```
> **_NOTE:_**  The vulnerable machine only version of this range is available at the tag `:pentest` by replacing the above image with `martiandefense/redplanet-appsec:pentest`
