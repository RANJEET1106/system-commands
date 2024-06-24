# System Commmands Week 4

#### Note:All Necessary text files are maintioned at bottom. first create them in your pwd and then run commands for better understanding.

# Regex (Regular Expression)
- regex is a pattern template to filter text
- **BRE**: POSIX **B**asic **R**egular **E**xpression engine
- **ERE**: POSIX **E**xtended **R**egular **E**xpression engine

## Usage
- `grep <pattern> filename`

- `command | grep <pattern>`
- Default engine: BRE
- Switch to use ERE:
    - `egrep <pattern> filename`

    - `grep -E <pattern> filename`

## Special Characters (BRE & ERE)
- `.` Any single character except null or newline

- `*` Zero or more of the preceding character/expression

- `[]` Any of the enclosed characters; hyphen (`-`) indicates character range

- `^` Anchor for beginning of line or **negation** of enclosed characters

- `$` Anchor for end of the line

- `\` Escape special characters

## Special Characters (BRE)
- `\{n,m\}` Range of occurances of preceding pattern at least n and utmost m times

- `\(\)` Grouping of regular expression

## Special Characters (ERE)
- `{n,m}` Range of occurances of preceding pattern at least n and utmost m times

- `()` Grouping of regular expression

- `+` One or more of preceding character/expression

- `?` Zero or one of preceding character/expression

- `|` Logical OR over the patterns

## Character Classes

- `[[:print:]]` &emsp; Printable

- `[[:blank:]]` &emsp; Space / Tab

- `[[:alnum:]]` &emsp; Alphanumeric

- `[[:space:]]` &emsp; Whitespace

- `[[:alpha:]]` &emsp; Alphabetic

- `[[:punct:]]` &emsp; Punctuation

- `[[:lower:]]` &emsp; Lower case

- `[[:xdigit:]]` &emsp; Hexadecimal

- `[[:upper:]]` &emsp; Upper case

- `[[:graph:]]` &emsp; Non-space

- `[[:digit:]]` &emsp; Decimal digits

- `[[:cntrl:]]` &emsp; Control characters

## Backreferences
- `\1` through `\9`
- `\n` matches whatever was matched bt nth earlier paranthesized subexpression
- A line with two occurances of hello will be matched using: `\(hello\).*\1`

## BRE operator precedence
- Highest

    - `[..]` `[==]` `[::]` char collation

    - `\`metachar

    - `[]` Bracket expansion

    - `\(\)` `\n` subexpresions and backreferences

    - `* \{ \}` Repetition of preceding single char regex

    - Concatenation

    - `^` `$` anchors
- Lowest

## ERE operator precedence
- Highest

    - `[..]` `[==]` `[::]` char collation

    - `\`metachar

    - `[]` Bracket expansion

    - `()` grouping

    - `*` `+` `?` `{ }` Repetation of preceding regex

    - `\(\)` `\n` subexpresions and backreferences

    - `* \{ \}` Repetition of preceding single char regex

    - Concatenation

    - `^` `$` anchors

    - `|` alternation
- Lowest

## Some grep commands

- `grep 'Anu' names.txt` or `cat names.txt | grep 'Anu'` 
    - Prints the lines which contains `Anu` in `names.txt`

- `grep 'S.n' names.txt`
    - Prints the line wwhere there is letter between `S` and `n`

- `grep -i '^M' names.txt`
    - Starts with `M` or `m`

- `'an$'` lies end with `an`
- `'an\b'` words end with `an` ; `\b` is word boundry
- `'M[ME]'` words having either `MM` or `ME` we can also do `'[ME]M'` for `MM` or `EM`
- `'\bS.*[mn]'` name starts with `S ` and have `m or n` after `S`.
- `B90[^5-7]` : `B90` followed by characters other  than `5,6,7`

## Egrep
- `[aeiou]\{2\}` 2 consecutive vowels 

- `'\(ma\).*\1'` two times `ma` is present
- `'M+'` matches `M` either one or more number of times ; `'M*'` matches if `M` occure 0 or more times similar for groups `'(ma)+'`
- `'(am|ma)'` eitherr `am` or `ma`
- `'\b .{4}$'` last word of 4 characters
- `grep '[[:alnum:]]$' chartypes.txt` Prints the line ends with alnum


- `cat chartypes.txt | egrep -v '^$'` prints all except empty lines `-v` prints all except the given condition `'^$'` which represent the empty line

- `egrep '[[:digit:]]{12}' patterns.txt` Prints the line conataining adhar number

- `egrep '\b[[:digit:]]{6}\b' patterns.txt` Prints the line containing telephone number which has only 6 characters

- `egrep '\b[[:alpha:]]{2}[[:digit:]]{2}[[:alpha:]][[:digit:]]{3}\b' patterns.txt` Displays line containing roll number

- `egrep '\b[[:alnum:]]+\.[[:alnum:]]+\b' patterns.txt` urls of type `alnum.alnum`. backslash `\` is used as escape character for `.`

## Horizontal Trimming

- `cut -c 1-4 fields.txt` Prints only first four characters of each line

- `cut -d " " -f 2 fields.txt` use space as delimiter and prints the 2nd part
    - similarly `cut -d " " -f 1-2 fields.txt` for multiple fields.

# Files

## chartypes.txt
```
hello: alphabetical stuff: 5g
l: start lower end upper : H
L: start upper end lower : h
5g: alpha numeric stuff : 42
42: solution to everything :	  
	: start with control C end with dot : .

, : start with comma end with equals :=
  : start with blank end with control char :	
```

## fields.txt
```
1234;hello world,line-1
234567;welcome cmdline,line-2
3456;parse text,line-3
```

## names.txt
```
MM228901 Mary Manickam
ED22B902 Raman Singh
ME228903 Umair Ahmad
CS228904 Charles M. Sagayam
EE228905 Anu K. Jain
NA228906 Anupama Sridhar
PH22B907 Vel Sankaran
```

## patterns.txt
```
Aadhar card number contains 12 digits and can look like 123456781234 for example.
Pincodes of cities in India contain 6 digits and that of IITM is 600036. 
Phone numbers without the country code or 8 prefix for std code are 10 digits. 
An example for my office landline is 4422574770 and prefix with 8 to dial me in my office 
Roll numbers in IIT for regular students are of the pattern MM22B001 where the first two 
letters correspond to the Department code, 2 digits for the year of joining, then the program 
code character and then a 3 digit number for ther roll number within the class. 
URLs can be given these days without the protocol like https://www.iitm.ac.in/ They can be
given as just github.com for example.
```