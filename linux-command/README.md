## Linux commands with use cases


#####  Prints all lines in www.conf file that start with any character other than <span style="color:red">#</span> and <span style="color:red">;</span>

```sh
$ grep "^[^#;]" www.conf

$ grep '^[[:blank:]]*[^[:blank:]#;]' www.conf # Ignore leading blank characters

$ grep -vxE '[[:blank:]]*([#;].*)?' www.conf

$ awk '$1 ~ /^[^;#]/' www.conf
```