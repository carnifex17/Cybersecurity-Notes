# Bash Scripting Basics

**Bash is the scripting language we use to communicate with Unix-based OS and give commands to the system.**

---

#### Script Execution - Examples
```bash
carnifex17@kali[/kali]$ bash script.sh <optional arguments>
carnifex17@kali[/kali]$ sh script.sh <optional arguments>
carnifex17@kali[/kali]$ ./script.sh <optional arguments>
```
---

#### Shebang
The `#!/bin/bash` at the beginning of a Bash script is known as a shebang or hashbang. It serves as a directive to the operating system, indicating which interpreter should be used to execute the script.

## Conditional Execution

#### If-Else
```bash
if [condition]
then [execution]
else [what would be executed if condition would fail]
fi [closing]
```
#### If-Only
```bash
if [condition]
then [execution]
fi [closing]
```
#### If-Elif-Else
```bash
if [first condition]
then [execution]
elif [second condition]
then [execution]
else [what would be executed if conditions would fail]
fi [closing]
```
#### Case
```bash
case <expression> in
	pattern_1 ) statements ;;
	pattern_2 ) statements ;;
	pattern_3 ) statements ;;
esac
```
**Example::**
```bash
case $opt in 
	"1") network_range ;;
	"2") ping_host ;;
	"3") network_range && ping_host ;;
	"*") exit 0 ;;
esac
```
---
### Comparison Operators
| Operator | Explanation |
|-|-|
| `-eq` | equal to |
| `-ne` | not equal to |
| `-lt` | less than |
| `-le` | less than or equal to |
| `-gt` | greater than |
| `-ge` | greater than or equal to |

### String Operators
|Operator|Description|
|-|-|
|`==`|is equal to|
|`!=`|is not equal to|
|`<`| 	is less than in ASCII alphabetical order|
|`>`| 	is greater than in ASCII alphabetical order|
|`-z`|if the string is empty (null)|
|`-n`|if the string is not null|

### File Operators

|Operator|Description|
|-|-|
|`-e `|if the file exist|
|`-f `|tests if it is a file|
|`-d `|tests if it is a directory|
|`-L `|tests if it is if a symbolic link|
|`-N `|checks if the file was modified after it was last read|
|`-O `|if the current user owns the file|
|`-G `|if the file’s group id matches the current user’s|
|`-s `|tests if the file has a size greater than 0|
|`-r `|tests if the file has read permission|
|`-w `|tests if the file has write permission|
|`-x `|tests if the file has execute permission|



### Special Variables
| | |
|-|-|
|`$#`|Number of arguments passed to the script.|
|`$@`|List of command-line arguments.|
|`$n`|`n` is number of argument|
|`$$`|Id of executing process|
|`$?`|Success of command. `0` is success, `1` is a failure|

### Regular Variables

```bash
> variable="Declared without an error."
> echo $variable
> Declared without an error.
```
## Arrays

```bash
> domains=(shadow wizard money gang)
> echo ${domains[0]}
> shadow
```
**OR**
```bash
> domains=(shadow wizard "money gang")
> echo ${domains[2]}
> money gang
```

## Loops

### For 
```bash
for variable in list
do
    # Commands to be executed for each item in the list
done
```
**Example:**
```bash
fruits=("apple" "orange" "banana")
for fruit in "${fruits[@]}"
do
    echo "I like $fruit"
done
```
---
### While
```bash
while [ condition ]
do
    # Commands to be executed while the condition is true
done
```
**Example:**
```bash
count=1 # Count from 1 to 5
while [ $count -le 5 ]
do
    echo $count
    ((count++))
done
```
---
### Until
```bash
until [ condition ]
do
    # Commands to be executed until the condition becomes true
done
```
**Example:**
```bash
count=1 # Count from 1 to 5
until [ $count -gt 5 ]
do
    echo $count
    ((count++))
done
```


### Script Termination

|Exit Status|Explanation|
|-|-|
|`exit 0`|Succesful execution|
|`exit 1`|General error condition|
|`exit 2`|Specific error condition|

### Wildcards
**In Bash, a wildcard refers to a character or a set of characters that can be used to represent a group of filenames or strings. Wildcards are often used in commands to perform operations on multiple files or strings that match a specified pattern.**
| Wildcard       | Example Usage                    | Explanation                                             |
|-----------------|----------------------------------|---------------------------------------------------------|
| `*` (Asterisk)  | `echo *.txt`                     | Matches all files ending with ".txt".                   |
| `?` (Question Mark) | `ls file?.txt`                | Matches files like "file1.txt", "fileA.txt", etc.       |
| `[ ]` (Square Brackets) | `ls [aeiou]*.txt`          | Matches any file starting with a vowel and ending with ".txt". |
| `{ }` (Brace Expansion) | `cp file{1,2,3}.txt dest/` | Expands to "file1.txt", "file2.txt", and "file3.txt" and copies to the destination. |
| `!(pattern)` (Extended Pattern Matching) | `ls !(file*.txt)`    | Matches all files except those starting with "file" and ending with ".txt". |
| `?(pattern)` (Zero or One Occurrence) | `ls file?(1).txt`   | Matches "file.txt" or "file1.txt".                      |
| `+(pattern)` (One or More Occurrences) | `ls file+(1).txt`  | Matches "file1.txt", "file11.txt", etc.                 |
| `*(pattern)` (Zero or More Occurrences) | `ls file*(1).txt` | Matches "file.txt", "file1.txt", "file11.txt", etc.    |

### Tips & Tricks

1. You Could use `tee` command for writing output to both standard output and file. If you would use `tee -a`, it would
2. Use `bash -x -v` to verbose debugging

