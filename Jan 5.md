# LEC 2 Redirection, Pipes, Shell Misc

## Last Time

- `cat /usr/share/dict/words`

   command + argument

- `cat`

- `cat > out.txt`   => output redirection

- `Ctrl ^C`  -> kills

- `Ctrl ^D`  -> sends **EOF(End Of File)**

## Output Redirection

In general, 
`command  args  >  file`
shell runs "command" giving it args as arguments and the output of the program is directed to "file".

```ruby
cat < sample.txt
```
Directing input from sample.txt into cat

## Difference:

```
cat sample.txt
```
- sample.txt was an arg to cat
- __cat__ opened and send the contents

```
cat < sample.txt
```
- __shell__ opens sample.txt and send contents to cat

ex: `wc sample.txt`

ouput: 35 278 1494 sample.txt

`wc < sample.txt`

output: 35 278 1494

_________________

`cat < in.txt > out.txt`

copy the contents in in.txt into out.txt

`cat in.txt > out.txt`

cat opened the in.txt, read it and redirect it to the out.txt

`cat in.txt >> out.txt`

appends ouput of the command to the end of out.txt

## Streams
A linux process has 3 streams
```ruby
                                ------------
                                |          | --------> standard output (stdout)  <- use > to change to a file
standard input(stdin)    ------>|  porcess |
  (default keyboard)            |          | --------> standard error (stderr)
                                ------------             (default screen)
  use < to change from                                   use >> to change to file
  keyboard to a file
        
```
`ex: myprog 1 abc < in.txt > out.txt >> error.log`

`cat < in.txt > out.txt >> &1`

## Wildcard Matching

example: `cat *.txt`
            |
            -> **globbing pattern**
            
__\*__ : match anything

__\*.txt__ : match anything end in .txt

The shell detects globbing patterns, does the file matching and replaces the pattern with the matches. (what `cat` will see is a list of files instead of \*.txt) 

#### To disable globbing : `echo '*.txt'` or `echo "*.txt"`

## Pipes

- enables you to connect the stdout of one program to the stdin of another program

```ruby
      ------------
      |          | -->
----->| program 1|       stdin -------------
      |          | ---->-----> |           |----->
      ------------ stdout      | program 2 | 
                               |           |----->                         
                               -------------
```

__Example__ : how many words occur in the first 20 lines of sample.txt

`head -n` gives first n lines

`wc -w` count words

Soln 1: 
```
head -20 sample.txt > temp
wc -w temp
```

Soln 2:
``` 
head -20 sample.txt | wc -w
```

__Example__ : Suppose words1.txt, words2.txt etc contain list of words, one per line. Duplicate free list of all words in words\*.txt

`uniq`: removes adjacent duplicate lines

`sort`: sorts lines

```
cat words*.txt | sort | uniq > file
```

## How to give output of one program as an argument to another? (Command Substitution)

__Example__:

```
echo "Today is $(date) and I am $(whoami)
```
- echo gets 1 argument

```
echo Today is $(date) and I am $(whoami)
```
- echo gets many argument, excutes one by one

```
echo 'Today is $(date)'
```
- prints Today is $(date) (__disable the substitution__)

__*Single quotes prevent embedded while double quoes will not*__


## Searching within a file: egrep (Extended Global Regular Expression Pattern)

- Usage: `egrep pattern file`

```
egrep cs246 index.html
```
outputs lines that contain cs246

```
egrep "CS246|cs246" file

or

egrep (CS|cs)246  file
```
grep `CS246` or `cs246`

__Attention__: `(c|C)(s|S)246` is different (cS246, Cs246)

- `a|b|c|d` is equal to [abcd]

`[...]`: one character from this set

`[^...]`: anyone character __not__ from this set














