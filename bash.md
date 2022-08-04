# Quickstart for bash
- https://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html
- https://learnxinyminutes.com/docs/bash/

## Variables
```
variable=1 # no spaces before and after =
```
## Printing / Strings

- Backslash escape character `\`
- Single quotes `'` will preserve all characters
- Double quotes `"` will preserve characters and special functions / subtitutions via dollar sign (`$`), backquote/backtick (`` ` ``), backslash (`\`)  
```
variable="value"
echo "Hello"
echo "Variable: $variable"
echo "Variable: ${variable}"  # Output: "Variable: value"
echo "Variable: \${variable}" # Output: "Variable: ${variable}"
echo 'Variable: ${variable}'  # Output: "Variable: ${variable}"
echo 'Variable: \${variable}' # Output: "Variable: \${variable}"

command="ls"
echo "Run this command: $command"
echo "Output: $($command)" # command substitution
echo "Output: `$command`"  # command substitution
```

## Comments

```
# Comment here
variable="Hello world"  
echo $variable  # Comment
```
**Multiline comments**

```
<<COMMENT
    This is a multiple line comment
    End of the example
COMMENT
```

## Running scripts as files

```
# create file
touch script_file.sh

# edit with editor 
vi script_file.sh

# make file executable
chmod +x script_file.sh 

# run script
./script_file.sh
```

**Example `script_file.sh`**
```
#!/bin/bash
echo "Hello I'm a script"
```
**Example running and output**
```
./script_file.sh
Hello I'm a script
```


## Functions

```
variable="Outside of function"

function functionName()
{
    # scope variable to function and do not override global scope
    local variable=$1;
    local secondArguement=$2;
    echo "Argument is $variable"
}

echo $variable       # "Outside of function"
functionName "abc"   # "Argument is abc"
echo $variable       # "Outside of function"
```


## Conditionals and Loops

### Conditioinal

- `-a file`: True if file exists.
- `-b file`: True if file exists and is a block special file.
- `-c file`: True if file exists and is a character special file.
- `-d file`: True if file exists and is a directory.
- `-e file`: True if file exists.
- `-f file`: True if file exists and is a regular file.
- `-g file`: True if file exists and its set-group-id bit is set.
- `-h file`: True if file exists and is a symbolic link.
- `-k file`: True if file exists and its "sticky" bit is set.
- `-p file`: True if file exists and is a named pipe (FIFO).
- `-r file`: True if file exists and is readable.
- `-s file`: True if file exists and has a size greater than zero.
- `-t fd`: True if file descriptor fd is open and refers to a terminal.
- `-u file`: True if file exists and its set-user-id bit is set.
- `-w file`: True if file exists and is writable.
- `-x file`: True if file exists and is executable.
- `-G file`: True if file exists and is owned by the effective group id.
- `-L file`: True if file exists and is a symbolic link.
- `-N file`: True if file exists and has been modified since it was last read.
- `-O file`: True if file exists and is owned by the effective user id.
- `-S file`: True if file exists and is a socket.
- `file1 -ef file2`: True if file1 and file2 refer to the same device and inode numbers.
- `file1 -nt file2`: True if file1 is newer (according to modification date) than file2, or if file1 exists and file2 does not.
- `file1 -ot file2`: True if file1 is older than file2, or if file2 exists and file1 does not.
- `-o optname`: True if the shell option optname is enabled. The list of options appears in the description of the -o option to the set builtin (see The Set Builtin).
- `-v varname`: True if the shell variable varname is set (has been assigned a value).
- `-R varname`: True if the shell variable varname is set and is a name reference.
- `-z string`: True if the length of string is zero.
- `-n string`, `string`: True if the length of string is non-zero.
- `string1 == string2`, `string1 = string2`: True if the strings are equal. `=` should be used with the test command for POSIX conformance.
- `string1 != string2`: True if the strings are not equal.
- `string1 < string2`: True if string1 sorts before string2 lexicographically.
- `string1 > string2`: True if string1 sorts after string2 lexicographically.
- `arg1 OP arg2`: OP is one of `-eq`, `-ne`, `-lt`, `-le`, `-gt`, or `-ge`. These arithmetic binary operators return true if arg1 is equal to, not equal to, less than, less than or equal to, greater than, or greater than or equal to arg2, respectively. Arg1 and arg2 may be positive or negative integers. When used with the [[ command, Arg1 and Arg2 are evaluated as arithmetic expressions (see Shell Arithmetic).


### If / Else

```
if [ "a" = "$b" ]; then
  echo "hi"
elif [ "b" = "$b" ]; then
  echo "hi BB"
else
  echo "no match"
fi
```

## Switch / Case

```
case $ANIMAL in
  horse | dog | cat) echo "four feet";;
  man | kangaroo ) echo "two feet";;
  *) echo "an unknown number of feet";;
esac
```

## While loops

```
i=4
while [ $i -gt 1 ] ; do
  echo "loop $i";

  i=$(expr $i - 1)

  if [ $i -eq 2 ]; then
    break;
  fi
done;
```

## For loops

```
for name in joey suzy bobby;do echo $name;done
```

```
for name in joey suzy bobby;do
  echo $name;
done
```

```
for i in web{0..10};do
   echo ${i};
done;
```

### Multiple Conditions

```
if [ $a -lt 2 ] || [ $a -gt 10 ]; then  
  echo "hi";
fi

