# Scenario
Description: The goal is to make the script /home/admin/agent/check.sh return OK, without editing the original /etc/hosts file.

Think of testing changes in the critical directory /etc in a safe way. In this case, adding "127.0.0.1 my.local.test" to /etc/hosts .

There would be many ways of trying to do this with "sudo" access, like the usual procedure of making a copy of the config file, editing there and copying or renaming back to the original file. In our case, to avoid all those simple solutions, there is no general "sudo" privileges in this scenario (but there may be for some commands).

# Solution
```
sudo mount
-> works

mkdir -p ~/overlay/etc/{upper,work,merged}

cp /etc/hosts ~/overlay/etc/upper/hosts
echo "127.0.0.1 my.local.test" >> ~/overlay/etc/upper/hosts

sudo mount -t overlay overlay -o lowerdir=/etc,upperdir=$HOME/overlay/etc/upper,workdir=$HOME/overlay/etc/work ~/overlay/etc/merged

sudo mount --bind ~/overlay/etc/merged /etc

./agent/check.sh
OK
```