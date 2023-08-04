# LEMP

```
sudo apt update
```
```
sudo apt install nginx
```

---

```
sudo ufw allow 'Nginx Full'
```
```
sudo ufw allow 'OpenSSH'
```

---

*Install MySQL*
```
sudo apt install mysql-server
```
```
sudo mysql_secure_installation
```

*Connect to MySQL*
```
sudo mysql
```

*Create DB*
```
CREATE DATABASE new_db;
```

*Create user*
```
CREATE USER 'new_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
```

*Give permissions to new user*
```
GRANT ALL ON new_db.* TO 'new_user'@'%';
```

*Exit from MySQL cli*

```exit```

---

*Install php*
```
sudo apt install php8.1-fpm php-mysql
```

*Install php modules...*

---

*Create root for domain(s)*
```
sudo mkdir /var/www/domain.tld
```

*Add user for domain*
```
sudo adduser username
```

*chown new user to domain root*
```
sudo chown -R username:username /var/www/domain.tld
```

*Customize nginx configuration (example)*
```
sudo nano /etc/nginx/sites-available/domain.tld
```

*Link configuration to sites-enabled*
```
sudo ln -s /etc/nginx/sites-available/domain.tld /etc/nginx/sites-enabled/
```

*Test nginx conf*
```
sudo nginx -t
```

*Reload nginx*
```
sudo systemctl reload nginx
```

