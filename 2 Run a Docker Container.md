### Nautilus DevOps team is testing some applications deployment on some of the application servers. They need to deploy a nginx container on Application Server 3. Please complete the task as per details given below:


On Application Server 3 create a container named nginx_3 using image nginx with alpine tag and make sure container is in running state.

```ruby
thor@jump_host ~$ ssh banner@172.16.238.12
The authenticity of host '172.16.238.12 (172.16.238.12)' can't be established.
ECDSA key fingerprint is SHA256:62O6Vcl9B41FX1xrRSvgxoNSz82O5YmEoR1xrLflzG4.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '172.16.238.12' (ECDSA) to the list of known hosts.
banner@172.16.238.12's password: 

[banner@stapp03 ~]$ docker --version
Docker version 19.03.15, build 99e3ed8919


[banner@stapp03 ~]$ docker pull nginx:alpine
alpine: Pulling from library/nginx
96526aa774ef: Pull complete 
f2004135e416: Pull complete 
fbf1cf5026c4: Pull complete 
38966af6931d: Pull complete 
c3ee70732c61: Pull complete 
7e2fd992447a: Pull complete 
76cbc9ea6abf: Pull complete 
37f8bcf34db7: Pull complete 
Digest: sha256:4c93a3bd8bf95412889dd84213570102176b6052d88bb828eaf449c56aca55ef
Status: Downloaded newer image for nginx:alpine
docker.io/library/nginx:alpine



[banner@stapp03 ~]$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES



[banner@stapp03 ~]$ docker run -d --name nginx_3 -p 80:80 nginx:alpine
fc2e0106666e7ff44e36ad0460d603091a3a1563c8c62a6e4f1da2bbb7a907da
```
The command `docker run -d --name nginx_3 -p 80:80 nginx:alpine` is used to create and run a Docker container from the `nginx:alpine` image with specific configuration options. Let's break down the command:

1. **`docker run`**: This part of the command tells Docker to run a new container.

2. **`-d`**: The `-d` flag stands for "detached." It runs the container in the background, which means it won't take over your current terminal session, and you can continue to use the terminal for other commands.

3. **`--name nginx_3`**: This option specifies the name of the container. In this case, the container will be named "nginx_3."

4. **`-p 80:80`**: The `-p` flag is used to map ports between the host and the container. In this case, it's mapping port 80 from the host to port 80 in the container. This means that any traffic directed to port 80 on the host machine will be forwarded to port 80 in the running container.

5. **`nginx:alpine`**: This is the image you want to use for creating the container. It specifies the image name (`nginx`) and the tag (`alpine`). The `alpine` tag indicates the lightweight Alpine Linux-based version of the Nginx image.

So, in summary, the command `docker run -d --name nginx_3 -p 80:80 nginx:alpine` creates a detached Docker container named "nginx_3" from the "nginx:alpine" image and maps port 80 on the host to port 80 in the container. This allows you to run Nginx in a containerized environment with the specified configuration.


```ruby
[banner@stapp03 ~]$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES
fc2e0106666e        nginx:alpine        "/docker-entrypoint.…"   27 seconds ago      Up 26 seconds       0.0.0.0:80->80/tcp   nginx_3
[banner@stapp03 ~]$ 
```
