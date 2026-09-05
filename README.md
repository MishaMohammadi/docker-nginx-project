# Docker + Nginx Web Application on AWS EC2

## 📌 Project Overview

This project demonstrates how to containerize and run a web application using **Docker and Nginx on an Amazon EC2 instance**.

The project starts with the official Nginx Docker image and then creates a **custom Docker image** using a Dockerfile. The custom image contains an HTML webpage and is deployed as a Docker container on an AWS EC2 instance.

Two Nginx containers are used to demonstrate Docker containerization and port mapping:

* Standard Nginx container → EC2 Port 80
* Custom Nginx container → EC2 Port 8080

---

## 🎯 Project Objective

The main objective of this project is to understand and demonstrate the basic Docker deployment workflow:

```text
Dockerfile
     ↓
docker build
     ↓
Docker Image
     ↓
docker run
     ↓
Docker Container
     ↓
Port Mapping
     ↓
Web Application
```

This project demonstrates how an application can be packaged into a Docker image and run consistently inside a container.

---

## ☁️ Architecture

```text
                         Internet
                            |
                            ↓
                  AWS Security Group
                    /             \
                  :80             :8080
                   |                |
                   ↓                ↓
          Standard Nginx      Custom Nginx
             Container          Container
                   |                |
                   ↓                ↓
          Welcome to Nginx!     index.html
                                    |
                                    ↓
                             Custom Website
```

---

## 🛠️ Technologies Used

* Amazon EC2
* Docker
* Nginx
* Linux
* HTML
* AWS Security Groups

---

## 📂 Project Structure

```text
docker-nginx-project/
│
├── Dockerfile
├── index.html
└── README.md
```

---

## 🐳 Docker Image

The official Nginx image was downloaded using:

```bash
docker pull nginx
```

The downloaded image was verified using:

```bash
docker images
```

---

## 📄 Dockerfile

The custom Docker image was created using the following Dockerfile:

```dockerfile
FROM nginx
COPY index.html /usr/share/nginx/html/
```

### Explanation

**`FROM nginx`**

Uses the official Nginx image as the base image.

**`COPY index.html /usr/share/nginx/html/`**

Copies the custom HTML webpage into Nginx's default web root directory inside the container.

---

## 🔨 Building the Custom Docker Image

The custom image was created using:

```bash
docker build -t nginx2 .
```

Here:

* `docker build` → Creates a Docker image
* `-t nginx2` → Gives the image the name `nginx2`
* `.` → Uses the current directory as the build context

---

## 🚀 Running the Containers

### Standard Nginx Container

The standard Nginx container was started using:

```bash
docker run -d -p 80:80 nginx
```

Port mapping:

```text
EC2 Port 80 → Container Port 80
```

This displays the default:

**Welcome to nginx!**

---

### Custom Nginx Container

The custom Nginx container was started using:

```bash
docker run -d -p 8080:80 nginx2
```

Port mapping:

```text
EC2 Port 8080 → Container Port 80
```

The container still uses port 80 internally because Nginx listens on port 80 by default.

Docker maps the EC2 host port 8080 to the container's port 80.

---

## 🔌 Port Mapping

| EC2 Host Port | Container Port | Purpose              |
| ------------: | -------------: | -------------------- |
|            80 |             80 | Standard Nginx       |
|          8080 |             80 | Custom Nginx Website |

The two containers use different EC2 host ports so they can run simultaneously.

---

## 🔐 AWS Security Group

The EC2 Security Group was configured to allow:

| Type       | Port | Purpose              |
| ---------- | ---: | -------------------- |
| SSH        |   22 | Remote EC2 access    |
| HTTP       |   80 | Standard Nginx       |
| Custom TCP | 8080 | Custom Nginx website |

Port 8080 was configured as **Custom TCP** rather than allowing all traffic.

---

## 🧪 Testing

The running containers were checked using:

```bash
docker ps
```

The custom Nginx container was tested locally using:

```bash
curl http://localhost:8080
```

HTTP response headers were verified using:

```bash
curl -I http://localhost:8080
```

A successful response returned:

```text
HTTP/1.1 200 OK
```

---

## 🌐 Accessing the Application

### Standard Nginx

```text
http://EC2-PUBLIC-IP
```

Displays the default Nginx welcome page.

### Custom Website

```text
http://EC2-PUBLIC-IP:8080
```

Displays the custom HTML website created for this project.

---

## 📸 Project Screenshots

The project was documented using screenshots showing:

1. Project directory creation
2. Docker installation and verification
3. Nginx image download
4. AWS Security Group configuration
5. Standard Nginx container
6. Default Nginx webpage
7. Dockerfile
8. Custom index.html
9. Custom Docker image
10. Both running containers
11. Container HTTP test
12. Final custom website
13. Final project files

---

## ✅ Result

Successfully created and deployed a custom Nginx Docker image on an Amazon EC2 instance.

The project demonstrates:

* Docker image management
* Dockerfile creation
* Custom Docker image creation
* Docker container deployment
* Nginx web server configuration
* Docker port mapping
* AWS Security Group configuration
* Container testing
* Running multiple containers on different host ports

---

## 💡 Key Docker Concept

The core workflow demonstrated in this project is:

```text
Dockerfile
     ↓
Docker Image
     ↓
Docker Container
     ↓
Port Mapping
     ↓
Application
```

This project provides a basic understanding of how Docker can be used to package and run applications in isolated, portable containers.
