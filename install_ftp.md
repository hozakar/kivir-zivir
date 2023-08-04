# Ftp Server

`
sudo apt update
`

`sudo apt install vsftpd`

`sudo systemctl start vsftpd`

`sudo systemctl enable vsftpd`

---

*Backup conf file (better safe than sorry)*
`sudo cp /etc/vsftpd.conf  /etc/vsftpd.conf_default`

 ---
 
*Open ports for ftp traffic*
`sudo ufw allow 20/tcp`

`sudo ufw allow 21/tcp`

---

*Configuration*
`sudo nano /etc/vsftpd.conf`

---

*In conf file*
`local_enable=YES`
`write_enable=YES`
`chroot_local_user=YES`
`user_sub_token=$USER`
`local_root=/var/www/$USER`
`pasv_min_port=40000`
`pasv_max_port=50000`
`userlist_enable=YES`
`userlist_file=/etc/vsftpd.userlist`
`userlist_deny=NO`

*For user list*
`sudo nano /etc/vsftpd.userlist`

---

*If you want to enable encryption*
`sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/vsftpd.pem -out /etc/ssl/private/vsftpd.pem`

*In conf file*
`rsa_cert_file=/etc/ssl/private/vsftpd.pem`
`rsa_private_key_file=/etc/ssl/private/vsftpd.pem`
`allow_anon_ssl=NO`
`force_local_data_ssl=YES`
`force_local_logins_ssl=YES`
`ssl_tlsv1=YES`
`require_ssl_reuse=NO`
`ssl_ciphers=HIGH`

---

`sudo systemctl restart vsftpd.service`