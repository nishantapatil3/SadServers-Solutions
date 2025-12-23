# Scenario
Description: There's a web server running on this host but curl localhost returns the default 404 Not Found page.

Fix the issue so that a file is served correctly and the message Welcome to the Real Site! is returned.

Test: Running curl localhost should return HTTP 200 with the message Welcome to the Real Site!.

# Solution
```
# find what is running
ps aux

# nginx is serving html, so get its config
cat /etc/nginx/sites-available/default

# nginx is serving index.html at /var/www/html/, so check its owner and fix it
sudo chusr root:www-data /opt/site-content/real_index.html

# check others execute permissions on www directory and fix it, so that other users can access it

# add execute to www directory
sudo chmod +x /var/www
```