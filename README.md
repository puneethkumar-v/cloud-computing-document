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
