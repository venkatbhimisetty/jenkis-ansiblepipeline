https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-ubuntu-18-04


Step 1.1 . Installing the Nginx Web Server
	sudo apt update
	sudo apt install nginx

Step 1.2. Enable ufw for NGINX
	sudo ufw allow 'Nginx HTTP'
	sudo ufw status

step 1.3. Know your server's public IP address
	ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'

         or use
        curl -4 icanhazip.com

	http://server_domain_or_IP

Step 2.1 . Installing MySQL to Manage Site Data
	sudo apt install mysql-server
	sudo mysql_secure_installation
	sudo mysql
	SELECT user,authentication_string,plugin,host FROM mysql.user;
	ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
	FLUSH PRIVILEGES;

Step 3.1 sudo nano /etc/nginx/sites-available/example.com

Step 3.2 sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/

Step 3.3 sudo unlink /etc/nginx/sites-enabled/default

Step 3.4 sudo nginx -t

Step 3.5 sudo systemctl reload nginx

Step 4.1 http://your_server_domain_or_IP/


https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-nginx-in-ubuntu-18-04

How To Create a Self-Signed SSL Certificate for Nginx in Ubuntu 18.04 


Step 1.1 . Creating the SSL Certificate

	sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/certs/nginx-selfsigned.crt

Step 1.2. sudo openssl dhparam -out /etc/nginx/dhparam.pem 4096



Step 2.1 . Configuring Nginx to Use SSL

	sudo nano /etc/nginx/snippets/self-signed.conf

	sudo nano /etc/nginx/snippets/ssl-params.conf

Step 2.2 sudo cp /etc/nginx/sites-available/example.com /etc/nginx/sites-available/example.com.bak


Step 3.1 . Adjusting the Firewall
	sudo ufw app list
	sudo ufw status
	sudo ufw allow 'Nginx Full'
    	sudo ufw delete allow 'Nginx HTTP'


Step 3.2 Enabling the Changes in Nginx
	sudo nginx -t
	sudo systemctl restart nginx

Step 4.1 . Testing Encryption
	https://server_domain_or_IP
	

Step 5 . Changing to a Permanent Redirect	

	sudo nano /etc/nginx/sites-available/example.com

	Find the return 302 and change it to return 301:
	/etc/nginx/sites-available/example.com   ----->	 return 301 https://$server_name$request_uri;

	sudo nginx -t
	sudo systemctl restart nginx


