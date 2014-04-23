Bash One Liners
=============

###### Detect Cyrillic In Filenames

```shell
find . | grep -P "[\x80-\xFF]"
```
