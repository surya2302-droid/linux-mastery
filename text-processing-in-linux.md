# REDIRECT
### stdin -> means standard input code is 0
### stdout -> means standard output code is 1
### stderr -> means standard errors code is 2

## To wrtite all erros that occures while running a commands in a specified file
```
sudo bash run.sh 2 > errors.txt 
```

here `run.sh` is the bash script we want to run and `2` is the code for `stderr` so whatever errors occured while running the bash script will be written in the file  `errors.txt`

## to wrtie all logs into a file (boath errors and standard logs)

``` 
sudo bash run.sh >> logs.txt 2>&1 
```
this will write all the logs to `logs.txt` file.

## USe of input redirect
 `<` is used for input redirect 

 ```
 cat < logs.txt
```

though cat logs.txt will return similar result but in some cases input redirects are rewuired like wc command

```
wc -l logs.txt 
```
will return <`no of lines` > `logs.txt` 
but 
```
wc -l <logs.txt
```
will return only the number of lines.  this might be useful in shell scripting


# AWK command
used for  pattern base text processing like csv -> comma separated value

```
awk '{pattern}' filename
```
lets assume a file like `name.txt` contains values like this

```
ab bc cd 
xy yx zx
as sd fd
```

this file has 3 rows and 3 coloumns coloumns are separated  by `space `

we can use `awk '{print $2}' name.txt` and this will give us a result like
```
bc
yx
sd
```

here print is instruction and $2 means the second coloumn 

but if our file is not separated by `space` then we have to specify the delimeter with awk command like if out file is separated by `,` 

```
ab,bc,cd
xy,yx,zx
as,sd,fd
```
then we have to use 
`awk -F , '{print $2}' name.txt`  -F  is used to specify the delimeter

to add serial no at the begining `awk '{print NR,$0}' filename `.
 
 `$0`  will print all the coloumns

use filer or condition in qwk command 
```
 awk '{if($3>400) print $0}' filename 
 ```
this will print all rows where coloumn3 's value is greater than 400

we can also use awk to update value in a certain file 
```
 awk '{if($3=400){$2=100} print $0}' filename 
 ```
this will update the value of coloumn2 to 100 for the rows where 3rd coloumn's value is 400


`$NF` -> will print the last coloumn
To find the rows that contains a specific word or letter
```awk '/India/ {print $0}' filename```
this will print all the rows that have India in it

to print row   ```awk 'NR=="8" {print $0}' filename```  ---> print 8th ROW

to print 8th to 10th row

```awk 'NR=="8" , NR=="10" {print $0}' filename```

to print the line no of empty line

```awk 'NF==0 {print NR}' filename```

to print the end line 

```awk 'END {print NR}' filename```

We can also use loop in awk command.

here is a example for and while loop to print 0-10
```
awk 'BEGIN {for (i=0;i<=10;i++) print i;}'

awk 'BEGIN {while (i<10) {i++;print "num is" i;}}'
```

# CUT command

### options

-c [LIST]: Cuts based on characters. The list can be a single position, a range, or a combination.

Example: ```cut -c 1-5 filename.txt``` extracts characters 1 through 5 from each line.


-f [LIST]: Cuts based on fields. The list can be a single field, a range, or a combination.

Example: ```cut -f 1,3 -d ',' filename.csv``` extracts the first and third fields from each line, using a comma as the delimiter.


-d [DELIMITER]: Specifies a field delimiter. The default delimiter is a tab character.

Example: ```cut -f 2 -d ':' /etc/passwd``` extracts the second field from the colon-separated /etc/passwd file.


-b [LIST]: Cuts based on bytes. This is useful for fixed-width data.

Example: ```cut -b 1-5 filename.txt``` extracts bytes 1 through 5 from each line.

# paste command

The paste command in Linux is used to merge lines of files horizontally. It combines corresponding lines from multiple files or multiple lines from a single file, separated by a specified delimiter. This command is useful for joining columns of data.


