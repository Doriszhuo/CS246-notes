# Lec 4: Shell Scripts, C++(Hopefully) 

## Last time
- egrep
- file permissions
- shell variables
-------------

A script has access to the first argument using $1, second argument using $2 and so on.

- $0: the way the script was called

```ruby
#!/bin/bash
egrep "^$1$" /sur/share/dict/words
```
