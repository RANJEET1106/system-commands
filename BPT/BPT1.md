# Biweekly Programming Assignment 1

## Question No 1

A company has 5 departments, each named `Dept1` to `Dept5`. Within each department, there are 3 teams labeled `TeamA` to `TeamC`. Each team works on 10 projects.There is a directory for every team in `~/se2001/BPT1_problem_1/`.

**Write Bash command(s) to create a file for each project, with the files named from `project1` to `project10`, in every team directory. Each file should be empty to ensure minimal space usage.**

**Note** Please run `synchro init` command before you start working on your solution.

## Solution

`synchro init`

```sh
for dept in Dept{1..5}; do for team in Team{A..C}; do for i in {1..10}; do touch ~/se2001/BPT1_problem_1/"$dept"/"$team"/project"$i"; done; done; done
```

## Question No 2

**1. Create Directories**:
- Create a base directory called `project`.
- Within `project`, create the following subdirectories using brace expansion:
- `src/{module1,module2}/{include,lib}`
- `docs/{api,manual}`
- Create a directory `bin` within `project`.

**2. Create Files**:
- Inside `src/module1/include`, create an empty file named `module1.h`.
- Inside `src/module1/lib`, create an empty file named `module1.so`.
- Inside `src/module2/include`, create an empty file named `module2.h`.
- Inside `src/module2/lib`, create an empty file named `module2.so`.

**3. Create Hard Links**:
- Create a hard link to `module1.h` in the `bin` directory and name it `module1_hardlink.h`.
- Create a hard link to `module2.so` in the `bin` directory and name it `module2_hardlink.so`.

**4. Create Soft Links**:
- Create a soft link to the `docs` directory in the `project` directory and name it `documentation`.
- Create a soft link to `module1.so` inside `module2/lib` directory and name it `module1_symlink.so`.

**5. Modify Permissions**:
- Set the permission of `project` directory to `755`.
- Set the permission of all directories under `project/src` to `700`.
- Set the permission of all `.h` files to `644`.
- Set the permission of all `.so` files to `755`.

## Solution

### Create base directory 'project'
`mkdir project`

### Create subdirectories using brace expansion

`mkdir -p project/src/{module1,module2}/{include,lib}`\

`mkdir -p project/docs/{api,manual}`\

`mkdir -p project/bin`

### Create empty files

`touch project/src/module1/include/module1.h`\

`touch project/src/module1/lib/module1.so`\

`touch project/src/module2/include/module2.h`\

`touch project/src/module2/lib/module2.so`

### Create hard links in the bin directory

`ln project/src/module1/include/module1.h project/bin/module1_hardlink.h`\

`ln project/src/module2/lib/module2.so project/bin/module2_hardlink.so`

### Create soft link 

`ln -s project/docs project/documentation`

`ln -s ../module1.so project/src/module2/lib/module1_symlink.so`

### Set permissions 

`chmod 755 project`

`chmod -R 700 project/src/*`

`chmod 644 project/src/**/*.h`

`chmod 755 project/src/**/*.so`



## Question No 3

You are given two text files, `file1.txt` and `file2.txt` in the `/opt/assets/` directory, each containing a list of names of world rivers (one name per line) in current working directory. Write two sequential commands in a file `script.sh` and make it executable such that the script will do the following
1. Display the differences between them in a unified format.
2. Print the names that are common to both files.

**Hint**
- **Use appropriate flags/options present in the following commands. Please use man pages or --help flag to understand what each flag do.**
 - **Use `diff`**: Compare the two files and display the differences between them in a unified format.
- **Use**  `comm`: can be used for the following
- Names that are common to both files.

## Solution

use the following script.sh
```sh script.sh
#!/usr/bin/bash

diff -u /opt/assets/file1.txt /opt/assets/file2.txt
comm -12 /opt/assets/file1.txt /opt/assets/file2.txt
```
then use the command `chmod 777 script.sh` it will make `script.sh` executable

## Question No 4

Please use the nslookup command (on powershell or linux on your local system) to identify the IP addresses associated with the following websites. After obtaining the IP addresses, enter each one into a browser to check if it directs you to the corresponding website. For each website, print the result using the echo command: if the website is successfully reached using the IP address, print "www.website.com Yes", otherwise print "www.website.com No". Perform these steps for each website sequentially:

```www.google.com```\
```www.yahoo.com```\
```www.duckduckgo.com```\
```www.youtube.com```\
```www.aws.amazon.com```

Create a file with name `script.sh` which contains the `echo` commands sequentially.

Hint:

You can use the nslookup command for DNS lookup.

What is DNS and Why Perform a DNS Lookup?: The Domain Name System (DNS) translates human-readable domain names (like www.example.com) into IP addresses (like 93.184.216.34). DNS is crucial because it allows users to access websites using domain names instead of remembering complex IP addresses. A DNS lookup retrieves the IP address associated with a domain name, which is essential for network troubleshooting and ensuring that domain names are correctly mapped to their respective IP addresses.

## Solution

use the following script.sh

```sh , script.sh
#!/usr/bin/bash

echo "www.google.com Yes"
echo "www.yahoo.com No"
echo "www.duckduckgo.com Yes"
echo "www.youtube.com No"
echo "www.aws.amazon.com No"
```
then use the command `chmod 777 script.sh` it will make `script.sh` executable