```sh

paste [options] [file...]
```
### Options
-d [delimiter]: Specifies a custom delimiter to separate the pasted lines. By default, paste uses a tab character.

Example: ```paste -d ',' file1 file2``` uses a comma as the delimiter.


-s: Serializes the paste operation, combining lines from a single file into a single line.

Example: ```paste -s file1```

 joins all lines of file1 into a single line.

```sh

$ cat file1
A
B
C

$ cat file2
1
2
3

$ paste file1 file2
A   1
B   2
C   3
```

### Using a Custom Delimiter

```sh

$ paste -d ',' file1 file2
A,1
B,2
C,3

```

``` cat file.txt |paste - - ``` -> marge two lines in one

```sh
$ cat file.txt
ab
bc
df
gf
hg
yt
er
ww
er
ff

$ cat file.txt |paste - -
ab      bc
df      gf
hg      yt
er      ww
er      ff

```

# sort command

`sort filename` ---> sort file as per first letter (alphabetically)

`sort -n filename` -----> sort with numeric value

`sort -k 2 filename` -----> sort file as respect to second coloumn 

`sort -k 2 -d "|" filename ` -----> by default sort use `space` as delimeter to specify diffarent delimeter we use `-d` command

`sort -c filename` ----->  check if the file is already sorted .




# tr command

The `tr` command in Linux is a utility for translating or deleting characters from input data. It reads from standard input and writes to standard output, making it useful for text manipulation tasks such as character substitution, deletion, and squeezing repeated characters.

### Basic Usage
The basic syntax of the `tr` command is:
```sh
tr [OPTION] SET1 [SET2]
```

### Options
- **SET1**: The set of characters to translate or delete.
- **SET2**: The set of characters to translate to. If provided, each character in SET1 is replaced by the corresponding character in SET2.
- **-d**: Deletes all characters in SET1 from the input.
- **-s**: Squeezes multiple consecutive occurrences of characters in SET1 into a single occurrence.
- **-c**: Complements the set of characters in SET1, i.e., matches all characters not in SET1.

### Examples

#### Translating Characters
Translating lowercase letters to uppercase:
```sh
echo "hello world" | tr 'a-z' 'A-Z'
```
Output:
```
HELLO WORLD
```

#### Deleting Characters
Deleting all vowels from the input:
```sh
echo "hello world" | tr -d 'aeiou'
```
Output:
```
hll wrld
```

#### Squeezing Repeated Characters
Squeezing multiple spaces into a single space:
```sh
echo "hello    world" | tr -s ' '
```
Output:
```
hello world
```

#### Complementing Character Sets
Deleting all non-digit characters:
```sh
echo "h3ll0 w0rld" | tr -cd '0-9'
```
Output:
```
30
```

When using `-s` without `SET2`, the command squeezes repeated characters specified in `SET1`.


#  join command

The `join` command in Linux is used to combine lines of two files based on a common field. It performs a join operation similar to database joins, making it useful for merging related data from different files.

The basic syntax of the `join` command is:
```sh
join [OPTION]... FILE1 FILE2
```

### Common Options
- **-1 FIELD**: Specifies the field in the first file to join on (default is the first field).
- **-2 FIELD**: Specifies the field in the second file to join on (default is the first field).
- **-t CHAR**: Specifies the input and output field separator (default is space).
- **-o FORMAT**: Specifies the format for the output line.
- **-a FILENUM**: Prints unpairable lines from file FILENUM (1 or 2).
- **-e STRING**: Replaces empty output fields with STRING.
- **-i**: Ignores case when comparing fields.
- **-v FILENUM**: Prints only unpairable lines from file FILENUM.

### Examples

Joining two files on the first field:
```sh
$ cat file1
1 Alice
2 Bob

$ cat file2
1 Engineering
2 Sales

$ join file1 file2
1 Alice Engineering
2 Bob Sales
```

