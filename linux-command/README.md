# Linux important commands 


#### How to show lines in a files that does not strat with some prefix.  Let say I want show all the lines in www.conf file without the lines that are comment out. It means show the line that are not start with ';' or '#' We can do that in many ways, I like the below two soluntions 

```sh
$ grep "^[^#;]" www.conf

$ grep '^[[:blank:]]*[^[:blank:]#;]' www.conf # Ignore leading blank characters

$ grep -vxE '[[:blank:]]*([#;].*)?' www.conf

$ awk '$1 ~ /^[^;#]/' www.conf
```