# Lec 4: Shell Scripts, C++(Hopefully) 

## Last time
- egrep
- file permissions
- shell variables

-------------

A script has access to the first argument using `$1`, second argument using `$2` and so on.

- `$0`: the way the script was called

- examples: (egrep the input from the dictionary)
  ```ruby
  #!/bin/bash
  egrep "^$1$" /sur/share/dict/words
  ```



- __NOTES:__
  1. `/dev/null` is a file to which you can direct output to be discarded (like a "black hole")
  2. every process returns a status code:
    - `0`: for success
    - non-zero: for failure
  3. The status code is stored in `$?`
  4. __Test Program__: `[ $? -eq 0 ]`    --> `-eq`: integer compare
    
- eg: A good password is not in the dictionary. Is the given password any good
  ```ruby
  #!/bin/bash
  egrep "^$1$" /usr/share/dict/words > /dev/null
  if [ $? -eq 0 ]; then
    echo "Not a good password"
  else
    echo "Maybe a good password"
  fi
  ```
