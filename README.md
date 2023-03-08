# Cloud Computing Document

## Cloud Service chose:

### LINODE:

- Linode is a cloud hosting provider that offers virtual private servers (VPS) for developers and businesses.
- Linode provides a range of cloud computing services including Linux VPS hosting, managed Kubernetes, object storage, and more.
- Another key advantage of Linode is its affordability.
- Overall, Linode is a reliable and affordable cloud hosting provider that offers a range of services for developers and businesses.

## Specifications of the Virtual Machine:

- vCPU cores: 4 CPU cores (Shared).
- Memory: 8 GB RAM.
- SSD Storage: 100 GB.
- Transfer: 5 GB.
- Network In: 1 Gbps.
- Network Out: 2 Gbps.
- Dedicated IPv4 and IPv6 addresses.
- Standard Linux Distributions (Ubuntu).

## Price for the above mentioned specs in LINNODE:

- $40/month

## Process involved in deploying https://exceptions.rvce.edu.in project:

### Accessing to the root server using ssh

```sh
ssh rvce@ip
```

### Installing a web server to deploy our application:

- Nginx is the web server we did install to deploy our application which is powered through REACTJs

```sh
sudo apt install nginx
```

### Creating a folder where our project's source code is going to live:

```sh
sudo mkdir /var/www/exceptions.rvce.edu.in
```

### Changing the permission and ownership of the above created folder

```sh
sudo chmod 755 -R /var/www/exceptions.rvce.edu.in
sudo chown -R rvce:www-data /var/www/exceptions.rvce.edu.in/
```

### Creating a configuration file for nginx:

```sh
sudo nano /etc/ngnix/site-available/exceptions.rvce.edu.in
```

### Adding the following code in the exceptions.rvce.edu.in file:

```js
server {
    listen 80;
    listen [::]:80;

    root /var/www/exceptions.rvce.edu.in;
    index index.html;
}
```

### Unlinking the default config file:

```sh
sudo unlink /etc/nginx/sites-enabled/default
```

### Linking the config file which we have created:

```sh
sudo ln -s /etc/nginx/sites-available/exceptions.rvce.edu.in /etc/nginx/sites-enabled/
```

### Restarting the nginx:

```sh
sudo systemctl restart nginx
```

### Testing nginx if it's working:

```sh
sudo nginx -t
```

The above mentioned process is enough to deploy any React application, one can easily deploy their app using a scp command as below:

```sh
scp -r dist/* rvce@exceptions.rvce.edu.in:/var/www/exceptions.rvce.edu.in/
```

Although the application will be deployed but it will be following `http` protocol not safe

The following steps involves in transfering `http` to `https`:

## Configuring Firewall rules with UFW:

### Installing ufw:

```sh
sudo apt install ufw
```

### Add firewall rules to allow ssh (port 22) connections as well as http (port 80) and https (port 443) traffic.

```sh
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https
```

### Enable UFW if its not already enabled

```sh
sudo ufw enable
```

### Verify that UFW is enabled and properly configured for ssh and web traffic.

```sh
sudo ufw status
```

### Installing certbot using snap:

```sh
sudo snap install --classic certbot
```

### Configure a symbolic link to the Certbot directory using the ln command.

```sh
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```

### Requesting a TLS/SSL Certificate Using Certbot

```sh
sudo certbot --nginx
```

### Enter email address.

### Accept terms of service.

### Optionally subscribe to mailing list.

### Enter domain name(s).

```sh
exceptions.rvce.edu.in
```

Now we have successfully installed ssl certificate to our deployed application

Hence our application is easily accessible and will be running with `https` protocol

## References:

- [linode-specifications](https://www.linode.com/products/shared/)
- [installing-ssl-certificate](https://www.linode.com/docs/guides/enabling-https-using-certbot-with-nginx-on-ubuntu/)
