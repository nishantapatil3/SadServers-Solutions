# Scenario
Description: There is a secret stored in a file that the local Apache web server can provide. Find this secret and have it as a /home/admin/secret.txt file.

Note that in this server the admin user is not a sudoer.

Also note that the password crackers Hashcat and Hydra are installed from packages and John the Ripper binaries have been built from source in /home/admin/john/run

# Solution
```
cat /etc/apache2/sites-enabled

~/john/run/john /etc/apache2/.htpasswd
-> gets username:password

curl localhost -u carlos:chalet
-> no auth error

curl localhost/webfile -u carlos:chalet --file secret.zip
-> get secret.zip

john/run/zip2john secret.zip > zip.hash
john/run/john zip.hash

unzip secret.zip (use password from zip.hash)
-> gets secret.txt
```