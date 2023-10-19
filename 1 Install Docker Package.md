###  Last week the Nautilus DevOps team met with the application development team and decided to containerize several of their applications. The DevOps team wants to do some testing per the following:


Install docker-ce and docker-compose packages on App Server 1.


Start docker service.


Install Docker CE
https://computingforgeeks.com/install-docker-and-docker-compose-on-rhel-8-centos-8/?expand_article=1


```ruby
[root@stapp01 ~]# sudo yum makecache
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered with an entitlement server. You can use subscription-manager to register.

CentOS Stream 8 - AppStream                                                            24 kB/s | 4.4 kB     00:00    
CentOS Stream 8 - BaseOS                                                               28 kB/s | 3.9 kB     00:00    
CentOS Stream 8 - Extras                                                              9.4 kB/s | 2.9 kB     00:00    
CentOS Stream 8 - Extras common packages                                               18 kB/s | 3.0 kB     00:00    
Docker CE Stable - x86_64                                                              57 kB/s | 3.5 kB     00:00    
Red Hat Universal Base Image 8 (RPMs) - BaseOS                                         19 kB/s | 3.8 kB     00:00    
Red Hat Universal Base Image 8 (RPMs) - AppStream                                      94 kB/s | 4.2 kB     00:00    
Red Hat Universal Base Image 8 (RPMs) - CodeReady Builder                              82 kB/s | 3.8 kB     00:00    
Metadata cache created.
[root@stapp01 ~]# sudo yum remove docker \
>                   docker-client \
>                   docker-client-latest \
>                   docker-common \
>                   docker-latest \
>                   docker-latest-logrotate \
>                   docker-logrotate \
>                   docker-engine \
>                   podman \
>                   runc
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered with an entitlement server. You can use subscription-manager to register.

No match for argument: docker
No match for argument: docker-client
No match for argument: docker-client-latest
No match for argument: docker-common
No match for argument: docker-latest
No match for argument: docker-latest-logrotate
No match for argument: docker-logrotate
No match for argument: docker-engine
No match for argument: podman
No match for argument: runc
No packages marked for removal.
Dependencies resolved.
Nothing to do.
Complete!
[root@stapp01 ~]# yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered with an entitlement server. You can use subscription-manager to register.

Last metadata expiration check: 0:01:55 ago on Thu Oct 19 11:42:41 2023.
Dependencies resolved.
======================================================================================================================
 Package                           Arch        Version                                   Repository              Size
======================================================================================================================
Installing:
 containerd.io                     x86_64      1.6.24-3.1.el8                            docker-ce-stable        34 M
 docker-buildx-plugin              x86_64      0.11.2-1.el8                              docker-ce-stable        13 M
 docker-ce                         x86_64      3:24.0.6-1.el8                            docker-ce-stable        24 M
 docker-ce-cli                     x86_64      1:24.0.6-1.el8                            docker-ce-stable       7.2 M
 docker-compose-plugin             x86_64      2.21.0-1.el8                              docker-ce-stable        13 M
Installing dependencies:
 checkpolicy                       x86_64      2.9-1.el8                                 baseos                 348 k
 container-selinux                 noarch      2:2.221.0-1.module_el8+653+feef7bfe       appstream               69 k
 diffutils                         x86_64      3.6-6.el8                                 baseos                 358 k
 docker-ce-rootless-extras         x86_64      24.0.6-1.el8                              docker-ce-stable       4.9 M
 fuse-common                       x86_64      3.3.0-17.el8                              baseos                  22 k
 fuse-overlayfs                    x86_64      1.12-1.module_el8+454+d7ef4b8d            appstream               70 k
 fuse3                             x86_64      3.3.0-17.el8                              baseos                  54 k
 fuse3-libs                        x86_64      3.3.0-17.el8                              baseos                  95 k
 iptables                          x86_64      1.8.5-10.el8                              baseos                 592 k
 iptables-libs                     x86_64      1.8.5-10.el8                              baseos                 103 k
 libcgroup                         x86_64      0.41-19.el8                               baseos                  70 k
 libibverbs                        x86_64      46.0-1.el8.1                              baseos                 410 k
 libmnl                            x86_64      1.0.4-6.el8                               baseos                  30 k
 libnetfilter_conntrack            x86_64      1.0.6-5.el8                               baseos                  65 k
 libnfnetlink                      x86_64      1.0.1-13.el8                              baseos                  33 k
 libnftnl                          x86_64      1.2.2-3.el8                               baseos                  87 k
 libpcap                           x86_64      14:1.9.1-5.el8                            baseos                 169 k
 libselinux-utils                  x86_64      2.9-8.el8                                 baseos                 243 k
 libslirp                          x86_64      4.4.0-1.module_el8+487+8e42a277           appstream               70 k
 policycoreutils                   x86_64      2.9-24.el8                                baseos                 409 k
 policycoreutils-python-utils      noarch      2.9-24.el8                                baseos                 260 k
 python3-audit                     x86_64      3.0.7-4.el8                               baseos                  87 k
 python3-libselinux                x86_64      2.9-8.el8                                 baseos                 283 k
 python3-libsemanage               x86_64      2.9-9.el8_6                               ubi-8-baseos-rpms      128 k
 python3-policycoreutils           noarch      2.9-24.el8                                baseos                 2.3 M
 python3-setools                   x86_64      4.3.0-5.el8                               baseos                 627 k
 rpm-plugin-selinux                x86_64      4.14.3-26.el8                             baseos                  78 k
 selinux-policy                    noarch      3.14.3-130.el8                            baseos                 665 k
 selinux-policy-targeted           noarch      3.14.3-130.el8                            baseos                  16 M
 slirp4netns                       x86_64      1.2.1-1.module_el8+661+d1afb926           appstream               56 k
 xz                                x86_64      5.2.4-4.el8_6                             ubi-8-baseos-rpms      153 k
Enabling module streams:
 container-tools                               rhel8                                                                 

Transaction Summary
======================================================================================================================
Install  36 Packages

Total download size: 120 M
Installed size: 436 M
Is this ok [y/N]: y
Downloading Packages:
(1/36): fuse-overlayfs-1.12-1.module_el8+454+d7ef4b8d.x86_64.rpm                      343 kB/s |  70 kB     00:00    
(2/36): container-selinux-2.221.0-1.module_el8+653+feef7bfe.noarch.rpm                336 kB/s |  69 kB     00:00    
(3/36): libslirp-4.4.0-1.module_el8+487+8e42a277.x86_64.rpm                           337 kB/s |  70 kB     00:00    
(4/36): slirp4netns-1.2.1-1.module_el8+661+d1afb926.x86_64.rpm                        719 kB/s |  56 kB     00:00    
(5/36): fuse-common-3.3.0-17.el8.x86_64.rpm                                           418 kB/s |  22 kB     00:00    
(6/36): diffutils-3.6-6.el8.x86_64.rpm                                                1.9 MB/s | 358 kB     00:00    
(7/36): checkpolicy-2.9-1.el8.x86_64.rpm                                              1.8 MB/s | 348 kB     00:00    
(8/36): fuse3-3.3.0-17.el8.x86_64.rpm                                                 821 kB/s |  54 kB     00:00    
(9/36): fuse3-libs-3.3.0-17.el8.x86_64.rpm                                            1.7 MB/s |  95 kB     00:00    
(10/36): iptables-libs-1.8.5-10.el8.x86_64.rpm                                        1.1 MB/s | 103 kB     00:00    
(11/36): iptables-1.8.5-10.el8.x86_64.rpm                                             4.7 MB/s | 592 kB     00:00    
(12/36): libcgroup-0.41-19.el8.x86_64.rpm                                             915 kB/s |  70 kB     00:00    
(13/36): libmnl-1.0.4-6.el8.x86_64.rpm                                                655 kB/s |  30 kB     00:00    
(14/36): libnfnetlink-1.0.1-13.el8.x86_64.rpm                                         699 kB/s |  33 kB     00:00    
(15/36): libnetfilter_conntrack-1.0.6-5.el8.x86_64.rpm                                625 kB/s |  65 kB     00:00    
(16/36): libnftnl-1.2.2-3.el8.x86_64.rpm                                              1.6 MB/s |  87 kB     00:00    
(17/36): libibverbs-46.0-1.el8.1.x86_64.rpm                                           2.1 MB/s | 410 kB     00:00    
(18/36): libpcap-1.9.1-5.el8.x86_64.rpm                                               2.3 MB/s | 169 kB     00:00    
(19/36): libselinux-utils-2.9-8.el8.x86_64.rpm                                        3.8 MB/s | 243 kB     00:00    
(20/36): policycoreutils-2.9-24.el8.x86_64.rpm                                        4.3 MB/s | 409 kB     00:00    
(21/36): python3-audit-3.0.7-4.el8.x86_64.rpm                                         1.5 MB/s |  87 kB     00:00    
(22/36): policycoreutils-python-utils-2.9-24.el8.noarch.rpm                           2.5 MB/s | 260 kB     00:00    
(23/36): python3-libselinux-2.9-8.el8.x86_64.rpm                                      3.6 MB/s | 283 kB     00:00    
(24/36): python3-setools-4.3.0-5.el8.x86_64.rpm                                       6.2 MB/s | 627 kB     00:00    
(25/36): rpm-plugin-selinux-4.14.3-26.el8.x86_64.rpm                                  1.7 MB/s |  78 kB     00:00    
(26/36): python3-policycoreutils-2.9-24.el8.noarch.rpm                                 15 MB/s | 2.3 MB     00:00    
(27/36): selinux-policy-3.14.3-130.el8.noarch.rpm                                      10 MB/s | 665 kB     00:00    
(28/36): docker-buildx-plugin-0.11.2-1.el8.x86_64.rpm                                  44 MB/s |  13 MB     00:00    
(29/36): selinux-policy-targeted-3.14.3-130.el8.noarch.rpm                             32 MB/s |  16 MB     00:00    
(30/36): containerd.io-1.6.24-3.1.el8.x86_64.rpm                                       49 MB/s |  34 MB     00:00    
(31/36): docker-ce-24.0.6-1.el8.x86_64.rpm                                             46 MB/s |  24 MB     00:00    
(32/36): docker-ce-rootless-extras-24.0.6-1.el8.x86_64.rpm                             27 MB/s | 4.9 MB     00:00    
(33/36): docker-ce-cli-24.0.6-1.el8.x86_64.rpm                                         15 MB/s | 7.2 MB     00:00    
(34/36): docker-compose-plugin-2.21.0-1.el8.x86_64.rpm                                 61 MB/s |  13 MB     00:00    
(35/36): python3-libsemanage-2.9-9.el8_6.x86_64.rpm                                   700 kB/s | 128 kB     00:00    
(36/36): xz-5.2.4-4.el8_6.x86_64.rpm                                                  1.1 MB/s | 153 kB     00:00    
----------------------------------------------------------------------------------------------------------------------
Total                                                                                  55 MB/s | 120 MB     00:02     
Docker CE Stable - x86_64                                                              35 kB/s | 1.6 kB     00:00    
Importing GPG key 0x621E9F35:
 Userid     : "Docker Release (CE rpm) <docker@docker.com>"
 Fingerprint: 060A 61C5 1B55 8A7F 742B 77AA C52F EB6B 621E 9F35
 From       : https://download.docker.com/linux/centos/gpg
Is this ok [y/N]: y
Key imported successfully
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                              1/1 
  Installing       : python3-libselinux-2.9-8.el8.x86_64                                                         1/36 
  Installing       : libmnl-1.0.4-6.el8.x86_64                                                                   2/36 
  Running scriptlet: libmnl-1.0.4-6.el8.x86_64                                                                   2/36 
  Installing       : docker-compose-plugin-2.21.0-1.el8.x86_64                                                   3/36 
  Running scriptlet: docker-compose-plugin-2.21.0-1.el8.x86_64                                                   3/36 
  Installing       : libselinux-utils-2.9-8.el8.x86_64                                                           4/36 
  Installing       : libnfnetlink-1.0.1-13.el8.x86_64                                                            5/36 
  Running scriptlet: libnfnetlink-1.0.1-13.el8.x86_64                                                            5/36 
  Installing       : fuse3-libs-3.3.0-17.el8.x86_64                                                              6/36 
  Running scriptlet: fuse3-libs-3.3.0-17.el8.x86_64                                                              6/36 
  Installing       : libnetfilter_conntrack-1.0.6-5.el8.x86_64                                                   7/36 
  Running scriptlet: libnetfilter_conntrack-1.0.6-5.el8.x86_64                                                   7/36 
  Installing       : libnftnl-1.2.2-3.el8.x86_64                                                                 8/36 
  Running scriptlet: libnftnl-1.2.2-3.el8.x86_64                                                                 8/36 
  Installing       : python3-setools-4.3.0-5.el8.x86_64                                                          9/36 
  Installing       : python3-libsemanage-2.9-9.el8_6.x86_64                                                     10/36 
  Installing       : xz-5.2.4-4.el8_6.x86_64                                                                    11/36 
  Installing       : docker-buildx-plugin-0.11.2-1.el8.x86_64                                                   12/36 
  Running scriptlet: docker-buildx-plugin-0.11.2-1.el8.x86_64                                                   12/36 
  Installing       : docker-ce-cli-1:24.0.6-1.el8.x86_64                                                        13/36 
  Running scriptlet: docker-ce-cli-1:24.0.6-1.el8.x86_64                                                        13/36 
  Installing       : python3-audit-3.0.7-4.el8.x86_64                                                           14/36 
  Installing       : libibverbs-46.0-1.el8.1.x86_64                                                             15/36 
  Installing       : libpcap-14:1.9.1-5.el8.x86_64                                                              16/36 
  Installing       : iptables-libs-1.8.5-10.el8.x86_64                                                          17/36 
  Running scriptlet: iptables-1.8.5-10.el8.x86_64                                                               18/36 
  Installing       : iptables-1.8.5-10.el8.x86_64                                                               18/36 
  Running scriptlet: iptables-1.8.5-10.el8.x86_64                                                               18/36 
  Running scriptlet: libcgroup-0.41-19.el8.x86_64                                                               19/36 
  Installing       : libcgroup-0.41-19.el8.x86_64                                                               19/36 
  Running scriptlet: libcgroup-0.41-19.el8.x86_64                                                               19/36 
  Installing       : fuse-common-3.3.0-17.el8.x86_64                                                            20/36 
  Installing       : fuse3-3.3.0-17.el8.x86_64                                                                  21/36 
  Installing       : fuse-overlayfs-1.12-1.module_el8+454+d7ef4b8d.x86_64                                       22/36 
  Running scriptlet: fuse-overlayfs-1.12-1.module_el8+454+d7ef4b8d.x86_64                                       22/36 
  Installing       : diffutils-3.6-6.el8.x86_64                                                                 23/36 
  Running scriptlet: diffutils-3.6-6.el8.x86_64                                                                 23/36 
  Installing       : policycoreutils-2.9-24.el8.x86_64                                                          24/36 
  Running scriptlet: policycoreutils-2.9-24.el8.x86_64                                                          24/36 
  Installing       : rpm-plugin-selinux-4.14.3-26.el8.x86_64                                                    25/36 
  Installing       : selinux-policy-3.14.3-130.el8.noarch                                                       26/36 
  Running scriptlet: selinux-policy-3.14.3-130.el8.noarch                                                       26/36 
  Running scriptlet: selinux-policy-targeted-3.14.3-130.el8.noarch                                              27/36 
  Installing       : selinux-policy-targeted-3.14.3-130.el8.noarch                                              27/36 
  Running scriptlet: selinux-policy-targeted-3.14.3-130.el8.noarch                                              27/36 
  Installing       : checkpolicy-2.9-1.el8.x86_64                                                               28/36 
  Installing       : python3-policycoreutils-2.9-24.el8.noarch                                                  29/36 
  Installing       : policycoreutils-python-utils-2.9-24.el8.noarch                                             30/36 
  Running scriptlet: container-selinux-2:2.221.0-1.module_el8+653+feef7bfe.noarch                               31/36 
  Installing       : container-selinux-2:2.221.0-1.module_el8+653+feef7bfe.noarch                               31/36 
  Running scriptlet: container-selinux-2:2.221.0-1.module_el8+653+feef7bfe.noarch                               31/36 
  Installing       : containerd.io-1.6.24-3.1.el8.x86_64                                                        32/36 
  Running scriptlet: containerd.io-1.6.24-3.1.el8.x86_64                                                        32/36 
  Installing       : libslirp-4.4.0-1.module_el8+487+8e42a277.x86_64                                            33/36 
  Installing       : slirp4netns-1.2.1-1.module_el8+661+d1afb926.x86_64                                         34/36 
  Installing       : docker-ce-rootless-extras-24.0.6-1.el8.x86_64                                              35/36 
  Running scriptlet: docker-ce-rootless-extras-24.0.6-1.el8.x86_64                                              35/36 
  Installing       : docker-ce-3:24.0.6-1.el8.x86_64                                                            36/36 
  Running scriptlet: docker-ce-3:24.0.6-1.el8.x86_64                                                            36/36 
  Running scriptlet: container-selinux-2:2.221.0-1.module_el8+653+feef7bfe.noarch                               36/36 
  Running scriptlet: docker-ce-3:24.0.6-1.el8.x86_64                                                            36/36 
  Verifying        : container-selinux-2:2.221.0-1.module_el8+653+feef7bfe.noarch                                1/36 
  Verifying        : fuse-overlayfs-1.12-1.module_el8+454+d7ef4b8d.x86_64                                        2/36 
  Verifying        : libslirp-4.4.0-1.module_el8+487+8e42a277.x86_64                                             3/36 
  Verifying        : slirp4netns-1.2.1-1.module_el8+661+d1afb926.x86_64                                          4/36 
  Verifying        : checkpolicy-2.9-1.el8.x86_64                                                                5/36 
  Verifying        : diffutils-3.6-6.el8.x86_64                                                                  6/36 
  Verifying        : fuse-common-3.3.0-17.el8.x86_64                                                             7/36 
  Verifying        : fuse3-3.3.0-17.el8.x86_64                                                                   8/36 
  Verifying        : fuse3-libs-3.3.0-17.el8.x86_64                                                              9/36 
  Verifying        : iptables-1.8.5-10.el8.x86_64                                                               10/36 
  Verifying        : iptables-libs-1.8.5-10.el8.x86_64                                                          11/36 
  Verifying        : libcgroup-0.41-19.el8.x86_64                                                               12/36 
  Verifying        : libibverbs-46.0-1.el8.1.x86_64                                                             13/36 
  Verifying        : libmnl-1.0.4-6.el8.x86_64                                                                  14/36 
  Verifying        : libnetfilter_conntrack-1.0.6-5.el8.x86_64                                                  15/36 
  Verifying        : libnfnetlink-1.0.1-13.el8.x86_64                                                           16/36 
  Verifying        : libnftnl-1.2.2-3.el8.x86_64                                                                17/36 
  Verifying        : libpcap-14:1.9.1-5.el8.x86_64                                                              18/36 
  Verifying        : libselinux-utils-2.9-8.el8.x86_64                                                          19/36 
  Verifying        : policycoreutils-2.9-24.el8.x86_64                                                          20/36 
  Verifying        : policycoreutils-python-utils-2.9-24.el8.noarch                                             21/36 
  Verifying        : python3-audit-3.0.7-4.el8.x86_64                                                           22/36 
  Verifying        : python3-libselinux-2.9-8.el8.x86_64                                                        23/36 
  Verifying        : python3-policycoreutils-2.9-24.el8.noarch                                                  24/36 
  Verifying        : python3-setools-4.3.0-5.el8.x86_64                                                         25/36 
  Verifying        : rpm-plugin-selinux-4.14.3-26.el8.x86_64                                                    26/36 
  Verifying        : selinux-policy-3.14.3-130.el8.noarch                                                       27/36 
  Verifying        : selinux-policy-targeted-3.14.3-130.el8.noarch                                              28/36 
  Verifying        : containerd.io-1.6.24-3.1.el8.x86_64                                                        29/36 
  Verifying        : docker-buildx-plugin-0.11.2-1.el8.x86_64                                                   30/36 
  Verifying        : docker-ce-3:24.0.6-1.el8.x86_64                                                            31/36 
  Verifying        : docker-ce-cli-1:24.0.6-1.el8.x86_64                                                        32/36 
  Verifying        : docker-ce-rootless-extras-24.0.6-1.el8.x86_64                                              33/36 
  Verifying        : docker-compose-plugin-2.21.0-1.el8.x86_64                                                  34/36 
  Verifying        : python3-libsemanage-2.9-9.el8_6.x86_64                                                     35/36 
  Verifying        : xz-5.2.4-4.el8_6.x86_64                                                                    36/36 
Installed products updated.

Installed:
  checkpolicy-2.9-1.el8.x86_64                          container-selinux-2:2.221.0-1.module_el8+653+feef7bfe.noarch 
  containerd.io-1.6.24-3.1.el8.x86_64                   diffutils-3.6-6.el8.x86_64                                   
  docker-buildx-plugin-0.11.2-1.el8.x86_64              docker-ce-3:24.0.6-1.el8.x86_64                              
  docker-ce-cli-1:24.0.6-1.el8.x86_64                   docker-ce-rootless-extras-24.0.6-1.el8.x86_64                
  docker-compose-plugin-2.21.0-1.el8.x86_64             fuse-common-3.3.0-17.el8.x86_64                              
  fuse-overlayfs-1.12-1.module_el8+454+d7ef4b8d.x86_64  fuse3-3.3.0-17.el8.x86_64                                    
  fuse3-libs-3.3.0-17.el8.x86_64                        iptables-1.8.5-10.el8.x86_64                                 
  iptables-libs-1.8.5-10.el8.x86_64                     libcgroup-0.41-19.el8.x86_64                                 
  libibverbs-46.0-1.el8.1.x86_64                        libmnl-1.0.4-6.el8.x86_64                                    
  libnetfilter_conntrack-1.0.6-5.el8.x86_64             libnfnetlink-1.0.1-13.el8.x86_64                             
  libnftnl-1.2.2-3.el8.x86_64                           libpcap-14:1.9.1-5.el8.x86_64                                
  libselinux-utils-2.9-8.el8.x86_64                     libslirp-4.4.0-1.module_el8+487+8e42a277.x86_64              
  policycoreutils-2.9-24.el8.x86_64                     policycoreutils-python-utils-2.9-24.el8.noarch               
  python3-audit-3.0.7-4.el8.x86_64                      python3-libselinux-2.9-8.el8.x86_64                          
  python3-libsemanage-2.9-9.el8_6.x86_64                python3-policycoreutils-2.9-24.el8.noarch                    
  python3-setools-4.3.0-5.el8.x86_64                    rpm-plugin-selinux-4.14.3-26.el8.x86_64                      
  selinux-policy-3.14.3-130.el8.noarch                  selinux-policy-targeted-3.14.3-130.el8.noarch                
  slirp4netns-1.2.1-1.module_el8+661+d1afb926.x86_64    xz-5.2.4-4.el8_6.x86_64                                      

Complete!
[root@stapp01 ~]# 
[root@stapp01 ~]# 
[root@stapp01 ~]# 
[root@stapp01 ~]# 
[root@stapp01 ~]# 
[root@stapp01 ~]# yum install docker-ce --allowerasing
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered with an entitlement server. You can use subscription-manager to register.

Last metadata expiration check: 0:04:09 ago on Thu Oct 19 11:42:41 2023.
Package docker-ce-3:24.0.6-1.el8.x86_64 is already installed.
Dependencies resolved.
Nothing to do.
Complete!
[root@stapp01 ~]# systemctl enable --now docker
Created symlink /etc/systemd/system/multi-user.target.wants/docker.service → /usr/lib/systemd/system/docker.service.
[root@stapp01 ~]# systemctl status  docker
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; vendor preset: disabled)
   Active: active (running) since Thu 2023-10-19 11:47:23 UTC; 28s ago
     Docs: https://docs.docker.com
 Main PID: 2487 (dockerd)
    Tasks: 24
   Memory: 34.6M
   CGroup: /docker/a88c516a43a91e9506d4673a91053f6b4de77249fd9949bb9897f09fef852cb6/system.slice/docker.service
           └─2487 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

Oct 19 11:47:23 stapp01.stratos.xfusioncorp.com dockerd[2487]: time="2023-10-19T11:47:23.322010646Z" level=info msg="L
oading containers: done."
Oct 19 11:47:23 stapp01.stratos.xfusioncorp.com dockerd[2487]: time="2023-10-19T11:47:23.389900059Z" level=warning msg
="WARNING: No swap limit support"
Oct 19 11:47:23 stapp01.stratos.xfusioncorp.com dockerd[2487]: time="2023-10-19T11:47:23.389955612Z" level=info msg="D
ocker daemon" commit=1a79695 graphdriver=vfs version=24.0.6
Oct 19 11:47:23 stapp01.stratos.xfusioncorp.com dockerd[2487]: time="2023-10-19T11:47:23.390075995Z" level=info msg="D
aemon has completed initialization"
Oct 19 11:47:23 stapp01.stratos.xfusioncorp.com dockerd[2487]: time="2023-10-19T11:47:23.515612358Z" level=info msg="A
PI listen on /run/docker.sock"
Oct 19 11:47:23 stapp01.stratos.xfusioncorp.com systemd[1]: docker.service: Got notification m
essage from PID 2487 (READY=1)
Oct 19 11:47:23 stapp01.stratos.xfusioncorp.com systemd[1]: docker.service: Changed start -> r
unning
Oct 19 11:47:23 stapp01.stratos.xfusioncorp.com systemd[1]: docker.service: Job docker.service
/start finished, result=done
Oct 19 11:47:23 stapp01.stratos.xfusioncorp.com systemd[1]: Started Docker Application Container Engine.
Oct 19 11:47:23 stapp01.stratos.xfusioncorp.com systemd[1]: docker.service: Failed to send uni
t change signal for docker.service: Connection reset by peer
[root@stapp01 ~]# docker version
Client: Docker Engine - Community
 Version:           24.0.6
 API version:       1.43
 Go version:        go1.20.7
 Git commit:        ed223bc
 Built:             Mon Sep  4 12:33:07 2023
 OS/Arch:           linux/amd64
 Context:           default

Server: Docker Engine - Community
 Engine:
  Version:          24.0.6
  API version:      1.43 (minimum version 1.12)
  Go version:       go1.20.7
  Git commit:       1a79695
  Built:            Mon Sep  4 12:32:10 2023
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.6.24
  GitCommit:        61f9fd88f79f081d64d6fa3bb1a0dc71ec870523
 runc:
  Version:          1.1.9
  GitCommit:        v1.1.9-0-gccaecfc
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
[root@stapp01 ~]# 

```