Joining on the second field of the first file and the first field of the second file:
```sh
$ cat file3
Alice 1
Bob 2

$ cat file4
1 Engineering
2 Sales

$ join -1 2 -2 1 file3 file4
1 Alice Engineering
2 Bob Sales
```

Joining two files with a comma as the delimiter:
```sh
$ cat file5
1,Alice
2,Bob

$ cat file6
1,Engineering
2,Sales

$ join -t ',' file5 file6
1,Alice,Engineering
2,Bob,Sales
```

Including unpairable lines from both files:
```sh
$ cat file7
1 Alice
2 Bob
3 Charlie

$ cat file8
1 Engineering
2 Sales

$ join -a 1 -a 2 file7 file8
1 Alice Engineering
2 Bob Sales
3 Charlie
```

# split command


The `split` command in Linux is used to split a file into smaller parts. This command is particularly useful for managing large files by breaking them down into more manageable chunks.


The basic syntax of the `split` command is:
```sh
split [OPTION] [INPUT [PREFIX]]
```

### Options
- **-b [SIZE]**: Splits the file into pieces of the specified byte size.
  - Example: `split -b 1M largefile` splits `largefile` into 1 MB chunks.
- **-l [NUMBER]**: Splits the file into pieces with the specified number of lines.
  - Example: `split -l 1000 largefile` splits `largefile` into chunks of 1000 lines each.
- **-d**: Uses numeric suffixes instead of alphabetic suffixes for the output files.
  - Example: `split -d largefile` creates output files with numeric suffixes like `xaa`, `xab`, etc.
- **-a [N]**: Uses suffixes of length N (default is 2).
  - Example: `split -a 3 largefile` creates output files with suffixes of length 3 like `xaa`, `xab`, etc.
- **--additional-suffix=[SUFFIX]**: Adds an additional suffix to the output files.
  - Example: `split --additional-suffix=.txt largefile` creates output files like `xaa.txt`, `xab.txt`, etc.
- **-C [SIZE]**: Splits the file at the specified size, but ensures lines are not broken.


#### Splitting by Size
Splitting a file into 1 MB chunks:
```sh
split -b 1M largefile chunk_
```
This command creates files named `chunk_aa`, `chunk_ab`, `chunk_ac`, etc., each 1 MB in size.

#### Splitting by Lines
Splitting a file into chunks of 1000 lines each:
```sh
split -l 1000 largefile
```
This command creates files named `xaa`, `xab`, `xac`, etc., each containing 1000 lines.

#### Splitting with Numeric Suffixes
Splitting a file into 500 KB chunks with numeric suffixes:
```sh
split -b 500K -d largefile part_
```
This command creates files named `part_00`, `part_01`, `part_02`, etc., each 500 KB in size.

#### Using a Custom Suffix Length
Splitting a file with a custom suffix length of 3:
```sh
split -l 200 -a 3 largefile segment_
```
This command creates files named `segment_aaa`, `segment_aab`, `segment_aac`, etc., each containing 200 lines.

#### Adding an Additional Suffix
Splitting a file into 1 MB chunks and adding a `.txt` suffix:
```sh
split -b 1M --additional-suffix=.txt largefile chunk_
```
This command creates files named `chunk_aa.txt`, `chunk_ab.txt`, `chunk_ac.txt`, etc., each 1 MB in size.


# nl comand

nl add line no in any file 

### example
```sh
nl filename
```

# wc command

count line word character in a file


wc [OPTION]... [FILE]...
```

### Options
- **-l**: Prints the number of lines.
- **-w**: Prints the number of words.
- **-c**: Prints the number of bytes.
- **-m**: Prints the number of characters.
- **-L**: Prints the length of the longest line.
  
### Counting Lines, Words, and Bytes
Displaying the number of lines, words, and bytes in a file:
```sh
$ wc example.txt
  10  50  300 example.txt
```
This output shows that `example.txt` contains 10 lines, 50 words, and 300 bytes.

#### Counting Only Lines
Displaying only the number of lines in a file:
```sh
$ wc -l example.txt
  10 example.txt
