# Scenario
Description: There are four Linux users working together in a project in this server: abe, betty, carlos, debora.

First, they have asked you as the sysadmin, to make it so each of these four users can read the project files of the other users in the /home/admin/shared directory, but none of them can modify a file that belongs to another user. Users should be able modify their own files.

Secondly, they have asked you to modify the file shared/ALL so that any of these four users can write more content to it, but previous (existing) content cannot be altered.

# Solution
```
# check file permissions
ls -l shared

# First users need read access to all other files.
sudo chmod +r project_*

# All users should be able to write to ALL file.
sudo groudadd project
sudo usermod -aG project abe
sudo usermod -aG project betty
sudo usermod -aG project carlos
sudo usermod -aG project debora
sudo chown root:project ALL

# ALL files should be appended only.
sudo chmod g+w ALL
sudo chattr +a ALL
```