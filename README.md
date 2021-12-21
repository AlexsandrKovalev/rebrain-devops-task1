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
	> more information can be found on the [developer's website](https://nginx.org/). 
		
###### Supported NGINX functionality

	*HTTP server
	*reverse proxy
	*mail proxy
	*TCP / UDP proxy
	
###### How work nginx?
Unlike a regular web server, Nginx does not create one thread for each request, but splits it into smaller 
structures of the same type, called working connections. Each such connection is processed by a separate 
workflow, and after execution they are merged into a single block that returns the result to the main data 
processing process. One working connection can process up to 1024 requests of the same type at the same time.
	
## Nginx configuration items and architecture

### Important configuration items

###### Nginx architecture
<h4 align="center">
  <img alt="NGINX_work" src="how_work_nginx_2.png">
</h4>

