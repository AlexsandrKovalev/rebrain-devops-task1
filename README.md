<h4 align="center">
  <img alt="NGINX" src="Nginx_logo.png">
</h4>

# Content
1. Information about Nginx
   - About Nginx
     - What is nginx?
	 - Supported NGINX functionality
	 - How work nginx?
   - Nginx configuration items and architecture
	 - Important configuration items
	 - Nginx architecture
2. Install Nginx
3. Example nginx.conf file configuration


# Information about Nginx

## About Nginx

###### What is nginx?
Nginx - is a free web and mail proxy server with non-threaded (asynchronous) architecture and open source.
	> **more information can be found on the [developer's website](https://nginx.org/).** 
		
###### Supported NGINX functionality

* *HTTP server*
* *Reverse proxy*
* *Mail proxy*
* *TCP / UDP proxy*
	
###### How work nginx?
Unlike a regular web server, Nginx does not create one thread for each request, but splits it into smaller 
structures of the same type, called working connections. Each such connection is processed by a separate 
workflow, and after execution they are merged into a single block that returns the result to the main data 
processing process. One working connection can process up to 1024 requests of the same type at the same time.
	
# Nginx configuration items and architecture

## Important configuration items
- worker_processes - the number of worker processes that the server will use. The number must match the number of processor cores.
- worker_connections is the maximum number of connections for each worker process. The higher the indicator, the more people are served at the same time.
- access_log & error_log - These files are used to log any error and access attempts. The logs are examined for troubleshooting and abnormal shutdowns.
- gzip are settings for 'compressing' Nginx requests. Enabling this setting will improve performance. By default, customizations are commented out.
- gzip_comp_level - compression level from 1 to 10. This figure usually does not exceed 6.
_ gzip_types is a list of response types to which compression is applied.


## Nginx architecture


<h4 align="center">
  <img alt="NGINX_work" src="how_work_nginx_2.png">
</h4>

# 2. Install Nginx

## Установка nginx
nginx для каждой операционной системы устанавливается по разному.

## Установка на Linux
To install nginx on Linux, packages from nginx.org can be used. This document will cover installation on Linux

###### installation process:

###### Official Red Hat/CentOS packages

1)To add NGINX yum repository, create a file named /etc/yum.repos.d/nginx.repo and paste one of the configurations below:
  CentOS:
	[nginx]
	name=nginx repo
	baseurl=https://nginx.org/packages/centos/$releasever/$basearch/
	gpgcheck=0
	enabled=1
  RHEL:  
	[nginx]
	name=nginx repo
	baseurl=https://nginx.org/packages/rhel/$releasever/$basearch/
	gpgcheck=0
	enabled=1
	
> **WARNING!** Due to differences between how CentOS, RHEL, and Scientific Linux populate the $releasever variable, it is necessary to manually replace $releasever with either 5 (for 5.x) or 6 (for 6.x), depending upon your OS version.

###### Official Debian/Ubuntu packages

Ubuntu:

The available NGINX Ubuntu release support is listed at this distribution page. For a mapping of Ubuntu versions to release names, please visit the Official Ubuntu Releases page.

Append the appropriate stanza to /etc/apt/sources.list. If there is concern about persistence of repository additions (i.e. DigitalOcean Droplets), the appropriate stanza may instead be added to a different list file under /etc/apt/sources.list.d/, such as /etc/apt/sources.list.d/nginx.list.

	\###Replace $release with your corresponding Ubuntu release.\###
	deb https://nginx.org/packages/ubuntu/ $release nginx
	deb-src https://nginx.org/packages/ubuntu/ $release nginx

###### Установка на FreeBSD
На FreeBSD можно установить nginx либо из пакетов, либо с помощью системы портов. Система портов даёт большую гибкость, позволяя выбирать из широкого набора настроек. Порт скомпилирует nginx с выбранными опциями и установит.

###### Сборка из исходных файлов
Если необходима специфическая функциональность, недоступная из пакетов или портов, можно скомпилировать nginx из исходного кода. Будучи наиболее гибким, этот подход может быть сложным для начинающего. Сборка nginx из исходных файлов освещает этот вопрос более подробно.

3. Example nginx.conf file configuration

Example nginx.conf file configuration you can see in [file](./nginx.conf)