install docker-compose on linux 
https://computingforgeeks.com/how-to-install-latest-docker-compose-on-linux/
```ruby
[root@stapp01 ~]# yum -y install curl wget
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered with an entitlement server. You can use subscription-manager to register.

Last metadata expiration check: 0:09:51 ago on Thu Oct 19 11:42:41 2023.
Package curl-7.61.1-28.el8.x86_64 is already installed.
Dependencies resolved.
======================================================================================================================
 Package                      Architecture            Version                        Repository                  Size
======================================================================================================================
Installing:
 wget                         x86_64                  1.19.5-11.el8                  appstream                  734 k
Upgrading:
 curl                         x86_64                  7.61.1-33.el8                  baseos                     353 k
 libcurl                      x86_64                  7.61.1-33.el8                  baseos                     303 k
Installing dependencies:
 libmetalink                  x86_64                  0.1.3-7.el8                    baseos                      32 k

Transaction Summary
======================================================================================================================
Install  2 Packages
Upgrade  2 Packages

Total download size: 1.4 M
Downloading Packages:
(1/4): libmetalink-0.1.3-7.el8.x86_64.rpm                                             222 kB/s |  32 kB     00:00    
(2/4): curl-7.61.1-33.el8.x86_64.rpm                                                  1.4 MB/s | 353 kB     00:00    
(3/4): libcurl-7.61.1-33.el8.x86_64.rpm                                               2.3 MB/s | 303 kB     00:00    
(4/4): wget-1.19.5-11.el8.x86_64.rpm                                                  2.4 MB/s | 734 kB     00:00    
----------------------------------------------------------------------------------------------------------------------
Total                                                                                 3.1 MB/s | 1.4 MB     00:00     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                              1/1 
  Upgrading        : libcurl-7.61.1-33.el8.x86_64                                                                 1/6 
  Installing       : libmetalink-0.1.3-7.el8.x86_64                                                               2/6 
  Installing       : wget-1.19.5-11.el8.x86_64                                                                    3/6 
  Running scriptlet: wget-1.19.5-11.el8.x86_64                                                                    3/6 
  Upgrading        : curl-7.61.1-33.el8.x86_64                                                                    4/6 
  Cleanup          : curl-7.61.1-28.el8.x86_64                                                                    5/6 
  Cleanup          : libcurl-7.61.1-28.el8.x86_64                                                                 6/6 
  Running scriptlet: libcurl-7.61.1-28.el8.x86_64                                                                 6/6 
  Verifying        : wget-1.19.5-11.el8.x86_64                                                                    1/6 
  Verifying        : libmetalink-0.1.3-7.el8.x86_64                                                               2/6 
  Verifying        : curl-7.61.1-33.el8.x86_64                                                                    3/6 
  Verifying        : curl-7.61.1-28.el8.x86_64                                                                    4/6 
  Verifying        : libcurl-7.61.1-33.el8.x86_64                                                                 5/6 
  Verifying        : libcurl-7.61.1-28.el8.x86_64                                                                 6/6 
Installed products updated.

Upgraded:
  curl-7.61.1-33.el8.x86_64                                libcurl-7.61.1-33.el8.x86_64                               
Installed:
  libmetalink-0.1.3-7.el8.x86_64                               wget-1.19.5-11.el8.x86_64                              

Complete!
[root@stapp01 ~]# curl -s https://api.github.com/repos/docker/compose/releases/latest | grep browser_download_url  | grep docker-compose-linux-x86_64 | cut -d '"' -f 4 | wget -qi -
[root@stapp01 ~]# chmod +x docker-compose-linux-x86_64
[root@stapp01 ~]# mv docker-compose-linux-x86_64 /usr/local/bin/docker-compose
[root@stapp01 ~]# docker-compose version
Docker Compose version v2.23.0
```
