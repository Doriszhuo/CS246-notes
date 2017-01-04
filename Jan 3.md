
__Jan 3rd__

- Admin Misc
- Linux Shell

_______________________________________

# Module 1 Linux  Shell

__Shell__: interface to the Operating System

- open programs

- manipulate files

## Graphical Shell vs Command line Shell:

| Graphical Shell | Command line Shell |
|:--:|:--:|
| Windows/Mac/Linux | traditional interface to linux |
| intuitive | not intuitive, steep learning curve |
| limited functionality | typing command on prompt |

## A bit about history:

Original unix OS came with a shell

Steven Bourne
  
- CShell, become Turbo C Shell(tcsh)
  
- Korn Shell, become Bourne Again Shell(bash)

_To know what it used: `echo $0`_

## Linux File System

- __Directory__: special files that can hold other files

Linux file system is a tree structure rooted at a directory called the root(root directory: **/**)

                          /
                       /  |  \
                     etc bin home
                      |        |
                     pwd       usr
                             /     \
                         nanaeem  blushman
                            |
                          cs246
                            |
                            a0

- __Path__: specifies the location of a filein the file system

__Absolute path: begins at the root dirctory__

```ruby
ex: /usr/share/dict/words -> 
```

__Relative path: path that begins at the current directory__


## Commands

- `ls` : lists all __no-hidden__ files in the current directory

hidden files: start with a .

list all with hidden: `ls -a`

- `pwd` : present working directory (the directory you are currently sitting in)

- `cd` : changing directory

```ruby
ex: cd /usr/share/dict
```

- `cat` : concatenate, displays contents of a file

```
cat /sur/shell/dot/words
```

- `Ctrl ^C` : kill the program

- `Ctrl ^D` : send __EOF__(end of file)

- `>`: output reditrection

```
cat > output.txt
some words
some more words
^D

cat output.txt
some words
some more words
```









