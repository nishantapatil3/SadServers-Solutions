# Scenario
Description: Break the Comma Separated Valued (CSV) file data.csv in the /home/admin/ directory into exactly 10 smaller files of about the same size named data-00.csv, data-01.csv, ... , data-09.csv files in the same directory. All the files should have the same header (first line with column names) as data.csv. None of the smaller files should be bigger than 32KB.

Note: to simplify, disregard broken lines in your files (ie, you can break a file at any point, not just at a newline). The resulting files don't have to be proper CSV files.

# Solution
Use split command to break data.csv file into n number of smaller files
```
split -d -n 10 data.csv data- breaks the data file into 10 files data-00 to data-09 of 31KB each but only data-00 has the CSV header.
```

Extract headers from first data file which is "data-00.csv"
```
head -1 data.csv > header.txt
```

Append two files such that header appears first
```
for i in {0..9}; do cat header.txt data-0$i > data-0$i.csv; done
```