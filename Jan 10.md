# Lec 3

## Last time

1. egrep regexpattern file

  - eg: 
  ```
  egrep cs246 index.html
  ```
  math lines that contain cs246
  ```
  "cs246|CS246"
  ```
  match lines that contain cs246 or CS246

  - _equivalent to `(cs|CS)246`_

  - _not equicalent to `(c|C)(s|S)246` (which also contains cS246 and Cs246)_

2. `a|b|c|d` shortcut: `[abcd]`

  - This means any one characters from this set
  -`[^abcd]`: anyone characters that's not in this set
  
___________________________

## Subexpressions
1. `?` : o or 1 occurance of preceding subexpression

  - `cs ?246`
  
   matches `cs246`, `cs 246`
   
  - `(cs )?246`
  
   matches `246 `, `cs 246`

2. `*`: 0 or more occurances of preceding subespressions
  ```
  (cs)*246
  ```
  matches `246`, `cs246`, `cscs246`, etc
  
3. `+`: 1 or more occurances

4. `.`: any one characters
  
  `.*`: 0 or more any characters
  
 __NOTE__: If by `*` you really want the `*` character, escape it `\*` (same for +, ?, .)

 Examples:
 ``` 
 cs.*246
 ```
 lines that contain strings that start with cs and end with 246

5. Use `^` to indicate line must start with the pattern
  
  `$` to indicate line must end with the pattern
  
  ```
  ^cs.*246$
  ```
  lines start with cs and end with 246
  
Examples: 

1. lines with even length
 ```
 "^(..)*$"
 ```

2. list all files in the current directory, whose name contains exactly one "a" 
 ```
 ls | egrep "^[^a]*a[^a]*$"
 ```
 
3. print all words from the dictionary that start with "e" and consists of 5 characters
 ```
 ^e....$
 ```
 
## Permissions

__`ls -l`: long form listing__

ex: 
```
-rwxr-xr--      1        nanaeem      staff      123          Jan 10          abc.txt

           shorcuts,     owners,     group,     size,  last modified time,  filename
```
For the first 10 bits:`-rwxr-xr--`

**NOTE:**
- **`r`: read**
- **`w`: write**
- **`x`: execute**

and,
- `-`: type
- `rwx`: user(owner)
- `r-x`: group(all members who are in the same group as the file)
- `r--`: others

For a directory:
- `r` means can I see directory contents (whether `ls` will work)
- `w` means can I modify contents fo the directory
- `x` means are you able to enter the directory

## Changing Permissions

- Only the owner can change permisions

```
chmod     mode      file(s)
      /     |     \
     /      |      \
ownership operator  permissions
  class

u user    + add         r
g group   - remove      w
o other   = set         x
a all
```

ex: `g+rw`, `g=rw`, `a=rwx`

Some other ways: `chmod #`
- `chmod 711`: `111001001` => `rwx--x--x`
- `chmod 755`: `111101101` => `rwxr-xr-x`
- `chmod 777`: same as `a=rwx`

--------------------
## Playing with Shell (couldn't come up with a proper title)

```
$> x=1
```
creates a shell variable `x` with the string value of `1`

__NOTE: `x = 1` will not work. Need to be no space__

To recieve the value, $x (better: ${x})












 
 
 