```
This output shows that `example.txt` contains 10 lines.

#### Counting Only Words
Displaying only the number of words in a file:
```sh
$ wc -w example.txt
  50 example.txt
```
This output shows that `example.txt` contains 50 words.

#### Counting Only Bytes
Displaying only the number of bytes in a file:
```sh
$ wc -c example.txt
  300 example.txt
```
This output shows that `example.txt` contains 300 bytes.

#### Counting Characters
Displaying the number of characters in a file (useful for multi-byte character encodings):
```sh
$ wc -m example.txt
  300 example.txt
```
This output shows that `example.txt` contains 300 characters.

#### Finding the Longest Line
Displaying the length of the longest line in a file:
```sh
$ wc -L example.txt
  80 example.txt
```
This output shows that the longest line in `example.txt` is 80 characters long.

#### Combining Options
Using multiple options together to display lines, words, and characters:
```sh
$ wc -lw example.txt
  10  50 example.txt
```
This output shows that `example.txt` contains 10 lines and 50 words.

#### Using `wc` with Pipes
Counting words from the output of another command:
```sh
$ echo "Hello, world!" | wc -w
  2
```
This output shows that the phrase "Hello, world!" contains 2 words.


# uniq command 

The `uniq` command in Linux is used to report or filter out repeated lines in a file. It is commonly used in combination with the `sort` command because `uniq` works only on adjacent lines. The `uniq` command can also count and display the number of occurrences of each line.

The basic syntax of the `uniq` command is:
```sh
uniq [OPTION]... [INPUT [OUTPUT]]
```

### Options
- **-c**: Precedes each output line with the number of times it occurred.
- **-d**: Only prints duplicate lines.
- **-u**: Only prints unique lines.
- **-i**: Ignores differences in case when comparing lines.
- **-f N**: Ignores the first N fields when comparing lines.
- **-s N**: Ignores the first N characters when comparing lines.
- **-w N**: Compares no more than N characters in lines.
- **--help**: Displays help information.

###  Basic Usage
Removing duplicate lines from a file:
```sh
$ cat file.txt
apple
banana
apple
banana
cherry

$ uniq file.txt
apple
banana
apple
banana
cherry
```
This command removes adjacent duplicate lines. If lines are not adjacent, they will not be considered duplicates.

####  Counting Occurrences
Counting the occurrences of each line:
```sh
$ uniq -c file.txt
  2 apple
  2 banana
  1 cherry
```
This output shows that "apple" and "banana" each occur twice, while "cherry" occurs once.

####  Displaying Only Duplicates
Displaying only lines that are duplicated:
```sh
$ uniq -d file.txt
apple
banana
```
This output shows only the lines that are duplicated in the input.

####  Displaying Only Unique Lines
Displaying only lines that are not duplicated:
```sh
$ uniq -u file.txt
cherry
```
This output shows only the lines that are unique in the input.

####  Ignoring Case
Ignoring case differences when comparing lines:
```sh
$ cat file.txt
Apple
banana
apple
Banana
cherry

