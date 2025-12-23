# Scenario
Description: Mary and John are working on a Golang web application, and the security team has asked them to implement security measures. Unfortunately, they have broken the application, and it no longer functions. They need your help to fix it.

The fixed application should be able to allow clients to communicate with the application over HTTPS without ignoring any checks. (eg: curl https://webapp:7000/users.html) and serve its static files.

# Solution
```
sudo systemctl status webapp.service
sudo systemctl status webapp.service

cd /home/webapp/
sudo chown webapp:webapp pki
sudo chmod +r pki/server.*

sudo chown -Rv webapp.webapp /home/webapp/static-files
sudo chmod -Rv 0640 /home/webapp/static-files/*


sudo cp -v /home/webapp/pki/CA.crt /usr/local/share/ca-certificates/CA.crt
sudo chmod 0644 /usr/local/share/ca-certificates/CA.crt
sudo update-ca-certificates

echo QUIT | openssl s_client -connect localhost:7000 -showcerts 2>/dev/null | openssl x509 -noout -subject -ext subjectAltName

sudo vim /etc/apparmor.d/usr.local.bin.webapp
add => 
/home/webapp/static-files/ r,
/home/webapp/static-files/* r,

sudo systemctl status apparmor.service
sudo systemctl restart apparmor.service

``