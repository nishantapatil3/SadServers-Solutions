# Scenario
Description: Break the Comma Separated Valued (CSV) file data.csv in the /home/admin/ directory into exactly 10 smaller files of about the same size named data-00.csv, data-01.csv, ... , data-09.csv files in the same directory. All the files should have the same header (first line with column names) as data.csv. None of the smaller files should be bigger than 32KB.

Note: unlike the original Minneapolis scenario, here the resulting files have to be proper CSV files.

As a helper tool, you can run the program check_csv.py to check if your data-??.cs files look like proper CSV files.

# Solution
```
import csv

outfile_prefix = "data-"
max_bytes = 1000 * 32 # 32KB

with open("data.csv", "r") as file:
    csv_reader = csv.reader(file)
    
    # get header
    header = next(csv_reader)
    
    file_count = 0
    out_file = f"{outfile_prefix}0{file_count}.csv"
    outfile = open(out_file, 'w', newline='')
    writer = csv.writer(outfile)
    writer.writerow(header)
    current_size = outfile.tell()
    
    for row in csv_reader:
        writer.writerow(row)
        outfile.flush()
        current_size = outfile.tell()
        
        if current_size >= max_bytes:
            outfile.close()
            file_count += 1
            out_file = f"{outfile_prefix}0{file_count}.csv"
            outfile = open(out_file, 'w', newline='')
            writer = csv.writer(outfile)
            writer.writerow(header)
            writer.writerow(row)
            current_size = outfile.tell()
    
    outfile.close()
```

```
awk ' NR==1 {header=$0; next} {     file=sprintf("data-%02d.csv", (NR-2) % 10);      if (NR <= 11) print header > file;      print $0 >> file; } ' data.csv 

```