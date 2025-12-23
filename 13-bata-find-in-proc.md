# Scenario
Description: A spy has left a password in a file in /proc/sys . The contents of the file start with "secret:" (without the quotes).

Find the file and save the word after "secret:" to the file /home/admin/secret.txt with a newline at the end (e.g. if the file contents were "secret:password" do: echo "password" > /home/admin/secret.txt).

(Note there's no root/sudo access in this scenario).

Test: Running md5sum /home/admin/secret.txt returns a7fcfd21da428dd7d4c5bb4c2e2207c4

# Solution
```
grep -r secret 2>/dev/null
```