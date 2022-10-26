---
title: "FMR Docker with embedded MySQL"
summary: "Easy to use way to get started with Fusion Metadata Registry with a self-contained Docker image"
# Publish date
publishDate: "2022-08-05T00:00:00Z"
# post save as draft
draft: false
# Image
image: "images/containers/docker-fmr.jpg"
# download url
download_url : "https://hub.docker.com/r/metadatatechnology/fmr-mysql"
# sponsor
sponsor : "BIS"
# type
type: "containers"
Topic: "FMR"
---

## Quick start
1. Download and install <a href="https://www.docker.com/products/docker-desktop/" target="_blank">Docker Desktop</a> (if not already installed)

2. Start a Windows Command Prompt or a bash shell and run the following command:

```bash
docker run --name fmr -p 8080:8080 metadatatechnology/fmr-mysql:latest
```

3. Navigate to <a href="http://localhost:8080">http://localhost:8080</a>

4. Log in with username: root and password: password



## Overview

A self-contained Docker image providing everything required for a basic functional FMR installation. It's simple to download and install requring only Docker Desktop or another Docker container runtime. Note that the instructions here are focus on Docker Desktop.

The content is persistent within the container so your structures will still be there even if you stop and restart.

This environment is a single Docker image available from the public <a href="https://hub.docker.com/r/metadatatechnology/fmr-mysql">Docker Hub</a> repository. 

### Key features
- FMR web application and web user interface
- Embedded MySQL operating database for persistent storage of structural metadata
- Single root superuser account for creating and maintaining structural metadata, and administration

### Use cases
- Personal desktop SDMX structural metadata management tool: SDMX structure store, structure authoring and structure maintenance
- SDMX 3.0 structural metadata registry and SDMX data processing engine suitable for light production workloads
- FMR testing and evaluation

### Architecture
- Fusion Metadata Registry 11
- Apache Tomcat Java web application server
- Embedded MariaDB (MySQL compatible) operating database

### System requirements and pre-requisites 
- Windows 10/11, Linux or Apple Mac
- Minimum of 4GB memory

## Download and install

#### Install Docker Desktop
Docker Desktop is a virtual machine for running containerised applications which is free for non-commercial use. 

Downloaded from here: <a href="https://www.docker.com/products/docker-desktop/" target="_blank">https://www.docker.com/products/docker-desktop/</a>

#### Download the image and create a container
Start a Windows Command Prompt or a bash shell and run the following commands.
```bash
docker pull metadatatechnology/fmr-mysql:latest
docker container create --name fmr --publish 8080:8080 metadatatechnology/fmr-mysql:latest
```
## Start up

#### Start the FMR container
``` bash
docker start fmr
```
The container will take between 1 and 2 minutes to start.

Using a normal web browser, navigate to <a href="http://localhost:8080/" target="_blank">http://localhost:8080/</a>

The FMR home page should appear when startup is complete.
{{< figure src="fmr-homepage.png" width="40%">}}

#### Log in using the root superuser account
Log in as the root superuser to start administering the environment. The default credentials are:

- Username: root
- Password: password

It's a good idea to change the default password to something more secure which can be done in the Security section of the admin pages:<br>
<a href="http://localhost:8080/settings/security/rootuseraccount.html">http://localhost:8080/settings/security/rootuseraccount.html</a>

## Shutdown
```bash
docker stop fmr
```
