# Scenario
Description: Join (merge) all the 338 files in /home/admin/polldayregistrations_enregistjourduscrutin?????.csv into one single /home/admin/all.csv file with the contents of all the CSV files in any order. There should be only one line with the names of the columns as a header.

# Solution
```
cat polldayregistrations_enregistjourduscrutin*.csv > concat.csv

vim concat.csv
:g/Electoral/d
:wq

head -1 polldayregistrations_enregistjourduscrutin24066.csv > heading.txt
cat heading.txt concat.csv > all.csv
```