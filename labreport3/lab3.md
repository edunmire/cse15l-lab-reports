# Lab Report 3

## Researching Commands

Author: Emma Dunmire

Date: 5/4/2023

**Learning About `grep`**
---

*All of the following information was discovered by using the `man grep` commad in bash.*

*1. Flag `-n`*

The `-n` flag provides line numbers for where the matching text was found in a file.
* Example 1
```
$ grep -n "sodium" pmed.0010051.txt
19:        She had been taking carbamazepine for 17 y and sodium valproate for 13 y for a mixed
26:        6 /l. When the sodium valproate was added, her MCV increased to 112 fl,        
52:        because of her worsening seizures, we increased her sodium valproate dose, increasing her
54:        discontinued her sodium valproate and started her on clonazepam and oxcarbazepine as
64:        stopping her sodium valproate, her appetite improved and she put on 15 lbs over the next 6
77:        of sodium valproate, with the longest interval between the initiation of therapy and the
81:        acute bone marrow suppression and PRCA after 17 y of carbamazepine and 13 y of 
sodium
98:        her brisk reticulocytosis upon discontinuing sodium valproate, were both consistent with
104:        wk) to stopping the drug [6,9]. We believe that the continued use of sodium valproate,
108:        and she gained weight after stopping the sodium valproate. There is a known association
```
* Example 2
```
$ grep -n "age" pmed.0010051.txt
20:        seizure disorder. At age 22 y, before starting any anticonvulsants, her baseline
```

This flag is useful for quickly finding where certain words are mentioned in a text.
In the case of this file, there are 112 lines.
If finding the age of the patient is buried in the text, a quick search using grep shows the line number where the
patients age is located.

*2. Flag `-c`*

The `-c` flag provides a count for where the matching text was found in a file, rather than outputting all the lines.
* Example 1
```
$ grep -c "sodium" pmed.0010051.txt
10
```
* Example 2
```
$ find plos/*.txt > plos-files.txt
$ grep -c "plos/pmed.*.txt" plos-files.txt
150
```

This flag is useful for determining how many occurences of a certain string pattern exist.
In Example 1, this was useful to find how many times a certain word appeared.
In Example 2, the flag could be used on a text file containing file names to determine how many
files with a certain name appeared.

*3. Flag `-v`*

The `-v` flag provides the reverse output of regular call to grep. It will return all the lines
not containing the string provided.
* Example 1
```
$ grep -v "a" plos/pmed.0010051.txt




        PRESENTATION of CASE
        count (WBC), 2.9 × 10
        6 /l (4.8–10.8 × 10
        6 /l (1.5–6.2 × 10
        6 /l (150–350 × 10
        6 /l).
        6 /l.


        Discussion
        nutrient supply.
        elements.
```
* Example 2
```
$ grep -c -v "plos/pmed.*.txt" plos-files.txt        
102
```

This flag is useful for finding lines that do not contain the string, which possibly could be a work-around for ignoring error messages. Example 1 shows a basic use of the flag, and it's interesting to note that `grep -v` will include all empty lines in the output (which is why there is so much blank space in the output). Example 2 demonstrates how to using `-c` and `-v` together can provide a count of how many lines (or files in this case) do not follow the pattern of the string.

*4. Flag `-i`*

The `-i` flag allows grep to not be case sensitive.
* Example 1
```
$ grep -c "H" plos/pmed.0010051.txt
11
$ grep -c -i "H" plos/pmed.0010051.txt
83
```
* Example 2
```
$ find */*/*.txt > technical-files.txt
$ grep -i -c "Media/l" technical-files.txt
19
$ grep -c "Media/l" technical-files.txt
1
```

This flag is useful for determining finding all strings that match, ignoring differences in upper and lower case.
In Example 1, a basic example of the flag is used. It determined how many times an upper case H appeared versus how many lower and upper case H's appeared.
In Example 2, the flag could be used on a text file containing file names to determine how many files with a certain name appeared. In this case, many files began with an upper case L but only one began with a lower case l. The flag allowed for both types to be found. This can be helpful if the person searching is unsure if the files and/or directories contain lower case or upper case letters.
