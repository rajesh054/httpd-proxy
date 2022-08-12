# httpd-proxy
This document include the setup for how to use the httpd-proxy docker image

On Docker Hub there apache proxy images are very outdated.
This document will help you create and use a reverse-proxy container to  server any applications, like ReactJS, NextJS ,Springboot etc

 You can use the below instructions to make a httpd-proxy container with the latest version of apache

1) Download the docker file and httpd.conf file in the repo

2) open the httpd.conf file and edit the virtualhost config as show below
<VirtualHost *:80>
    ServerName www.example.co.in     # Replace example.co.in with URL on which the site as to be hosted
    DocumentRoot "/usr/local/apache2"
    ServerSignature off
    ProxyPreserveHost On
    ProxyRequests Off
    TimeOut 300
    ProxyTimeout 300
    ProxyPass / http://IP:3000/       #Replace IP with docker container IP of nextjs or react container. U can also use container name instead of IP
    ProxyPassReverse / http://IP:3000/
    
</VirtualHost>

Save the file 

3) Build a docker Image using the docker file given in repository

docker build -t (name of image)  -f Dockerfile2 .

4) Now run the container 

docker container run  --name (ContainerName)  -d --network localnetwork -p 8088:80 rajesh054/httpd-proxy


Note: In the above command we used a custom bridge network , Advantage of using a custom bridge network is that, all container can recogine themselve with there container name (DNS). It helps in giving DNS or Container Name in proxy url instead of IP.


*** Other Way to use the httpd conf file with httpd image is to mount local httpd.conf file to the httpd.conf file inside the container which helps to add multiple proxy urls with ease.

Please view the document in RAW format, Due to formating issue
