# Commands  : Series 3


<div dir="rtl" markdown="1">
گزارش کار هفتم :‌
<div dir="ltr" markdown="1">

* **[SED](#SED)**

* **[AWK](#AWK)**

<div dir="rtl" markdown="1">
دو ابزار برای پردازش متن 
<div dir="ltr" markdown="1">

## SED:

`Linux system provides some tools for text processing, one of those tools is sed.`
SED command in UNIX is stands for stream editor and it can perform lot’s of function on file like:

* searching
* find and replace
* insertion
* deletion
 
`By using SED you can edit files even without opening it`, which is `much quicker` way to find and replace something in file, than first opening that file in VI Editor and then changing it.

**Syntax:**

`sed OPTIONS... [SCRIPT] [INPUTFILE...] `

**Example:**

Consider the below text file as an input.

```
$cat > geekfile.txt
unix is great os. unix is opensource. unix is free os.
learn operating system.
unix linux which one you choose.
unix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
Sample Commands
```

### Replacing or substituting string : 

The below simple sed command replaces the word “unix” with “linux” in the file.

```
$sed 's/unix/linux/' geekfile.txt
```

**Output :**

```
linux is great os. unix is opensource. unix is free os.
learn operating system.
linux linux which one you choose.
linux is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
Here the “s” specifies the substitution operation. The “/” are delimiters. The “unix” is the search pattern and the “linux” is the replacement string.
```

`By default, the sed command replaces the first occurrence of the pattern in each line and it won’t replace the second, third…occurrence in the line.
`
### Replacing the nth occurrence of a pattern in a line : 
Use the /1, /2 etc flags to replace the first, second occurrence of a pattern in a line. The below command replaces the second occurrence of the word “unix” with “linux” in a line.

```
$sed 's/unix/linux/2' geekfile.txt
```

**Output:**
```
unix is great os. linux is opensource. unix is free os.
learn operating system.
unix linux which one you choose.
unix is easy to learn.linux is a multiuser os.Learn unix .unix is a powerful.
```


### Replacing all the occurrence of the pattern in a line : 
The substitute flag /g (global replacement) specifies the sed command to replace all the occurrences of the string in the line.

```
$sed 's/unix/linux/g' geekfile.txt
```

**Output :**

```
linux is great os. linux is opensource. linux is free os.
learn operating system.
linux linux which one you choose.
linux is easy to learn.linux is a multiuser os.Learn linux .linux is a powerful.
Replacing from nth occurrence to all occurrences in a line : Use the combination of /1, /2 etc and /g to replace all the patterns from the nth occurrence of a pattern in a line. The following sed command replaces the third, fourth, fifth… “unix” word with “linux” word in a line.
```
```
$sed 's/unix/linux/3g' geekfile.txt
```

**Output:**

```
unix is great os. unix is opensource. linux is free os.
learn operating system.
unix linux which one you choose.
unix is easy to learn.unix is a multiuser os.Learn linux .linux is a powerful.
Parenthesize first character of each word : This sed example prints the first character of every word in parenthesis.
```
```
$ echo "Welcome To The Geek Stuff" | sed 's/\(\b[A-Z]\)/\(\1\)/g'
```

**Output:**

```
(W)elcome (T)o (T)he (G)eek (S)tuff
```

### Replacing string on a specific line number : 

You can restrict the sed command to replace the string on a specific line number. An example is


```
$sed '3 s/unix/linux/' geekfile.txt
```

**Output:**

```
unix is great os. unix is opensource. unix is free os.
learn operating system.
linux linux which one you choose.
unix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
The above sed command replaces the string only on the third line.
```


### Deleting lines from a particular file : 
SED command can also be used for deleting lines from a particular file. SED command is used for performing deletion operation without even opening the file

**Examples:**

1. To Delete a particular line say n in this example
**Syntax:**
`$ sed 'nd' filename.txt`
**Example:**
`$ sed '5d' filename.txt`

2. To Delete a last line

**Syntax:**
`$ sed '$d' filename.txt`

3. To Delete line from range x to y

**Syntax:**
`$ sed 'x,yd' filename.txt`
**Example:**
`$ sed '3,6d' filename.txt`

5. To Delete from nth to last line

**Syntax:**
`$ sed 'nth,$d' filename.txt`
**Example:**
`$ sed '12,$d' filename.txt`

6. To Delete pattern matching line

**Syntax:**
`$ sed '/pattern/d' filename.txt`
**Example:**
`$ sed '/abc/d' filename.txt`



## AWK:

Awk is a scripting language used for manipulating data and generating reports.The awk command programming language requires no compiling, and allows the user to use variables, numeric functions, string functions,and logical operators.


Awk is abbreviated from the names of the developers – Aho, Weinberger, and Kernighan.

1. AWK Operations:

* Scans a file line by line
* Splits each input line into fields
* Compares input line/fields to pattern
* Performs action(s) on matched lines

2. Useful For:

* Transform data files
* Produce formatted reports

3. Programming Constructs:

* Format output lines
* Arithmetic and string operations
* Conditionals and loops

**Syntax:**

`awk options 'selection _criteria {action }' input-file > output-file`

**Options:**

`-f program-file : Reads the AWK program source from the file 
                  program-file, instead of from the 
                  first command line argument.
-F fs            : Use fs for the input field separator
`

Consider the following text file as the input file for all cases below : 


```
$cat > employee.txt 
ajay manager account 45000
sunil clerk account 25000
varun manager sales 50000
amit manager account 47000
tarun peon sales 15000
deepak clerk sales 23000
sunil peon sales 13000
satvik director purchase 80000
```


### Default behavior of Awk : 

By default Awk prints every line of data from the specified file.

```$ awk '{print}' employee.txt```

**Output:**

```
ajay manager account 45000
sunil clerk account 25000
varun manager sales 50000
amit manager account 47000
tarun peon sales 15000
deepak clerk sales 23000
sunil peon sales 13000
satvik director purchase 80000 
In the above example, no pattern is given. So the actions are applicable to all the lines. Action print without any argument prints the whole line by default, so it prints all the lines of the file without failure.
```

### Print the lines which matches with the given pattern.

```$ awk '/manager/ {print}' employee.txt ```

**Output:**

```
ajay manager account 45000
varun manager sales 50000
amit manager account 47000 
In the above example, the awk command prints all the line which matches with the ‘manager’.
```

### Splitting a Line Into Fields : For each record i.e line, the awk command splits the record delimited by whitespace character by default and stores it in the $n variables. If the line has 4 words, it will be stored in $1, $2, $3 and $4 respectively. Also, $0 represents the whole line.

```$ awk '{print $1,$4}' employee.txt```

**Output:**

```
ajay 45000
sunil 25000
varun 50000
amit 47000
tarun 15000
deepak 23000
sunil 13000
satvik 80000 
```

**Refrence:**
[GEEKFORGEEKS](https://www.geeksforgeeks.org/)