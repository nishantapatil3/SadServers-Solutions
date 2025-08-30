# Scenario
Description: There's an Nginx web server running on this machine, configured to serve a simple "Hello, World!" page over HTTPS. However, the SSL certificate is expired.

Create a new SSL certificate for the Nginx web server with the same Issuer and Subject (same domain and company information).

# Solution
Get config of Nginx, check the location of the SSL certificate
```
cat /etc/nginx/sites-available/default
```

Read contents of certificate, get certificate details
```
openssl x509 -in /etc/nginx/ssl/nginx.crt -text -noout
```

Create new certificate
```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/nginx/ssl/nginx.key -out /etc/nginx/ssl/nginx.crt -subj "/CN=localhost/O=Acme/OU=IT Department/L=Geneva/ST=Geneva/C=CH"
```

Restart service
```
sudo systemctl restart nginx
```