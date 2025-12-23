# Scenario
Description: Inspired by this nixCraft article.

The objective of this exercise is to delete all the Bash history lines that contain the term foo.

Clearing out or deleting the history file /home/admin/.bash_history is not allowed. Note that in our case, new commands (including the ones to try and delete "foo" from history) are also appended to the history file.

# Solution
```
# select history that do not contain word "foo"
grep -v "foo" .bash_history > bash_history.cleaned

# flush the data to bash_history
cat bash_history.cleaned > .bash_history 
```