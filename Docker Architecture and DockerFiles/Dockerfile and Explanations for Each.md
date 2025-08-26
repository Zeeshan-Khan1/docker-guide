Stages of Containerization

What it means: The process of moving from a traditional app → virtual machines → containers.

Work:

Code → You write your app.

Dependencies → Install libraries.

Dockerfile → Define how to build the image.

Image → Build with docker build.

Container → Run with docker run.


10. Architecture and Components of Docker

Docker has 3 main parts:

Docker Engine (Daemon) – Runs in background, manages containers.

Docker CLI – Commands you type (docker run, docker ps).

Docker Hub/Registry – Stores/pulls images.

Repo file:

[User] -> [Docker CLI] -> [Docker Daemon] -> [Images & Containers]

11. A quick look at the format of Dockerfile

Dockerfile is a text file with instructions.

Basic format:

FROM <base-image>
RUN <command>
COPY <src> <dest>
CMD ["executable", "param1", "param2"]


12. Demo: Dockerfile - Fundamental Instructions

Instructions used:

FROM – base image.

RUN – run a command during image build.

COPY – copy files from host to container.

CMD – command to run when container starts.

Example:

FROM ubuntu:20.04
RUN apt-get update && apt-get install -y curl
COPY index.html /usr/share/nginx/html/
CMD ["echo", "Hello from container!"]


13. Demo: Dockerfile - Configuration Instructions

Instructions used:

ENV – set environment variables.

WORKDIR – set working directory.

USER – specify user.

Example:

FROM ubuntu:20.04
ENV APP_ENV=production
WORKDIR /app
COPY . /app
CMD ["bash"]

14. Demo: Dockerfile - Expose Instructions

EXPOSE = tells Docker which port the container listens on.

Example:

FROM nginx:latest
COPY index.html /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]


Run:

docker build -t my-nginx .
docker run -p 8080:80 my-nginx


15. Note for the upcoming Apache demo

This is just a note folder where you explain:

"We’ll containerize an Apache web server in the next step."

16. Demo: Containerizing application with Dockerfile

Steps:

Write Dockerfile for Apache or Nginx app.

Build image:

docker build -t my-apache .


Run container:

docker run -d -p 8080:80 my-apache


Open browser → http://localhost:8080.

Example Dockerfile:

FROM httpd:latest
COPY ./index.html /usr/local/apache2/htdocs/
EXPOSE 80
CMD ["httpd-foreground"]
