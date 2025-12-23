# Scenario
Description: Given the file user_list.txt you must create all the users specified in the file with their corresponding passwords.

The entries in the user_list.txt file are stored as username;password

# Solution
```
while IFS=';' read -r user pass; do
  if [[ -n "$user" && -n "$pass" ]]; then
    sudo useradd -m "$user"
    echo "$user:$pass" | sudo chpasswd
    echo "$user added"
  else
    echo "Skipping line with missing user or password: '$user';'$pass'"
  fi
done < user_list.txt
```