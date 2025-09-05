# Scenario
Description: Find in the file frankestein.txt the second most frequent word and save in UPPER (capital) case in the /home/admin/mysolution file.

A word is a string of characters separated by space or newlines or punctuation symbols .,:; . Disregard case ('The', 'the' and 'THE' is the same word) and for simplification consider the apostrophe as another character not as punctuation ("it's" would be a word, distinct from "it" and "is"). Also disregard plurals ("car" and "cars" are different words) and other word variations (don't do "stemming").

We are providing a shorter test.txt file where the second most common word in upper case is "WORLD", so we could save this solution as: echo "WORLD" > /home/admin/mysolution

This problem can be done with a programming language (Python, Golang and sqlite3) or with common Linux utilities.

# Solution
```
# Find the second most frequent word in a txt file
import collections

with open("frankestein.txt", "r") as file:
    string_to_split = file.read()
    
    string_to_split = string_to_split.replace(" ", "$")
    string_to_split = string_to_split.replace("\n", "$")
    string_to_split = string_to_split.replace(".", "$")
    string_to_split = string_to_split.replace(",", "$")
    string_to_split = string_to_split.replace(":", "$")
    string_to_split = string_to_split.replace(";", "$")
    
    words = [w for w in string_to_split.split("$") if w]
    
    count = collections.Counter(words)
    
    count_arr = [(k,v) for k,v in count.items()]
    
    count_arr.sort(key=lambda x:x[1])
    
    print(count_arr[-2])
```