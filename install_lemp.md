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

```
exit
```

*If remote access to mysql is required*

*To allow access from a specific ip:*
```
sudo ufw allow from remote_ip to any port 3306
```

*To allow access from anywhere:*
```
sudo ufw allow 3306
```

*In MySQL configuration (usually **/etc/mysql/mysql.cnf** or **/etc/mysql/mysql.conf.d/mysqld.cnf**) find the line below and comment it out:*
```
bind-address = 127.0.0.1
```

---

*Install php*
```
sudo apt install php8.1-fpm php-mysql
```

*[Install PHP Modules](https://github.com/hozakar/kivir-zivir/blob/main/install_php_modules.md)*

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

*Customize nginx configuration ( [Simple Nginx Config Example](https://github.com/hozakar/kivir-zivir/blob/main/nginx_config_simple.md) )*
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

