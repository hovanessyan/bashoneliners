Bash One Liners
=============

## Strings

###### Detect Cyrillic In Filenames

```bash
find . | grep -P "[\x80-\xFF]"
```

###### Length of Longest String in a file

```bash
cat strings.txt | wc -L
```
