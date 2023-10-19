### One of the Nautilus project developers created a container on App Server 1. This container was created for testing only and now we need to delete it. Accomplish this task as per details given below:



Delete a container named kke-container, its running on App Server 1 in Stratos DC.


```ruby
thor@jump_host ~$ ssh tony@stapp01
The authenticity of host 'stapp01 (172.16.238.10)' can't be established.
ECDSA key fingerprint is SHA256:NYIyllyjiguTWW5T0vRr9dkRjzIZlP1No3eRre48xv0.
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
CONTAINER ID        IMAGE               COMMAND               CREATED             STATUS              PORTS               NAMES
35be4cd86566        busybox             "tail -f /dev/null"   2 minutes ago       Up 2 minutes                            kke-container
[root@stapp01 ~]# docker stop kke-container

        
[root@stapp01 ~]# docker stop kke-container
kke-container

[root@stapp01 ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES


[root@stapp01 ~]# docker rm kke-container
kke-container

```
