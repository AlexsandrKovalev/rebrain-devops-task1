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

<details><summary>What is nginx?</summary>
<p>

Nginx - is a free web and mail proxy server with non-threaded (asynchronous) architecture and open source.
	> **more information can be found on the [developer's website](https://nginx.org/).** 

</p>
</details>
<details><summary>Supported NGINX functionality</summary>
<p>

* *HTTP server*
* *Reverse proxy*
* *Mail proxy*
* *TCP / UDP proxy*
</p>
</details>
<details><summary>How work nginx?</summary>
<p>

Unlike a regular web server, Nginx does not create one thread for each request, but splits it into smaller 
structures of the same type, called working connections. Each such connection is processed by a separate 
workflow, and after execution they are merged into a single block that returns the result to the main data 
processing process. One working connection can process up to 1024 requests of the same type at the same time.
</p>
</details>


# Nginx configuration items and architecture

<details><summary>Important configuration items</summary>
<p>

**Nginx** consists of modules that are configured with directives specified in the configuration file. 
Directives are divided into simple and block directives. A simple directive consists of a name and 
parameters, separated by spaces, and ends with a semicolon (;). A block directive has the same 
structure as a simple directive, but instead of a semicolon after the name and parameters, there 
is a set of additional instructions placed inside curly braces ({and}). If other directives can be 
specified for a block directive inside curly braces, then it is called a context 
(examples: events, http, server and location).

Directives placed in the configuration file outside of any context are considered to be in the main
context. The events and http directives are located in the main context, server in http, and 
location in server.

The part of the line after the # symbol is considered a comment.

| Command | Description |
| --- | --- |
| `user` | Defines _user_ and _group_ credentials used by worker processes. If _group_ is omitted, a group whose name equals that of _user_ is used. |
| `worker_processes` | Defines the number of worker processes. |
| `error_log` | Configures logging. Several logs can be specified on the same configuration level (1.5.2). If on the _main_ configuration level writing a log to a file is not explicitly defined, the default file will be used |
| `pid` | Defines a _file_ that will store the process ID of the main process |
| `events` | Provides the configuration file context in which the directives that affect connection processing are specified. |
| `worker_connections` | Sets the maximum number of simultaneous connections that can be opened by a worker process. |
| `http {...}` | Provides the configuration file context in which the HTTP server directives are specified. |
| `log_format` | Specifies log format. |
| `access_log` | Sets the path, format, and configuration for a buffered log write. Several logs can be specified on the same configuration level. Logging to syslog can be configured by specifying the _syslog_ prefix in the first parameter |
| `include` | Includes another _file_, or files matching the specified _mask_, into configuration. Included files should consist of syntactically correct directives and blocks. |
| `server {...}` | Sets configuration for a virtual server. There is no clear separation between IP-based (based on the IP address) and name-based (based on the ???Host??? request header field) virtual servers. |
| `listen` | Sets the address and port for IP, or the path for a UNIX-domain socket on which the server will accept requests. Both address and port, or only address or only port can be specified. |
| `server_name ` | Sets names of a virtual server |
| `root ` | Sets the root directory for requests. For example, with the following configuration |
| `location / {...} ` | Sets configuration depending on a request URI. |
| `error_page ` | Defines the URI that will be shown for the specified errors. A uri value can contain variables. |
</p>
</details>
<details><summary>Nginx architecture</summary>
<p>

There are 2 algorithms for work synchronous and asynchronous. With the synchronous algorithm, a separate thread is allocated for each stage of the task and the entire operation is performed step by step, that is, the program does not proceed to the next step until it finishes the previous one. Thus, some elements of the system periodically stand idle while waiting for their turn. Hence, there are two disadvantages of such a system:

- irrational use of resources,
- limited number of operations.
- This is how the Apache web server works, for example.

The asynchronous algorithm solved the problems listed above. With an asynchronous algorithm, the code still goes through everything step by step, but the system does not have to wait for one step to complete before moving on to the next. All tasks are carried out in one thread. The program is always aware of the entire process as a whole and can proceed to the next stage when the previous one is not yet completed. Nginx works according to the asynchronous algorithm. Thanks to this approach, working with Nginx allows you to:

- perform more operations,
- work faster
- save memory.

<h4 align="center">
  <img alt="NGINX_work" src="how_work_nginx_2.png">
</h4>
</p>
</details>

# 2. Install Nginx

## Install nginx on Linux
To install nginx on Linux, packages from nginx.org can be used. This document will cover installation on Linux

###### Installation process:
<details><summary>Official Red Hat/CentOS packages</summary>
<p>

###### Red Hat/CentOS packages

1. To add NGINX yum repository, create a file named /etc/yum.repos.d/nginx.repo and paste one of the configurations below:

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

2. To install, use the command `sudo yum install nginx`. We confirm the appeared notification.

3. To start the server, use the command:

	`sudo systemctl start nginx.service`

4. You can check if the installation was successful by visiting the server's public IP address. You can find it out through the command:

	`ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'`

5. To make Nginx automatically start when the OS boots, enter:

	`sudo servicectl enable nginx.service`

</p>
</details>

<details><summary>Official Debian/Ubuntu packages</summary>
<p>

#### Ubuntu:

The available NGINX Ubuntu release support is listed at this distribution page. For a mapping of Ubuntu versions to release names, please visit the Official Ubuntu Releases page.

Append the appropriate stanza to /etc/apt/sources.list. If there is concern about persistence of repository additions (i.e. DigitalOcean Droplets), the appropriate stanza may instead be added to a different list file under /etc/apt/sources.list.d/, such as /etc/apt/sources.list.d/nginx.list.

	## Replace $release with your corresponding Ubuntu release.
	deb https://nginx.org/packages/ubuntu/ $release nginx
	deb-src https://nginx.org/packages/ubuntu/ $release nginx

e.g. Ubuntu 20.04 (Focal Fossa):

	deb https://nginx.org/packages/ubuntu/ focal nginx
	deb-src https://nginx.org/packages/ubuntu/ focal nginx

To install the packages, execute in your shell:

	sudo apt update
	sudo apt install nginx

If a W: GPG error: https://nginx.org/packages/ubuntu focal InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY $key is encountered during the NGINX repository update, execute the following:

	## Replace $key with the corresponding $key from your GPG error.
	sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys $key
	sudo apt update
	sudo apt install nginx

You have now nginx installed on your server but not ready to serve web pages. you have to start the nginx. You can do this by using this command:

	sudo systemctl start nginx

###### Debian 6:

Append the appropriate stanza to /etc/apt/sources.list.

	deb https://nginx.org/packages/debian/ squeeze nginx
	deb-src https://nginx.org/packages/debian/ squeeze nginx

###### Ubuntu PPA
This PPA is maintained by volunteers and is not distributed by nginx.org. It has some additional compiled-in modules and may be more fitting for your environment.

You can get the latest stable version of NGINX from the NGINX PPA on Launchpad: You will need to have root privileges to perform the following commands.

For Ubuntu 20.04 and newer:

	sudo -s
	nginx=stable # use nginx=development for latest development version
	add-apt-repository ppa:nginx/$nginx
	apt update
	apt install nginx

If you get an error about add-apt-repository not existing, you will want to install python-software-properties. For other Debian/Ubuntu based distributions, 
you can try the lucid variant of the PPA which is the most likely to work on older package sets:

	sudo -s
	nginx=stable # use nginx=development for latest development version
	echo "deb http://ppa.launchpad.net/nginx/$nginx/ubuntu lucid main" > /etc/apt/sources.list.d/nginx-$nginx-lucid.list
	apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C300EE8C
	apt update
	apt install nginx

</p>
</details>
<details><summary>Installing on FreeBSD</summary>
<p>
On FreeBSD, you can install nginx either from packages or using the ports system. The port system gives you a lot of flexibility, allowing you to choose 
from a wide range of settings. The port will compile nginx with the selected options and install.
</p>
</details>

<details><summary>Building from source files</summary>
<p>
If you need specific functionality that is not available from packages or ports, you can compile nginx from source. While most flexible, this approach can be tricky for a beginner. Building nginx from source covers this issue in more detail.
</p>
</details>

# 3. Example nginx.conf file configuration

Example nginx.conf file configuration you can see in [file](./nginx.conf)

