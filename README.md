Bash One Liners
=============

###### Detect Cyrillic In Filenames

```bash
find . | grep -P "[\x80-\xFF]"
```
