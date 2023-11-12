###  The Nautilus DevOps team has some confidential data present on App Server 2 in Stratos Datacenter. There is a container ubuntu_latest running on the same server. We received a request to copy some of the data from the docker host to the container. Below are more details about the task:



On App Server 2 in Stratos Datacenter copy an encrypted file /tmp/nautilus.txt.gpg from docker host to ubuntu_latest container (running on same server) in /tmp/ location. Please do not try to modify this file in any way.

```ruby
thor@jump_host ~$ ssh steve@stapp02
The authenticity of host 'stapp02 (172.16.238.11)' can't be established.
ECDSA key fingerprint is SHA256:avLoD2p9YdMVySj7hsr7IAoyN6rykp1LP0ljE0Fw9Jg.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'stapp02,172.16.238.11' (ECDSA) to the list of known hosts.
steve@stapp02's password: 
[steve@stapp02 ~]$ sudo su -

We trust you have received the usual lecture from the local System
Administrator. It usually boils down to these three things:

    #1) Respect the privacy of others.
    #2) Think before you type.
    #3) With great power comes great responsibility.

[sudo] password for steve: 
[root@stapp02 ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
089de39c0d98        ubuntu              "/bin/bash"         5 minutes ago       Up 5 minutes                            ubuntu_latest

[root@stapp02 ~]# docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/tmp/
```
explanation of the command `docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/tmp/`:

**1. Docker**: Docker is like a toolbox for building and running applications. It allows you to package an application and its dependencies into a container, which can run consistently on different systems.

**2. `docker cp`**: This is a command in Docker that allows you to copy files between your computer (the host) and a Docker container. It's similar to copying files from one folder to another, but it works with Docker containers.

**3. `/tmp/nautilus.txt.gpg`:** This is the path to a file on your computer. In this case, it's an encrypted file named `nautilus.txt.gpg`, and it's located in the `/tmp/` directory.

**4. `ubuntu_latest`:** This is the name of a Docker container. Containers are like isolated environments where you can run applications. `ubuntu_latest` is the name of the container you want to copy the file into.

**5. `:/tmp/`:** This part of the command specifies the destination path inside the container. You're telling Docker to copy the file into the `/tmp/` directory inside the `ubuntu_latest` container.

So, when you run this command, it will take the `nautilus.txt.gpg` file from your computer and put it into the `ubuntu_latest` container in its `/tmp/` directory. This can be useful when you want to move files between your computer and a running Docker container.