$ uniq -i file.txt
Apple
banana
cherry
```
This output shows that "Apple" and "apple", "banana" and "Banana" are considered duplicates when case is ignored.

####  Using with `sort`
Ensuring all duplicates are removed by sorting the file first:
```sh
$ sort file.txt | uniq
Apple
Banana
apple
banana
cherry
```
Using `sort` before `uniq` ensures that all duplicate lines are adjacent, allowing `uniq` to remove them correctly.

### The `uniq` command works only with adjacent duplicate lines. To remove all duplicates, the file must first be sorted.

# tail command


The `tail` command in Linux is used to display the last part of a file or input. By default, it shows the last 10 lines, but it can be customized to show any number of lines or bytes from the end of a file. It's particularly useful for viewing the most recent entries in log files.

The basic syntax of the `tail` 
```sh
tail [OPTION]... [FILE]...
```

### Options
- **-n [N]**: Displays the last N lines of the file.
  - Example: `tail -n 20 filename` shows the last 20 lines.
- **-c [N]**: Displays the last N bytes of the file.
  - Example: `tail -c 100 filename` shows the last 100 bytes.
- **-f**: Follows the file as it grows, displaying new lines as they are added.
  - Example: `tail -f logfile` is useful for real-time monitoring of log files.
- **-F**: Similar to `-f`, but will also follow the file if it is recreated or renamed.
  - Example: `tail -F logfile` is useful for log rotation.
- **--max-unchanged-stats=N**: With `-f`, reopens a file which has not changed for N iterations to see if it has been unlinked or renamed.
- **-q**: Suppresses printing of headers when multiple files are being examined.


# grep command


The `grep` command in Linux is used to search for patterns within files. It stands for "Global Regular Expression Print" and is a powerful tool for finding and filtering text based on patterns or regular expressions.

The basic syntax of the `grep` command is:
```sh
grep [OPTIONS] PATTERN [FILE...]
```

### Options
- **-i**: Ignores case when matching.
- **-v**: Inverts the match to select non-matching lines.
- **-c**: Counts the number of matching lines.
- **-l**: Lists filenames containing the match.
- **-n**: Shows line numbers with the output.
- **-H**: Prints the filename with the matching lines.
- **-r** or **-R**: Recursively searches directories.
- **-w**: Matches whole words only.
- **-o**: Prints only the matched parts of matching lines.
- **-E**: Uses extended regular expressions (equivalent to `egrep`).
- **-F**: Uses fixed strings (equivalent to `fgrep`).
- **--color**: Highlights the matching text.

### Examples

####  Basic Pattern Search
Searching for the pattern "hello" in a file:
```sh
$ grep "hello" file.txt
```
This command prints all lines in `file.txt` that contain the string "hello".

####  Case-Insensitive Search
Searching for the pattern "hello" in a file, ignoring case:
```sh
$ grep -i "hello" file.txt
```
This command prints all lines in `file.txt` that contain "hello" in any case (e.g., "Hello", "HELLO").

####  Inverted Match
Searching for lines that do not contain the pattern "hello":
```sh
$ grep -v "hello" file.txt
```
This command prints all lines in `file.txt` that do not contain the string "hello".

####  Counting Matches
Counting the number of lines that match the pattern "hello":
```sh
$ grep -c "hello" file.txt
```
This command prints the number of lines in `file.txt` that contain "hello".

####  Listing Matching Files
Listing all files in the current directory that contain the pattern "hello":
```sh
$ grep -l "hello" *
```
This command prints the names of all files that contain "hello".

####  Showing Line Numbers
Displaying lines with their line numbers that match the pattern "hello":
```sh
$ grep -n "hello" file.txt
```
This command prints lines in `file.txt` that contain "hello" along with their line numbers.

####  Recursive Search
Recursively searching for the pattern "hello" in all files in the current directory and subdirectories:
```sh
$ grep -r "hello" .
```
This command prints all lines containing "hello" in all files under the current directory.

####  Whole Word Match
Searching for whole words matching the pattern "hello":
```sh
$ grep -w "hello" file.txt
```
This command prints lines in `file.txt` where "hello" is a whole word (not part of another word).

####  Printing Only Matches
Printing only the matched parts of matching lines:
```sh
$ grep -o "hello" file.txt
```
This command prints only the parts of lines in `file.txt` that match "hello".


# sed command


The `sed` command in Linux, short for "stream editor," is a powerful utility for text stream processing. It is used for performing text transformations on input streams or files using simple commands specified in a script or directly on the command line.

The basic syntax of the `sed` command is:
```sh
sed [OPTIONS]... {script} [input-file...]
```

### Common Options
- **-e SCRIPT**: Specifies a script to run.
- **-f SCRIPT-FILE**: Specifies a file containing scripts to run.
- **-i[SUFFIX]**: Edits files in-place (optionally with a backup extension).
- **-n**: Suppresses automatic printing of pattern space.
- **-r**: Uses extended regular expressions (supports `+`, `?`, `{}`, `()`).
- **-i**: Edits files in-place.
- **--help**: Displays help information.

### `sed` Script Syntax
The `sed` script consists of commands (usually enclosed in single quotes) that specify operations on lines of text. Common commands include:
- **s/regexp/replacement/flags**: Substitutes `regexp` with `replacement`.
- **d**: Deletes pattern space.
- **p**: Prints pattern space.
- **a \text**: Appends `text` after a line.
- **i \text**: Inserts `text` before a line.
- **q**: Quits processing after reading the first line.

### Examples

####  Substitution (`s` command)
Replacing "apple" with "orange" in a file:
```sh
$ sed 's/apple/orange/' file.txt
```
This command replaces the first occurrence of "apple" with "orange" in each line of `file.txt`.

####  Deleting Lines (`d` command)
Deleting lines containing "banana" from a file:
```sh
$ sed '/banana/d' file.txt
```
This command deletes all lines containing "banana" from `file.txt`.

####  Printing Lines (`p` command)
Printing lines containing "cherry" from a file:
```sh
$ sed -n '/cherry/p' file.txt
```
This command prints only lines containing "cherry" from `file.txt`.

####  Appending Text (`a` command)
Appending "new line" after each line containing "old line" in a file:
```sh
$ sed '/old line/a \new line' file.txt
```
This command appends "new line" after each line containing "old line" in `file.txt`.

####  Inserting Text (`i` command)
Inserting "new line" before each line containing "old line" in a file:
```sh
$ sed '/old line/i \new line' file.txt
```
This command inserts "new line" before each line containing "old line" in `file.txt`.

####  Using Extended Regular Expressions (`-r` option)
Replacing "apple" or "orange" with "fruit" in a file using extended regular expressions:
```sh
$ sed -r 's/apple|orange/fruit/g' file.txt
```
This command uses extended regular expressions (`-r` option) to replace "apple" or "orange" with "fruit" globally (`/g` flag) in `file.txt`.

####  Editing Files In-Place (`-i` option)
Replacing "old" with "new" in a file and editing the file in-place:
```sh
$ sed -i 's/old/new/g' file.txt
```
This command edits `file.txt` directly, replacing all occurrences of "old" with "new".

`sed` operates on streams of text, making it suitable for text manipulation in scripts and pipelines.

Be cautious when using `-i` (in-place editing) as it modifies files directly without creating backups unless a suffix is specified (`-i.bak`).

`sed` supports basic regular expressions by default but can be instructed to use extended regular expressions with the `-r` option.


# cheat sheet with all commands


| Command                           | Description                                                                 | Example Usage                                                                                                                                                   | Options                                                                                         |
|-----------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
| `cat`                             | Concatenate and display file contents.                                      | `cat file.txt`                                                                                                                                                   | `-n` (number non-blank output lines), `-b` (number non-blank lines), `-s` (squeeze multiple adjacent blank lines into one)                                      |
| `head`                            | Output the first part of files.                                             | `head -n 5 file.txt`                                                                                                                                             | `-n` (specify number of lines), `-c` (specify number of bytes)                                                                                               |
| `tail`                            | Output the last part of files.                                              | `tail -n 10 file.txt`                                                                                                                                            | `-n` (specify number of lines), `-c` (specify number of bytes), `-f` (output appended data as the file grows)                                                  |
| `grep`                            | Search for patterns in files.                                               | `grep "pattern" file.txt`                                                                                                                                        | `-i` (ignore case), `-v` (invert match), `-n` (print line numbers), `-r` (recursive search), `-E` (use extended regular expressions)                           |
| `sed`                             | Stream editor for filtering and transforming text.                          | `sed 's/old/new/g' file.txt`                                                                                                                                     | `-i` (edit files in place), `-e` (add a script to the commands to be executed), `-n` (suppress automatic printing of pattern space)                        |
| `awk`                             | Powerful programming language for pattern scanning and processing.          | `awk '{print $1}' file.txt`                                                                                                                                      | `'{pattern}'` (action to be performed on matched pattern), `'{condition}'` (condition for executing action)                                                  |
| `sort`                            | Sort lines of text files.                                                   | `sort file.txt`                                                                                                                                                  | `-r` (reverse sort), `-n` (numerical sort), `-k` (sort by a specific column)                                                                                   |
| `uniq`                            | Report or omit repeated lines.                                              | `uniq file.txt`                                                                                                                                                  | `-c` (prefix lines by the number of occurrences), `-d` (only print duplicate lines), `-i` (ignore case), `-u` (only print unique lines)                       |
| `wc`                              | Print newline, word, and byte counts for each file.                         | `wc -l file.txt`                                                                                                                                                 | `-l` (count lines), `-w` (count words), `-c` (count bytes)                                                                                                     |
| `cut`                             | Remove sections from each line of files.                                    | `cut -d"," -f1 file.csv`                                                                                                                                         | `-d` (delimiter), `-f` (fields to select)                                                                                                                      |
| `tr`                              | Translate or delete characters.                                             | `tr '[:lower:]' '[:upper:]' < file.txt`                                                                                                                          | `-d` (delete specified characters), `-s` (squeeze repeated characters into one)                                                                                |
| `tee`                             | Read from standard input and write to standard output and files.             | `command | tee output.txt`                                                                                                                                          | `-a` (append to the given FILEs, do not overwrite)                                                                                                              |
| `paste`                           | Merge lines of files.                                                      | `paste file1.txt file2.txt`                                                                                                                                      | `-d` (delimiter), `-s` (concatenate all lines in one)                                                                                                          |
| `join`                            | Join lines of two files on a common field.                                  | `join file1.txt file2.txt`                                                                                                                                       | `-t` (specify the field separator), `-1` (join on this field of file 1), `-2` (join on this field of file 2)                                                   |
| `comm`                            | Compare two sorted files line by line.                                      | `comm file1.txt file2.txt`                                                                                                                                       | `-1` (suppress lines unique to file 1), `-2` (suppress lines unique to file 2), `-3` (suppress common lines)                                                    |
| `xargs`                           | Build and execute command lines from standard input.                        | `find . -name "*.txt" | xargs grep "pattern"`                                                                                                                                           | `-0` (input items are terminated by a null character), `-n` (max arguments per command line), `-P` (run commands in parallel)                                  |
| `grep -v`                         | Invert match; select non-matching lines.                                    | `grep -v "pattern" file.txt`                                                                                                                                     | `-i` (ignore case), `-n` (print line numbers), `-w` (match whole words), `-r` (recursive search), `-E` (use extended regular expressions)                      |
| `awk '{print NF}'`                | Count number of fields in each line.                                        | `awk '{print NF}' file.txt`                                                                                                                                      |                                                                                                 |
| `sort -n`                         | Sort numerically.                                                           | `sort -n file.txt`                                                                                                                                               | `-r` (reverse sort), `-k` (sort by a specific column)                                                                                                           |
| `uniq -c`                         | Prefix lines by the number of occurrences.                                  | `uniq -c file.txt`                                                                                                                                               | `-d` (only print duplicate lines), `-i` (ignore case), `-u` (only print unique lines)                                                                            |
| `cut -f2-`                        | Select all fields from the second field onwards.                            | `cut -f2- file.txt`                                                                                                                                              | `-d` (delimiter), `-s` (suppress lines not containing delimiters)                                                                                              |
| `tr -d '[:punct:]'`               | Delete all punctuation characters.                                          | `tr -d '[:punct:]' < file.txt`                                                                                                                                   | `-c` (complement set of characters), `-s` (squeeze repeated characters into one)                                                                                |
| `tee -a`                          | Append to the given FILEs, do not overwrite.                                | `command | tee -a output.txt`                                                                                                                                         | `-a` (append to the given FILEs, do not overwrite)                                                                                                              |

