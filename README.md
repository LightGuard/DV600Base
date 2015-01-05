Title: JBoss Data Virtualization Docker
Author: Kenneth Peeples
Summary: Build a Docker container for running JBoss Data Virtualization.
Level: Intermediate
Technologies: Data Virtualization, Docker
Target Product: datavirt

## dv-docker
This project builds a [docker](http://www.docker.io) container for running [JBoss Data Virtualization](http://http://www.redhat.com/products/jbossenterprisemiddleware/data-virtualization/) 6.0.0.GA.

## Fedora base
Using a Fedora base gives an error message as indicated 

It works properly with centos.  We will do more testing with fedora.
Error:
Redirecting to /bin/systemctl start mysqld.service
Failed to get D-Bus connection: No connection to service manager. 

Related to https://bugzilla.redhat.com/show_bug.cgi?id=1033604

## Prerequisites
1. Install [Docker](https://www.docker.io/gettingstarted/#1)
2. Download JBoss Data Virtualization from [jboss.org.](http://jboss.org/products/#IBP)
2. Put the downloaded file: jboss-dv-installer-6.0.0.GA-redhat-4.jar into dv-docker/software

## Products
1. Red Hat JBoss Data Virtualization 6.0
2. OpenJDK 1.7
3. MySQL
4. PostgreSQL 9.3
5. MongoDB

## Users
1. Fedora: jboss
2. Teiid: user/user with admin,odata,example-role Roles
	
## Building the docker container locally
Once you have [installed docker](https://www.docker.io/gettingstarted/#h_installation) and downloaded the JBoss Data Virtualization software, you should be able to create the JBoss Data Virtualization container via the following command:

If you are on OS X then see How to use [Docker on OS X.](https://github.com/fabric8io/fabric8-docker/blob/master/DockerOnOSX.md)

		$ docker build --rm=true --no-cache -t JBoss-Dockerfiles/DV600Base . 

The JBoss Data Virtualization container then build.

## Try it out
If you have docker installed you should be able to try it out via:

		$ docker run -P -d -t JBoss-Dockerfiles/DV600Base 

This will run the jbossdv600 container and starts automatically JBoss Data Virtualization, PostgreSQL, MySQL and MongoDB.  You can then run **docker attach $containerID** or **docker logs -f $containerID**  to get the logs at any time.	

Run **docker ps** to see all the running containers or **docker inspect $containerID** to view the IP address and details of a container.

## Experimenting
To spin up a shell in the JBoss Data Virtualization containers try:

		$ docker run -P -i -t JBoss-Dockerfiles/DV600Base /bin/bash

You can then noodle around the container and run stuff & look at files etc.

The /home/jboss/run.sh sript can be used to start the databases MongoDB, MySQL, PostgreSQL and JBoss Data Virtualization 6.0.0.GA.
