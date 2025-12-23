# Scenario
Description: Can't ping google.com. It returns ping: google.com: Name or service not known. Expected is being able to resolve the hostname. (Note: currently the VMs can't ping outside so there's no automated check for the solution).

# Solution
```
vim /etc/nsswitch.conf

add `dns` to `hosts:` line
```