# Noah Otsuka's Web Server

## Compatible Operating Systems

- Linux

## Starting the server



Run the following command to build and run a Docker container:

```bash
$ ./start
```

This Docker container is named noah-apache-server and runs on `localhost port 8080`.

Finally, input localhost:8080 into your browser of choice to receive the html served by the Apache server.

*NOTE:*

The `start` script requires sudo privileges (at least it did on macOS) to properly install the httpd base Docker Image used to run the Apache server, so if the shell is not already running with these privileges, the user may need to enter the sudo password.

## How the code works

### start

The `start` script is a bash script that consists of a few echo/printf commands and commands to build and run a Docker container on port 8080. As mentioned above, the `start` script runs the `docker build` command with sudo privileges. This is due to macOS (the machine used to create this project was a Macbook Pro 2018 running macOS Monterey 12.6) requiring sudo permissions to install the httpd base Docker image, which is used to install and run the Apache server.

The first Docker command in the file,

```bash
sudo docker build -t noah-apache-server .
```

is used for building a Docker image named `noah-apache-server`. The script then uses the name of the Docker image to then run it as a Docker container using the command below.

```bash
docker run -dp 8080:80 noah-apache-server
```

This run command boots up a Docker container in detatched mode using the flag `-d`, and also uses `-p` to map the host's port, `8080`, to the container''s port, `80`. This is because Apache webservers listen and bind on port 80 by default.

### Dockerfile

The `DockerFile` is a file used for configuring the Apache server Docker image. The concept for creating an Apache server is pretty straightforward. All that is needed in the Docker file is to use the httpd Docker image and copy the html from `src/` folder to the `/usr/local/apache2/htdocs/` folder for Apache to serve. 

### src/

The `src/` folder holds all html files to be served by the Apache server (there is only one). 

## Why I chose Apache

Throughout my career, I have heard many people mention Apache, and have always been curious as to what it is, so I saw this project as an opprotunity to get hands on with Apache and learn how it works.

Since most of my experience with web servers has been through Node.js, I was not too familiar with the webserver options presented for the project. I did some reasearch on each server, and found that Apache was the best for its ease of deployment and again my curiosity in the tool. 

## Why I chose Docker

Similiar to the reason I chose Apache, I chose Docker, because of its popularity and the opprotunity for me to learn more about it. Before this project, I only knew the high level concept of what Docker does, and I know that Docker is a widly used tool in software. So I chose to use Docker to also get hands on experience and learn more about Docker. Additionally, using Docker would allow me to not create any config management scripts, which would quicken the deployment/server creation process and allow for the project to be more portable and less prone to deployment bugs.
