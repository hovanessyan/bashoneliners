Bash One Liners
=============

## Strings

###### Length of Longest String in a file
```bash
cat strings.txt | wc -L
```
###### Text of Longest String in a file
```bash
awk '{print length($1), $1}' strings.txt | sort -nrk 1 | head -1 | cut -d ' ' -f 2
```
###### Length of Shortest String in a file
```bash
awk '{print length}' strings.txt | sort -n | head -n1
```
###### Text of Shortest String in a file
```bash
awk '{print length($1), $1}' strings.txt | sort -nk 1 | head -1 | cut -d ' ' -f 2
```
###### All strings in a file, with length < 10
```bash
cat test_meaningfull_usernames.txt | while read each; do LEN=`echo $each | wc -m`; if [ $LEN -lt 10 ]; then echo $each; fi; done;
```
###### Remove trailing spaces in files
```bash
vim -c '%s/ *$//g' -c 'wq' /path/to/file
```
---
###### Convert dot separated name in camelCase name "dotToCamelCase.sh"
```bash
line=$1
python -c "func = lambda s: s[:1].lower() + s[1:] if s else ''; result=''.join(item.title() for item in '$line'.split('.')); print func(result)"
```
**Input:**
print.this.shit

**Expression:**
```bash
./dotToCamelCase.sh print.this.shit
```

**Output:**   
printThisShit  

---

###### Swap every two lines in a file

**Input:**  
> firstline1  
secondline1  
firstline2  
secondline2  
firstline3  
> secondline3  

 
**Expression:**
```bash
cat lines.txt | sed -n 'h;n;p;g;p'
```

The **-n** flag suppresses the automatic printing.  
**h** puts copies of the current line from the pattern space to the hold space;  
**n** reads in the next line to the pattern space and **p** prints it;   
**g** copies the first line from the hold space back to the pattern space, bringing the first line back into the pattern space, and **p** prints it.  

**Output:**  
> secondline1  
firstline1  
secondline2  
firstline2  
secondline3  
> firstline3  

_Note:_
If the input has an odd number of lines, the final line will not be output. If output of that line is desired: sed -n '$p;h;n;p;g;p'

---

###### All letters in all lines in a file to lowercase
**Input:**  
> uSerName1  
UserName2  
user_NamE3  
UsEr_NaMe4  
username5  
> uSERName6  

**Expression:**
```bash
cat usernames.txt | tr '[A-Z]' '[a-z]'
```

**Output:**  
> username1  
username2  
user_name3  
user_name4  
username5  
> username6  

---

###### Extracts all lines between two strings

**Task:**Extract the lines between case 4.1 and endcase 4.1

**Input:**  
> Case 4  
case 4.1  
a 3  
a 5  
a 7  
a 1  
a 9  
a 4  
endcase 4.1  
//  
.  
.  
. Do things that dont get parsed  
.  
.  
//  
case 4.2  
a 1  
b 3  
a 6  
b7   
endcase 4.2  
endcase 4  
//  
.  
.  
.  
. More things  
.  
.  
//  
case 5  
.  
.  
.  
.  
> endcase 5  

**Expression:**
```bash
awk '/^case 4.1/,/^endcase 4.1/' ./input.txt > output.txt
```

**Output:**
case 4.1
a 3
a 5
a 7
a 1
a 9
a 4
endcase 4.1

---

###### Sum a column (first) of numbers from a file with AWK

```bash
awk '{ sum += $1 } END { print sum }' /path/to/input/file
```

## Files

###### Detect Cyrillic In Filenames
```bash
find . | grep -P "[\x80-\xFF]"
```

###### Find all files bigger than 100 mb
```bash
find / -type f -size +100000k -exec ls -lh {} \; | awk '{ print $9 ": " $5 }'
```

## Mercurial

###### Remove all .project and .classpath files from repository tree
```bash
find . -type f -name "*.project" -exec hg remove -f {} \;
find . -type f -name "*.classpath" -exec hg remove -f {} \;
```

###### Restore a removed file from Mercurial
**See all revisions that contain file removes**
```bash
hg log -r "removes('**')" --template "{rev}: {file_dels}\n"
```
**grep for specific file to see only it's revision number**
```bash
hg log -r "removes('**')" --template "{rev}: {file_dels}\n" | grep <filename>
```
**recover the file and it's ready for commit again**
```bash
hg revert -r <revNo - 1> <path_to_deleted_file>
```
