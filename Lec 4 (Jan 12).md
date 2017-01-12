# Lec 4: Shell Scripts, C++

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

- File: goodPasswordUsage
  ```ruby
  #!/bin/bash
  # Answers whether a candidate word might be a good password
  
  usage() {
    echo "Usage: $0 password" >&2
    exit 1
  }
  
  if [ ${#} -ne 1]; then
    usage
  fi
  
  egrep "^$1$" /usr/share/dict/words > /dev/null
  if [ $? -eq 0 ]; then
    echo "Not a good password"
  else
    echo "Maybe a good password"
  fi
  ```
  __Notes:__
  - function signature: name foolowed by parentheses
  - `${#}`: number of arguments to script
  
## Loops
 - File: Count
   ```ruby
   # count from 1 to $1
   
   #!/bin/bash
    
   x=1
   while [ $x -le $1 ]; do
     echo $x
     x = $((x+1))
   done
   ```
  
 - condition tamplate:
   ```ruby
     if [ condition ]; then
       _________
     elif [ condition ]; then
       _________
     else
       _________
     fi
   ```
    
 - File: rename C
   ```
   [mv hello.c hello.cc]
   ```
   equals
   ```ruby
   filename=hello.c
   mv ${filename} ${filename%c}cc 
   ```
   Note: `%c` remove the prefix
    
   ```ruby
   #!/bin/bash
   #Rename all .c files to .cc
   
   for name in *.c; do
     mv${name} ${name%c}cc
   done
   ```
 
 - How many times does the word $1 appears in the file $2
   ```ruby
   #!/bin/bash
   
   x=0
   for word in $(cat $2); do
    if [$word == "$1"]; then
      x=$((x+1))
    fi
   done
   echo $x
   ```
   
   Good practice: always double quotes the argument in case input becomes something like "To be" which might cause error(comparing a word with {To be} -> syntax error)
   
- payday
  ```ruby
  cal | awk ' { print $6 } ' | egrep "[0-9]" | tail -1
  ```

---------------------------------

## Module 2 C++
  Bjasne Stroustrup
  

  
