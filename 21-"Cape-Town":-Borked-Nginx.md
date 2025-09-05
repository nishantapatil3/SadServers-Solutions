# Scenario
Description: There's an Nginx web server installed and managed by systemd. Running curl -I 127.0.0.1:80 returns curl: (7) Failed to connect to localhost port 80: Connection refused , fix it so when you curl you get the default Nginx page.

Test: curl -Is 127.0.0.1:80|head -1 returns HTTP/1.1 200 OK

# Solution
```
# First check the status of the nginx service.
systemctl status nginx

# There is an error in the configuration. Remove the first line and rerun the service.
systemctl restart nginx
# Now the nginx is running but it is giving 500 error.

# There is an error in the application. 

cat /etc/systemd/system/nginx.service

# LimitNOFILE is limited to 10 concurrent reads. Comment it out or increase it to decent number of processes.

systemctl daemon-reload 
systemctl restart nginx


curl -Is 127.0.0.1:80|head -1
```