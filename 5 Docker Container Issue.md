###  There is a static website running within a container named nautilus, this container is running on App Server 1. Suddenly, we started facing some issues with the static website on App Server 1. Look into the issue to fix the same, you can find more details below:



Container's volume /usr/local/apache2/htdocs is mapped with the host's volume /var/www/html.

The website should run on host port 8080 on App Server 1 i.e command curl http://localhost:8080/ should work on App Server 1.


```ruby
thor@jump_host ~$ ssh tony@stapp01
The authenticity of host 'stapp01 (172.16.238.10)' can't be established.
ECDSA key fingerprint is SHA256:ZjuAj/PH9N3eIw/ahnRUHp2f8akUMU2vEDOKG613xlg.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes 
Warning: Permanently added 'stapp01,172.16.238.10' (ECDSA) to the list of known hosts.
tony@stapp01's password: 
[tony@stapp01 ~]$ sudo su -

We trust you have received the usual lecture from the local System
Administrator. It usually boils down to these three things:

    #1) Respect the privacy of others.
    #2) Think before you type.
    #3) With great power comes great responsibility.

[sudo] password for tony: 
[root@stapp01 ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[root@stapp01 ~]# curl http://localhost:8080/
curl: (7) Failed to connect to localhost port 8080: Connection refused
[root@stapp01 ~]# docker logs nautilus
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.18.0.2. Set the 'ServerName' directive globally to suppress this message
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.18.0.2. Set the 'ServerName' directive globally to suppress this message
[Thu Oct 19 13:34:20.249817 2023] [mpm_event:notice] [pid 1:tid 140614761441152] AH00489: Apache/2.4.57 (Unix) configured -- resuming normal operations
[Thu Oct 19 13:34:20.250001 2023] [core:notice] [pid 1:tid 140614761441152] AH00094: Command line: 'httpd -D FOREGROUND'
[Thu Oct 19 13:34:20.379695 2023] [mpm_event:notice] [pid 1:tid 140614761441152] AH00492: caught SIGWINCH, shutting down gracefully
[root@stapp01 ~]# docker exec -it nautilus bash
Error response from daemon: Container 4f4227718e8098371864a80885a342e320fc90429b7c3f014ef1469a3387fdb3 is not running
[root@stapp01 ~]# service apache2 start
Redirecting to /bin/systemctl start apache2.service
Failed to start apache2.service: Unit apache2.service not found.




[root@stapp01 ~]# docker run -d --name my_website_container -p 8080:80 -v /var/www/html:/usr/local/apache2/htdocs nginx:alpine
Unable to find image 'nginx:alpine' locally
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
626c35c1e93e42fe647172eae9655bf3dd2561d43963fb4deb4a9fa935f56bc8
```
To create a Docker container using the provided requirements where the container's volume `/usr/local/apache2/htdocs` is mapped with the host's volume `/var/www/html`, and the website should run on host port 8080, you can use the following `docker run` command:

```bash
docker run -d --name my_website_container -p 8080:80 -v /var/www/html:/usr/local/apache2/htdocs nginx:alpine
```

Here's an explanation of the command:

- `docker run`: This command is used to create and start a new Docker container.

- `-d`: It runs the container in detached mode, meaning it runs in the background.

- `--name my_website_container`: Assigns a name to the container, in this case, "my_website_container."

- `-p 8080:80`: Maps port 8080 on the host to port 80 in the container. This is how you expose the website on the host's port 8080.

- `-v /var/www/html:/usr/local/apache2/htdocs`: This option creates a volume mapping, where the host's directory `/var/www/html` is mapped to the container's directory `/usr/local/apache2/htdocs`. This ensures that the website content on the host is synchronized with the container.

- `nginx:alpine`: Specifies the Docker image to use, in this case, the "nginx" image based on Alpine Linux. This image is commonly used for serving web content.

After running this command, the website should be accessible on App Server 1 at `http://localhost:8080/` as specified in the requirements.


```ruby
[root@stapp01 ~]# curl http://localhost:8080/
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
[root@stapp01 ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
626c35c1e93e        nginx:alpine        "/docker-entrypoint.…"   27 seconds ago      Up 24 seconds       0.0.0.0:8080->80/tcp   my_website_container
[root@stapp01 ~]# 
```
