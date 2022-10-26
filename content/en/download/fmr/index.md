---
title: "Fusion Metadata Registry"
summary: "SDMX structural metadata registry with structure maintenance UI and data processing services"
# Publish date
publishDate: "2022-10-14T00:00:00Z"
# post save as draft
draft: false
# Image
image: "images/products/fmr.png"
# download url
download_url : "https://hub.docker.com/r/metadatatechnology/fmr-mysql"
# sponsor
sponsor : "BIS"
# type
type: "download"
Topic: "Registry"
---

## Built Java web application
The FMR built Java application is supplied as a WAR file (web application archive) ready for deployment to a Java web application server. Apache Tomcat, Oracle Web Logic and RedHat JBoss are supported.

| Version | Release date | Download |
|---------|----------------|-------------------------------------------------------------------------|
|11.4.0   | 14 Oct 2022 | https://sdmxio.s3.eu-west-2.amazonaws.com/FusionMetadataRegistry/FusionMetadataRegistry-11.4.0.zip|
|11.3.0   | 26 Sep 2022 | https://sdmxio.s3.eu-west-2.amazonaws.com/FusionMetadataRegistry/FusionMetadataRegistry-11.3.0.zip|
|11.2.2   | 13 Sep 2022 | https://sdmxio.s3.eu-west-2.amazonaws.com/FusionMetadataRegistry/FusionMetadataRegistry-11.2.2.zip|
|11.2.1   | 09 Sep 2022 | https://sdmxio.s3.eu-west-2.amazonaws.com/FusionMetadataRegistry/FusionMetadataRegistry-11.2.1.zip|
|11.2.0   | 22 Jul 2022 | https://sdmxio.s3.eu-west-2.amazonaws.com/FusionMetadataRegistry/FusionMetadataRegistry-11.2.0.zip|
|11.1.5   | 01 Jun 2022 | https://sdmxio.s3.eu-west-2.amazonaws.com/FusionMetadataRegistry/FusionMetadataRegistry-11.1.5.zip|


## Docker
An {{% link "containers/fmr-docker-mysql"%}}FMR Docker image{{%/link%}} is also available as an alternative to downloading and installing the Java web application. Docker provides a fully working FMR installation in less than 10 minutes suitable for testing, personal use and light production workloads.

The rest of this article refers to the installing the FMR Java web application directly onto a machine.

## Changelog
FMR changelog: https://fmrwiki.sdmxcloud.org/Change_Log

## System requirements
- Windows, Linux or Apple Mac 
- Minimum 4GB memory - additional memory could be required if processing large datasets or storing large volumes of metadata
- Minimum 2 core CPU
- Optionally a Microsoft Active Directory or LDAP service for user authentication

## Installation instructions
https://fmrwiki.sdmxcloud.org/Quick_start_guide_-_Windows,_Linux_or_Mac
 
## Prerequisites
FMR is a Java web application which requires the following:
- Java runtime environment. <a href="https://www.java.com/en/">Oracle Java</a> or <a href="https://docs.aws.amazon.com/corretto/latest/corretto-11-ug/downloads-list.html">Amazon Corretto</a> are good options.
- Java web application server. <a href="https://tomcat.apache.org/download-90.cgi">Apache Tomcat 9.0</a> is recommended. Other options include JBoss and Oracle WebLogic.
- SQL database. <a href="https://dev.mysql.com/downloads/mysql/">MySQL 8</a>, Microsoft SQL Server or Oracle are supported.

## MySQL installation notes
From release 11.4.0, the MySQL database connector (otherwise known as the JDBC driver) is no longer bundled with the FMR distribution and must be installed separately. The following article explains how to obtain and install the connector https://fmrwiki.sdmxcloud.org/Install_MySQL#Obtaining_and_Specifying_the_MySQL_JDBC_Driver

## Source code
Contact us at contact@sdmx.io for access to the source code


