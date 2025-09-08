# Description
Description: A developer created a database named 'main' but now some data is missing in the database. You need to restore the database using the the dump "/home/admin/backup.sql".
The issue is that the developer forgot the root password for the MariaDB server.
If you encounter an issue while restoring the database, fix it.

# Solution
```
$ sudo systemctl stop mariadb

$ sudo systemctl set-environment MYSQLD_OPTS="--skip-grant-tables --skip-networking"

$ sudo systemctl start mariadb

$ sed 's/?/;/g' backup.sql > backup2.sql

$ sudo mysql -u root main < backup2.sql
```