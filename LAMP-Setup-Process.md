# LAMP Stack Setup Process on Rocky Linux

## Setup and Install Apache

Update the OS and install the Apache package:
   ```bash
   sudo dnf update -y
   sudo dnf install httpd
  ```

1. Start and enable Apache:
```bash
sudo systemctl start httpd
sudo systemctl enable httpd
```

2. Configure the firewall to allow HTTP (port 80) and HTTPS (port 443) traffic:
```bash
sudo firewall-cmd --permanent --add-port=80/tcp
sudo firewall-cmd --permanent --add-port=443/tcp
sudo firewall-cmd --reload
```

3. Verify Apache's status:
```bash
sudo systemctl status httpd
```
4. Open a web browser and enter IP address. If we get a page that says "HTTP Server Test Page" then it is a success.

## Install MariaDB Server

1. Install MariaDB Server:
```bash
sudo dnf install mariadb-server
```

2. Start and enable MariaDB:
```bash
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

3. Secure MariaDB installation and set root password:
```bash
sudo mysql_secure_installation
```

4. Verify MariaDB's status:
```bash
sudo systemctl status mariadb
```

## Install PHP
1. Enable PHP 8.1:
```bash
sudo dnf module enable php:8.1
```

2. Install PHP and required modules:
```bash
sudo dnf install php php-cli php-gd php-curl php-zip php-mbstring php-mysqlnd -y
```

3. Restart Apache to process PHP requests:
```bash
sudo systemctl restart httpd
```

## Test PHP
1. Create and edit the info.php file:
```bash
sudo nano /var/www/html/info.php
```

2. Add the following code to info.php:
```php
<?php
phpinfo();
?>
```

3. Save the file (Ctrl + O) and exit (Ctrl + X).

4. Restart Apache to apply changes:
```bash
sudo systemctl restart httpd
```

5. Access the info.php page in your browser:
```http
http://server_ip/info.php
```

6. A table with PHP info should appear.
7. After testing, delete info.php from the server.
