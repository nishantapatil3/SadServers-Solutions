# Scenario
Description: (Similar to "Manhattan" scenario but harder). Your objective is to be able to insert a row in an existing Postgres database. The issue is not specific to Postgres and you don't need to know details about it (although it may help).

Postgres information: it's a service that listens to a port (:5432) and writes to disk in a data directory, the location of which is defined in the data_directory parameter of the configuration file /etc/postgresql/14/main/postgresql.conf. In our case Postgres is managed by systemd as a unit with name postgresql.

# Solution
```
systemctl status postgresql

journalctl -u postgresql
-> observe where file access id denied
-> /opt/postgres

# check if ther is a disk that is not mounted
lsblk -f

# nvme0n1p1 is not mounted
mount /dev/nvme0n1p1 /opt/postgres

# check if there is enough space
df -h
nvme0n1p1 -> 100% usage
cd /opt/postgres %% rm file*.blk

# now this will work
sudo -u postgres psql -c "insert into persons(name) values ('jane smith');" -d dt
```