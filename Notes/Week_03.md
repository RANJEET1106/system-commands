# System Commands Week 3


# Combining Commannds and Files

## 1.Executing Multiple Commands
- `command1 ; command2 ; command3;` &emsp; Each Command Will  be Executed **One After Other**

- `command1 && command2` &emsp; command2 will be **executed only if command1 succeeds**

- `command1 || command2` &emsp; command2 will **not be executed if command1 succeeds**

- `(command1 ; command2 ; command3;)` &ensp; Command **gets executed in bash subshell** and output is displayed on main shell.<br>
You can compare outputs of commands `echo $BASH_SUBSHELL` &nbsp  is`0` &nbsp; and `(echo $BASH_SUBSHELL)` &nbsp; is `1`.

## 2.File Descriptors

- `stdin` or (`0`) :- Used to tkae input from user
- `stdout` or (`1`) :- Used to get output
- `stderr` or (`2`) :- Used to display errors

## 3.Operator for Combining Command and File

1. `command > file1`  &emsp; Content of **file1 will be overwritten. New file1 will be created if it does not exist**.</br>
Ex. `ls -1 /usr/bin>file1` &ensp; argument `1`  is givent for `stdout` output of  `ls /usr/bin` to `file1`.</br>You can view content of file1 using command `less file1`. 

2. `cat > file1` &emsp; **Append keyboard input to the file1 without overwriting**</br>
use `ctrl+d` to come out of cat command</br>
**`cat` is used for conacatinating files rather than appending**

3. `cat file1` and `cat < file1` &emsp; **Display content of `file1`.**

4. `command >> file1` &emsp; Append `command` to the `file1`. **New file1 will be created if it does not exist**.

5. `command 2> file1` &emsp; **Write std error of command to file1.**</br>
**Output is displayed on screen and all errors are stored in file1.**

6. `command > file1 2> file2` &emsp; **Write output to `file1` and errors to `file2`.**

7. `wc file1` and `wc < file1` &emsp; Outputs the `{number_of_lines} {number_of_words} {number_of_character}` of file1.

8. `command > file1 2>&1` &emsp; **Store output and error of `command` both to `file1`.**

9. `command1 | command2` &emsp; **Output of `command1` is mapped to input of `command2`.**</br>
Ex. `ls /usr/bin | wc -l` &emsp; Output of `ls /usr/bin` which is list of directory is given directly to the `wc -l` which counts the line and prints no of lines present in `ls /usr/bin`.

10. `command > file1 2> /dev/null` &emsp; **store output** in `file1` and **discard all errors**. `/dev/null` file is like black hole , Whichever we put there simple disappears.

11. `command1 | tee file1` &emsp; **Display output on the screen as well as stores it in `file1`.**

</br></br></br>

# Software Management

## Need for Package Manager

- Tools for **installing,updating,removing,managing software.**
- **Install new / updated** software across network.
- Package - **File look up** , both ways
- **Database** of packages on the system **including versions**.
- **Dependency** checking.
- **Signature verification** tools.
- Tools for **building packages**

## Package Types

    RPM
        Red Hat
            CentOS
            Fedora
            Oracle Linux
     
        SUSE Enterprise Linux
            openSUSE

    DEB
        Debian
            Ubuntu
                Mint
            Knoppix

## Tools

    RPM
        Yellowdog Updater Modifier (yum)
            Red Hat Package Manager (rpm)
            Dedified YUM (dnf)
    
    DEB
        Advanced Package Tool (apt)
            dpkg
                dpkg-deb

    apt
        synaptic - GUI (Graphical User Interface)
        aptitude - CLI (Command Line Interface)

## Inquiring Package db

- `apt-catch search keyword` Search packages for a `keyword`.
- `apt-catch pkgnames` List all packages.
- `apt-catch show -a package` Display package record of a `package`.

## Package Names

- RPM
        - package-version-release.architecture.rpm
- DEB
        - package_version-revision_architecture.deb

## Package Priorities

- **required** : **Essential** to proper functioning of the system.
- **important** : Provides **functionality** that enables the **system to run well**.
- **standard** : Included in a **standard system installation**.
- **optional** : **Can omit** if you do not have enough storage.
- **extra** : **Could conflict with packages with higher priority , has specialized requirements , install only if needed.**

## Checksums :Validates Packages

- md5sum - 128 bit
- sha1sum - 160 bit
- sha256sum - 256 bit

### Only sudoers can install / upgrade /remove packages<br> &emsp; /etc/sudoers

## Commands Related to Managing Package using apt

### `/etc/apt` Files : `sources.list` and Folder : `sources.list.d`

- `sudo apt-get update` Fetch updates of programs present on the system.

- `sudo apt-get upgrade` Installs new updates
.
- `sudo apt autoremove` Remove older versions of programs which are updated.

- `sudo apt-get remove <package>` Removes the `package` from the system

- `sudo apt-get install <package>` Installs the `package`

- `sudo apt-get reinstall <package>` Refrash the versin of the `package`

- `sudo apt-get clean` Clean local repo of retrived packages

- `sudo apt-get purge <package>` Purge package files from the system


## Package Management Using dpkg

### `/var/lib/dpkg` Files : `arch`,`available`,`status` Folder : `info`

- `dpkg -l <pattern>` List **all packages** whose names **match the `pattern`.**

- `dpkg -L <package>` List **installed files** that came **from `packages`.**

- `dpkg -s <package>` Report the **status** of `package`.

- `dpkg -S <pattern>` Search **installed packages for a file.**

- `dpkg-query -W -f='${Section} ${binary:Package}\n' | sort | less` Argument `W` shows the installed packages

## Installing a Deb Package

`dpkg -i package_version-revision_architecture.deb`

<br><br><br>

# Linux Process Management

- `coproc <command>` Command run in **background** giving terminal control to the user. Use command `help coproc` to know more

- `kill <process_id>` Can kill the background processwith id = `process_id`.

- `ctrl+c` Kill the forground running process.

- `fg` Bring background running processs to the foreground.

- `jobs` and `ps` shows the currently running processes.More information use command `help jobs`.

- `top` Displays all ongoing processes in PC in decreasing order of CPU usage.

- `history` Commands previously used on terminal

- `echo *` List all directories and files in cd.
- `echo D*` List all the files start with `D`.

- `echo $?` Return code of last executed command.
- `echo $$` return PID of currently running process.