if [[ $a -lt 2 || $a -gt 10 ]]; then  
  echo "hi";
fi

if [ $a -gt 2 ] && [ $a -lt 10 ]; then  
  echo "hi";
fi
```


## Math
- https://askubuntu.com/a/939299/14930

```
$(($i + 1))    # arithmetic expansion `echo $(($i + 1))`
(($i + 1))     # arithmetic expression for conditionals e.g. `if (($i + 1)); then`
```

**Other syntax**
```
$[$i+1]        # old deprecated arithmetic expansion  `echo $[$i+1]`
let a=1+1      # `let` keyword is specific to certain shells for variable assignment
$(expr 1 + 1)  # uses `expr` to evaluate `echo $(expr 1 + 1)`
```

### Math Operators

- `id++`, `id--`: variable post-increment and post-decrement
- `++id`, `--id`: variable pre-increment and pre-decrement
- `-`, `+`: unary minus and plus
- `!`, `~`: logical and bitwise negation
- `**` : exponentiation
- `*`, `/`, `%`: multiplication, division, remainder
- `+`, `-`: addition, subtraction
- `<<`, `>>`  : left and right bitwise shifts
- `<=`` >=`, `<`, `>`: comparison
- `==`, `!=`: equality and inequality
- `&`  : bitwise AND
- `^`  : bitwise exclusive OR
- `|` : bitwise OR


## Environment variables

- `env` view variables

## Override variable values in function scope

```
VARIABLE1=VALUE1 VARIABLE2=VALUE2 function_name
```


```
variable="I'm a variable"

function afunction()
{
    echo "In function: $variable"
}

echo $variable                   # I'm a variable
afunction                        # In function: I'm a variable
variable="Yes you are" afunction # In function: Yes you are
afunction                        # In function: I'm a variable
echo $variable                   # I'm a variable
```

* * * 

## Count lines, words, characters

```
wc     # get count of lines, words and characters
wc -l  # line count
wc -w  # word count
wc -c  # character count
```

```
echo "Hello\nCount my lines, words and characters" | wc
       2       7      43
echo "Hello\nCount my lines, words and characters" | wc -l
       2
echo "Hello\nCount my lines, words and characters" | wc -w
       7
echo "Hello\nCount my lines, words and characters" | wc -c
      43
```

## Sorting

```
sort 

sort -r     # reverse
sort -f     # ignore case
sort -V     # version
sort -n     # numeric
sort -u     # unique
```


## Getting Unique values

```
uniq

uniq -i     # ignore case
```

## Display first/last part of file

```
head         # display first/top part of file
head -n 40   # specify number of lines to display

tail         # display last/end part of file
tail -n 40
tail -f      # follow file and display new data as it comes in
```

## Display contents of file

```
cat FILENAME
zcat GZIPPED_FILE           # extract gzip file and cat resulting files
cat -n FILENAME             # display line numbers
cat -v FILENAME             # display non-printible characters
cat -t FILENAME             # display non-printible characters including tab characters
cat file1 file2 > file3     # combine file1 and file2 into file3
cat file1 >> file3          # append file1 into file3 (create file3 if doesn't exist)
```

## Cut

```
cut -c LIST        # cut by character
cut -f LIST        # by field (default delimiter is tab) 
cut -f LIST -d " " # by field specifying new delimieter

# LIST is a range e.g. start1-end1,start2,start3-end3
```

```
ls -l | cut -c 1-11,31-35
echo "A\tB\tC\tD" | cut -f 1-3           # A       B       C
echo "A B C D"    | cut -f 1,2 -d " "    # A B
echo "A  B C D"   | cut -f 1,2 -d " "    # A
```

## Pattern Matching / Find Text with `grep`

- Finds text that matches pattern and prints entire line

```
grep PATTERN FILE_OR_DIRECTORY
cat FILE | grep PATTERN
```

```
grep -i         # case insensitive
grep -a         # treat files as ASCII text
grep -r / -R    # recursive search for directory searching `grep -R "test" *`
grep -v         # invert match: find all that don't match pattern
grep -A num     # show `num` lines after match
grep -B num     # show `num` lines before match
grep --colour   # highlight matches
grep -n         # show line numbers
grep -E 'pattern1|pattern2'    # search multiple patterns
```

## Pattern Matching / Find Text with custom output with `awk`

- Finds text that matches pattern and prints custom output

```
awk PATTERN_AND_ACTION file 
cat file | awk PATTERN_AND_ACTION

awk -F 'REGEX'   # specify custom field delimiter
```

```
ls -l | awk '{ print $0 }'    # print entire line
ls -l | awk '{ print $5 }'    # print 5th field
ls -l | awk '{ 
  if ($5 > 1000) 
    print "Big one " $0
  else if ($5 > 400)
    print "Medium one. Size: " $5 ", File: " $9
  else
    print "Small"
}' 
ls -l | awk -F '[rw]|user' '{print $1 "  " $2  "  " $3}'
```


## Text Replacemment with `sed`

- Replace text

```
sed 's/regexSearch/regexReplace/regexFlags' FILE
cat FILE | sed 's/regexSearch/regexReplace/regexFlags'
```

```
sed 's/root/user/ig' file
ls -l | sed 's/\([a-zA-Z0-9][a-zA-Z0-9]*\) \([a-zA-Z0-9][a-zA-Z0-9]*\)/\2 \1/'
```