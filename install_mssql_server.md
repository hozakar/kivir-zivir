
* SQL Server on Ubuntu: https://learn.microsoft.com/en-us/sql/linux/quickstart-install-connect-ubuntu?view=sql-server-ver16
* Do not modify "www.conf" & "php.ini"
* Default username password for sql server: sa / RPSsql12345
* Important in connection string: Trusted_Connection=True
* It may be necessary to: ```sudo ufw allow 1433```
* To install (usually is needed) sqlsrv & pdo_sqlsrv: https://gist.github.com/leidison/e62f7899d54923c32744bb69704524a4
* To change default collation to Turkish:
    * ALTER DATABASE db_name SET SINGLE_USER WITH ROLLBACK IMMEDIATE
    * ALTER DATABASE db_name COLLATE Turkish_CI_AS
    * ALTER DATABASE db_name SET MULTI_USER

