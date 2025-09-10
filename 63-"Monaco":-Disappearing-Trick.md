# Scenario
Description: There is a web server on :5000 with a form. POSTing the correct form password into this web service will return a secret.

Save this secret provided by the web page (not the password you sent to it) to /home/admin/mysolution, for example: echo "SecretFromWebSite" > ~/mysolution

TIP: a developer worked on the web server code in this VM, using the same 'admin' account.

Scenario credit: PuppiestDoggo

# Solution
```
cd ~/.git
git log
-> identify source code of develped server

cat /proc/574/environ
-> get SUPERSECRETPASSWORD=bdFBkE4suaCy

curl -X POST -d "password=bdFBkE4suaCy" http://localhost:5000/
Access granted! Secret is QhyjuI98BBvf

echo "QhyjuI98BBvf" > ~/mysolution
```