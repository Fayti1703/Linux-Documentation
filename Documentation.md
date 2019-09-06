# Linux Documentation

by firebird641

## nano

`nano` is a simple console text editor.

~~~bash
nano notes # edit the "notes" file in the current directory. Creates the file on save if it does not exist
~~~

## cat

`cat` (con**cat**enate) prints the contents of files. If multiple files are specified, they are printed one after the other without seperators.

~~~bash
cat notes
~~~

~~~bash
cat data1 data2
~~~

## printf

`printf` (**print f**ormat) prints a string according to a format string and input parameters. The format string may contain placeholders (`%<C>` where `<C>` is a character) and escape sequences (`\<C>`, where `<C>` is a character).
For more information on the format string and escape sequences, see the documentation of the C printf function (`man 3 printf`).
~~~bash
printf "Hi, I'm %s.\n" "$NAME"
~~~

## ls

`ls` (**l**i**s**t) prints the files in a directory. If no directory is given, it uses the current working directory.

The `-l` switch shows a longer listing that includes things like permission bits, file owners and last modified dates.
The `-a` switch shows all files in a directory, including hidden files

~~~bash
ls # show files in current directory
ls -l # list files in current directory
ls -la # list all files in current directory
~~~

## cp, mv, rm

~~~bash
# Copy
cp file1 file2
# Rename / Move
mv file1 file2
# Delete
rm file
rm -r directory # recursively remove
rmdir # removes a directory (it must be empty)
~~~

## fsck

`fsck` detects and fixes file system errors (like chkdsk). 

## pwd

`pwd` (Print Working Directory) prints the current directory path.

## Directory Structure Commands

~~~bash
/ # root directory
~ # current users home directory
~root # home directory of the root user
./ # current directory
~~~

## Change Directory

~~~bash
cd /home/user/ # go to /home/user/
~~~

## Chroot

Chroot allowes you to change the root directory. This means you can set up a folder as a virtual environment for example (this is used when installing Arch Linux). To run commands inside the chroot directory you need to have all necessary files inside the jail. You can also run commands in a chroot:

~~~
chroot /home/user/directory command
~~~

## Fakeroot

Fakeroot creates an environment that "simulates" root privileges on a command. It fools the process into thinking it is being run as root.

## File Extensions

Linux does not know any file extensions. It determines the type of a file by the first few bytes of the contents (called the "magic bytes"). Use whatever you want.

## Special Chaining Operators

~~~bash
apt update & apt dist-upgrade -y & # Backgrounds the Update commands
sleep 10 ; wall "Hello World" # send Message "Hello World" to all users after 10 Seconds
rm -rf !(*.html) # delete all files except *.html
~~~

## Autocomplete

When typing a command you can press the TAB-Key to let the system automatically complete your input if possible.

## Console Shortcuts

There are 6 tty Consoles on any Linux System. If it runs run a Desktop Manager, it is on the 7th Console. You can Access the Consoles with the Keyboard Shortcut:

~~~bash
Strg + Alt + F1-F7
~~~

## APT

APT (Advanced Packaging Tool) is a Linux Package Manager. It is used to Install / Remove / Update Software Packages for Debian-based Distributions like Ubuntu, Linux Mint and others.

~~~bash
apt update # Update Software List (check for updates)
apt dist-upgrade # Update Software based on Software List
apt install gimp # Install Package "GIMP"
apt search python # Search for Package "python"
apt remove firefox # Remove the Package "Firefox"
apt autoremove # Remove unnecessary Packages automatically
apt -f install # Install unmet dependencies
dpkg --configure -a # Complete Update/Upgrade Process if it has been interrupted
dpkg -i package.deb # Install the Debian Package "package.deb"
~~~

## Services

Services can be configured using the service command.

~~~bash
service --status-all # show status of all services
service networking restart # restart network service
service gdm start # start service gdm
service ssh stop # stop SSH service
~~~

## Networking

Here are some useful networking commands:

~~~bash
ifconfig -a # Show Status of all Interfaces
ip link # show all Network Interfaces
ip addr # Show interface IP/MAC-Addresses
netstat -tulpn # show Services listening on TCP/UDP Ports
nslookup google.com # resolve Google.com using the systems DNS Server
traceroute google.com # do a traceroute on google.com
~~~

The Network Interfaces can be configured in the **/etc/network/interfaces** file.

~~~bash
# DHCP Interface Example
auto eth0
iface eth0 inet dhcp
# Static Interface  Example
auto eth1
iface eth1 inet static
	address 192.168.0.1
	netmask 255.255.255.0
	gateway 192.168.0.1
	dns-nameservers 1.1.1.1
~~~

## Script Execution

When writing a script you want to execute with the console (./script), you need to specify the program that is being used to run the script. The following example is the first line of a python script.

~~~bash
#!/usr/bin/python
~~~

## mkpasswd

~~~bash
mkpasswd -l 16 # generates a password of length 16
~~~

## Checking Disk Usage

~~~bash
df # Disk Free: report disk space usage
du # Disk Usage: estimate file space usage
~~~

## iptables

`iptables` is a low-level IP-Filtering Firewall.

## arptables

`arptables` is a low-level ARP-Filtering Firewall.

## dd

The disk dump command allows you to create images from block devices or write images to block devices. It also permits copying from one block device to another.

~~~bash
dd if=source of=target # clones from source to target
~~~

## sync

Sync writes any data buffered in memory to the disk. Useful if there is an unexpected halt of the system or before removing an external data storage medium (though in those cases, when available, the `eject` command should be used).

## I/O Redirection

### Stream Numbers
0 ("STDIN") is Standard Input

1 ("STDOUT") is Standard Output

2 ("STDERR") is Standard Error, used for the output of errors or status messages.
### Redirection
~~~bash
command > output.log # Redirect STDOUT to output.log !! This overwrites the file!
command >> output.log # Redirect STDOUT to output.log, appending to the file instead.
command 2> error.log # Redirects STDERR to error.log !! This overwrites the file! Use two `>` to append.
command &> file.log # Redirects Output and Error to file.log
command > file.log 2>&1 # same as above
command 2>&1 # Redirects STDERR to STDOUT
command 2> errors.txt 1> output.txt # Redirects Error and Output to different files
command < file.txt # Redirects STDIN so it reads from file.txt
command1 | command2 # Redirects the STDOUT of command1 to the STDIN of command2
~~~
## Tee
This command allows you to write command output to a file and also redirect it to the STDOUT. Normally it is being used in a pipe.
~~~bash
command1 | tee output.txt | command2
~~~
## grep

grep looks for text.

~~~bash
cat text.txt | grep Hello # search for "Hello"
grep -v Hello ./text.txt # prints all lines that do not contain "Hello"
~~~

## locate

Very fast method to find files by their name. It uses a Search Database called mlocate.

~~~bash
locate file.txt # prints out all paths to files calles "file.txt"
locate -c file.txt # prints the number of results
sudo updatedb # updates the search database (mlocate)
~~~

## su

Substitute user changes the current user (default: root).

## who

Tells you who is logged in.

## Lists

~~~bash
command ./{element1,element2,element3}
~~~
## less

The less command allows you to scroll through a file (which may also be STDIN).

## echo

sh's `echo` builtin allows you to print strings to STDOUT.
Note that it is not well specified for anything more complicated than dumping output, so use printf instead.

~~~bash
echo "Hello World."
~~~

### Escape Code Flag

Bash permits the use of the `-e` flag for the interpretation of `\` escape codes.
Examples:
~~~bash
\b # backspace
\c # suppress newline
\n # newline
\r # carriage return
\t # tab (horizontal)
\v # tab (vertical)
\\ # backslash
~~~


## wall

`wall` (Write All) sends a message to all users.

~~~bash
wall "Hello. System Shutdown in 30 seconds." ; shutdown -h -t 30
~~~

## talk

`talk` let's you chat with logged in users. Note that it dumps your messages directly into their terminal.
Install it with apt. Use `mesg n` to forbid messages and `mesg y` to allow them.

~~~bash
talk customuser
~~~

## User Input

~~~bash
read variable1 variable2 variable3
~~~
## Arguments
### Number of arguments
~~~bash
$#
~~~
### Arguments
~~~bash
$0, $1, $2
~~~
## If-Statements
### if then
~~~bash
if command
then
  statement
fi
~~~
### if then else
~~~bash
if command
then
  statement1
else
  statement2
fi
~~~
## Using Operators
Most of the time you'll want to use the command `test`, or more likely, its short form,
`[`. If invoked with `[`, the last argument must be `]`.

Bash includes the built-in `[[`, which acts similarly, but is sometimes easier to use.

### Integer Comparison
~~~bash
-eq # equals
-ne # not equals
-gt # greater than
-ge # greater equal
-lt # lower than
-le # lower equal
~~~
### String comparison
~~~bash
= # is euqal to
== # is equal to
!= # is not equal to
< # less than
> # greater than
-z # is null (length of zero)
~~~
### Command chaining
~~~bash
&& # Run the command on the right if the command on the left ran successfully
|| # Run the command on the right if the command on the left ran unsuccessfully
~~~
Examples:
~~~bash
command1 && command2
~~~
Runs command2 only if command1 returns exit code 0.
~~~bash
command1 || command2
~~~
Runs command2 only if command1 doesn't return exit code 0.
## Arrays
### Definition
~~~bash
array=('element1' 'element2' 'element3')
~~~
### Outputting all elements
~~~bash
echo "${array[@]}"
~~~
### Outputting specific elements
~~~bash
echo "${array[0]}" # outputs 'element1'
~~~
### Outputting indices
~~~bash
echo "${!array[@]}"
~~~
### Appending item to array
~~~bash
array=('element1' 'element2')
array[2]='element3'
~~~
### Remove item from array
~~~bash
array=('element1' 'element2')
unset array[1] # removes 'element2' from array
~~~
## While-Loops
~~~bash
while command
do
  statement
done
~~~
## Until-Loops
~~~bash
until command
do
  statement
done
~~~
## For-Loops
~~~bash
# Elements from array
for element in array
do
  statement
done

# Word-split `command`'s STDOUT and loop over the words
for output in $(command)
do
  statement
done
~~~
## Functions

~~~bash
# declaring a function
print_something () {
	echo Hello I am a function
}
# calling a function
print_something
# declaring a function with arguments
print_something () {
	echo Hello $1
}
# calling a function with arguments
print_something Test
~~~

## File Permissions

### Users and Groups
Users have a name and a UID, unique ID.

Groups consist of multiple users and also have a name and a GID, group ID.
### Attribute String
~~~bash
d rwx r-x ---
1 2   3   4

# 1: Type
# 2: User
# 3: Group
# 4: Everyone
~~~
#### First Element (1 Character)
d = Directory

b = Block Device

c = Character Device

s = Socket

f = Pipeline

\- = File
#### Second to Fourth Element (3 Characters each)
r = Read Permission

w = Write Permission

x = Execution Permission

s = Execution Permission and setUID/GID

S = setUID/GID without execution permission

t = Sticky bit with execution permission

T = Sticky bit without execution permission

\- = No Right
### Octal Numbers
~~~bash
4 = Read
2 = Write
1 = Execute
0 = No Rights
~~~
All numbers added together define the permission for a file or folder.
### Examples
~~~bash
# No Rights: 0 / ---
# Executable: 1 / --x
# Writeable: 2 / -w-
# Readable: 4 / r--
# Executable + Writeable: 3 / -wx
# Executable + Readable: 5 / r-x
# Readable + Writeable: 6 / rw-
# Readable + Writeable + Executable: 7 rwx
~~~
### Special Rights
setUID: Run executable with the rights of the owner, not the one who is executing it (Octal 4).

setGID: Run executable with rights of the group, not the one of the executing group (Octal 2).

stickyBit (Octal 1):
	* On directories: For every file contained within: Only owner of the file can remove or rename the file.
	* On files: On old systems, executable files with this bit were put into swap space. Now, it does nothing.

## chmod

Change Mode sets the file permissions for a file or directory.

~~~bash
chmod +x file.sh # make file.sh executable
~~~

## chown

Change Owner sets the owner of a file or directory.

~~~bash
chown -R user:user ./directory/ # sets user "user" and group "user" as the owner of the directory as well as all files under it
~~~

## Find
### Permissions
~~~bash
find . -type -f -perm 0660 # Output all files that are readable and writeable for user and group
find . -type -f ! -perm 0777 # Output all file except those with 0777-Permissions
find . -type -perm 4777 # Output all files with setUID set
~~~
### Particular Users
~~~bash
find . -user alice
~~~
## Which, Whereis and Whatis
~~~bash
which command # outputs the pathnames where the command binary is stored
whereis command # outputs the pathnames of files under the path that contain `command`
whatis command # outputs a short description of command from manpages
~~~
## Creating users
### High Level

`useradd alice`. You will be prompted for other data.

### Low level
~~~bash
useradd alice -m -s /bin/bash -g users

-m # automatically create home directory
-s <shell> # set default shell
-g <group> # default user group
-c "<comment>" # define comment
~~~

## Remove users
### High Level

`deluser --backup-to /backup --remove-home alice`
* `--remove-home`: Delete home directory
* `--backup-to`: Create backup archive in directory specified
~~~bash
userdel -r alice

-r # delete home directory as well
~~~
## Group Management
~~~bash
groups # returns all groups connected to current user
cat /etc/group # returns all groups on system
groupadd mygroup # add a group named mygroup
gpasswd -a username groupname # adds user username to group groupname
gpasswd -d username groupname # deletes user username from group groupname
adduser username groupname # adds user username to group groupname
deluser username groupname # removes user username to group groupname
~~~
## .bashrc
.bashrc is being executed when a new shell or terminal session is opened. You can find it as a hidden file in every user directory.
A default file is also found in /etc/bashrc
## alias
alias defined shortcuts ('aliases') for commands.
~~~bash
alias shortname='command' # defines new alias
alias shortname # shows existing alias
unalias shortname # remove shortname alias
unalias -a # remove all aliases
~~~
## watch
Calls a command at regular time intervals and display its output
~~~bash
watch -n 1 command
# executes command every second
~~~
## head and tail
head prints first bytes, characters or lines of a file, while the tail command prints the last bytes, characters or lines
~~~bash
head -n 10 file.txt # shows first 10 lines of file.txt
tail -n 10 file.txt # shows last 10 lines of file.txt
tail -f file.txt # output appended data as the file grows
~~~
## wc
wc (Word Count) prints newline, word, and byte counts for each file.
You can select only one to be printed with `-l`, `-w` or `-c`
~~~bash
wc file.txt
1  6  42 file.txt
# 1: lines
# 6: words
# 42: characters
~~~
## tar Archive Management
Packing Archives:
~~~bash
tar -cvf archive.tar.gz archive
~~~
Unpacking Archives:
~~~bash
tar -xvf archive.tar.gz
~~~
## fstab
fstab contains information for automatically mounting partitions. Contents of this file are split into columns for each line.
Each column must be seperated from the last by whitespace, but the amount of whitespace does not matter.
~~~bash
<file system> <mount point> <filesystem type> <options> <dump> <pass>
/dev/sda      /mnt          ntfs              defaults  0      0
~~~

Some notes:

`dump` refers to an old backup utility. 0 disables.
`pass` configures fsck checking order on bootup. Lower numbers mean the file system is checked first. 0 disables.

It is recommended to use UUIDs (with `UUID=<uuid>`) where possible, as the numbering of devices is not guranteed to be consistent.
In addition, labels can be used (with `LABEL=<label>`) instead.

## Cronjobs
~~~bash
crontab -e # edit the current user's crontab
sudo crontab -e # edit the root user's crontab
~~~
Then configure the cronjob in the text editor.
## tmux Terminal Multiplexer
Basics
~~~bash
tmux new # new tmux Session
ctrl+B : # open tmux Prompt
ctrl+B d # detach tmux Session
tmux ls # show active tmux Sessions
tmux attach-session -t 0 # attach tmux Session 0
tmux a # attach latest tmux session
tmux kill-session -t 1 # kill Session 1
~~~
Naming Sessions
~~~bash
tmux new -s mysession # create a tmux Session named 'mysession'
tmux a -t mysession # attach the tmux Session 'mysession'
## a == attach-session
~~~
Panes
~~~bash
ctrl+B " # split Pane horizontally
ctrl+B % # split Pane vertically
ctrl+B ARROW_KEY # Switch between Panes
ctrl+B : # go to the tmux Console
ctrl+B resize-pane -D 2 # Resize Pane down by 2 lines
# U: up
# D: down
# L: left
# R: right
~~~
## Symbolic Links
Symbolic Links are Files that point to other files.

~~~bash
ln -s link_target link_name
~~~

## Formatting block devices

~~~bash
mkfs -t ext4 /dev/sda1 # format /dev/sda1 with ext4
# alternatively:
# mkfs.ext4 /dev/sda1 # format /dev/sda1 with ext4
~~~

## Boot Process

### Simplified Boot Process 

- BIOS runs the Bootloader
- Bootloader loads Initramfs + Kernel into Memory and starts the kernel
- Kernel starts **init** scripts of initramfs
- Kernel initializes services and drivers
- Kernel mounts / (root filesystem)
- Kernel starts **init** Program (PID 1)
- **init** starts Rest of System Processes

### Kernel Initialization

- CPU Inspection
- Memory Inspection
- Device Bus and Device Discovery
- Auxiliary Kernel Subsystem Setup
- Mount Root FS
- Start Userspace

## GRUB Bootloader

GRUB = Grand Unified Bootloader

Press "e" to view the Bootloader Config for the current Boot Option.

### GRUB Command Line

Startup: Press C inside the Boot Menu.

~~~bash
ls # list Devices
ls -l # more detailed device list
echo $root # determine GRUB root
ls ($root)/boot # go to /boot directory
set # view all current GRUB variables
~~~

### GRUB Configuration

File Path: /boot/grub/grub.cfg

**Do not edit grub.cfg directly! Use grub-mkconfig.**

/etc/grub.d provides shell scripts for grub-mkconfig.

~~~bash
grub-mkconfig # prints the configuration to the stdout
grub-mkconfig -o /boot/grub/grub.cfg # same as above but writes it to grub.cfg
~~~

### GRUB Installation

~~~bash
grub-install /dev/sda # install to /boot/grub
grub-install --boot-directory=/mnt/boot/ /dev/sdc # install to /mnt/boot
~~~

## Userspace Basics

### Intro to init

init is the first process of a linux system to start, with PID = 1. It executes all other processes.

Init Implementations:

- System V init: Traditional old version
- systemd: Standard for most distros
- Upstart: Ubuntu init (prior v15.04)

### Runlevels

Runlevels control the execution of processes and daemons in System V.
Systemd provides a rough mapping between runlevels and the respective targets.

~~~bash
0: Shutdown. Dismount Partitions. Close Network Connections.
1: Single-User emergency mode. Only the root user may log in.
2: Single-User Mode. No Network. Only local Resources.
3: Local Multi-User Mode. Network Init (Debian). Local Resources.
4: Multi-User Mode.
5: Graphical User Interface is running.
6: Reboot. Close Network Connections. Dismount Partitions.
~~~

### Changing Runlevels

~~~bash
init <runlevel> # = 1-6
~~~

### systemd

Systemd Startup:

- systemd loads config
- systemd determines boot goal (default.target)
- systemd loads boot goal dependencies
- systemd activates dependencies and default.target

### Units and Unit Types

A unit type is a systemd capability, like for example mounting Filesystems, Monitor Network Sockets, Run Timers. There are different Unit Types:

- Service Units (control daemons)
- Mount Units (control filesystem attachments)
- Target Units (control other Units)

## passwd

Changes the password for the specified user or the current user.
Requires root if not changing the current user's password.
If not root, requires the current user's password to confirm authenticity.

## sudo

sudo allows you to run commands as other users.

~~~bash
sudo passwd -d root # disable root login
~~~

Examples for /etc/sudoers:

~~~bash
root ALL = (ALL) ALL # Root may execute all commands with sudo
%administrator ALL = (ALL) ALL #  Group administrator my execute all commands with sudo
admin ALL = NOPASSWD: ALL # user admin may execute all programs without password input
user ALL = NOPASSWD: /usr/bin/python # user may execute /usr/bin/python without password input
~~~

## cmp

Compares two files byte by byte and outputs the position of the first difference.

## diff

Compares two files. If they are text files, print a human-readable difference, otherwise print if they differ.

## ftp

File Transfer Protocol Tool.

## curl

Allows you to download files from a server. It supports a wide range of network protocols: HTTP, FTP, HTTPS, LDAP, TELNET and others.

Example usage:

~~~bash
curl https://debian.org # get the main Debian webpage
curl http://10.10.0.123:8080 # get Ip 10.10.0.123 Port 8080
curl -o thatpage.html http://www.netscape.com # Store the web page to thatpage.html
curl -O www.haxx.se/index.html -O curl.haxx.se/download.html # fetch two files and store them with their remote name
curl -u name:passwd ftp://machine.domain:port/full/path/to/file # Download File from FTP Server with username and password
~~~

## Environment Variables

Environment Variables are Variables accessible by any shell and can for example define paths to executables or proxy configurations. They are different from Shell Variables.

Important commands:

~~~bash
KEY=value1:value2:value3 # Three values in one variable
KEY="value with spaces" # One String (with spaces) in a variable
env # print all set environment variables
echo $TEST_VAR # output value of TEST_VAR
export TEST_VAR # Convert Shell Variable into Environment Variable
export NEW_VAR="Testing export" # Set NEW_VAR as Environment Variable
export -n TEST_VAR # Convert Environment Variable to Shell Variable
unset TEST_VAR # Remove Shell Variable
~~~

## Killing Processes

You can either kill a process by its PID (Process IDentifier) or by its name:

~~~bash
kill 1234 # kill process with ID 1234
kill -SIGTERM 3139 # kill process 3139 with SIGTERM
killall python # kills all `python` processes
~~~

## man

Shows the manpages for a command, package, file, concept or system call, provided its documentation is installed on the system.

## Mounting devices

~~~bash
mount -l # list mounted devices
mount /dev/sda1 /mnt/mountpoint # mount /dev/sda1 to /mnt/mountpoint
umount /dev/sda1 # dismount device /dev/sda1
umount /mnt # dismount mountpoint /mnt
mount -a # mount all from fstab
umount -a # dismount all
~~~

## ping

Send ICMP Ping Requests to a machine by IP or hostname.

## Poweroff and Reboot

### systemd

~~~bash
systemctl poweroff # shut the machine down
systemctl reboot # reboot the machine
~~~

### Legacy
~~~bash
poweroff # poweroff the machine
reboot # reboot the machine
~~~

## ssh

~~~bash
ssh user@host[:port] # connect to server
ssh -D user@host[:port] # connect to server and create SOCKS Proxy
ssh -N user@host[:port] # connect but do not open a shell
~~~

## uname

Shows system information like

- Kernel name
- Hostname
- Processor Type
- Platform
- Kernel Version

depending on the arguments provided.

## wget

`wget` downloads files from HTTP/HTTPS/FTP Servers. Similar to `curl`, but always stores to a file, using the file name provided in the url.

~~~bash
wget https://cdimage.parrotsec.org/parrot/iso/4.5.1/Parrot-security-4.5.1_amd64.iso # Download ISO
~~~

## whoami

`whoami` prints information about the current user.

~~~bash
whoami # returns the current user name
~~~

## File System Structure

- / (root directory)
- /bin (Essential user command binaries)
  - "Basic" Regular Linux Commands
  - bash, grep, ls, ... ...
- /boot (Boot Loader)
  - initrd
  - grub config files
  - vmlinuz
- /dev (Device Files)
  - sdX
  - ttyX
  - usbX
- /etc (System Configuration Files)
  - configuration files
- /home (User Home Directories)
  - user folders
    - .bashrc
    - other user files
- /lib, /lib32, /lib64 (Shared Libraries)
  - libraries for /bin
  - libraries for /sbin
  - Shared Object Files
- /media (Automatic mounts)
  - The mountpoints in this directory are managed by programs that require no or little user input (file browsers, etc.)
  - cdrom
  - floppy
  - HDDs
  - USB Sticks
- /mnt (Mounted Filesystems)
  - Mountpoints for manually mounted file systems should go here
- /opt (Application Software Packages)
- /proc (Process Information)
  - Process ID folders
    - Process information
  - System Resources (like uptime)
- /sbin (System Binaries)
  - These normally require root
  - `init`, `route`, `fsck`, `iptables`, `reboot`, `fdisk`, `ifconfig`, `swapon`
- /srv (Data for System Services)
- /tmp (Temporary Files)
- /usr (User Utilities and Applications)
  - bin/
    - Non-essential programs
  - games/
    - Games and "entertainment" programs like espdiff or sl
  - include/
    - Header files
  - lib/, lib32/, lib64/
    - Libraries for programs in /usr/bin or /usr/local/bin
  - local/
    - Locally built applications
    - The same directory structure as /usr, except without the local/ folder.
  - sbin/
    - Non-essential system programs.
    - `chroot`, `grub-install`, `sendmail`, `visudo`
  - share/
    - Various files used by programs
    - Man pages are under the man/ directory in this folder
  - src/
    - Source code

## Kernel Modules

Kernel Modules extend or are part of the Linux Kernel. Examples:

- WiFi Driver
- Sound Card Driver
- USB Device Driver

### Displaying loaded Modules

~~~bash
# two ways to display kernel modules
kmod list
lsmod
~~~

### modinfo - Showing Module Information

~~~bash
modinfo snd # show info for snd module

~~~

### modprobe - Loading and Unloading Modules

With modprobe you can load or unload kernel modules at runtime.

~~~bash
modprobe -n MODULENAME # simulate loading a module
modprobe -a MODULENAME # load a module
modprobe -r MODULENAME # unload module
modprobe --show-depends MODULENAME # show dependencies  of a module
~~~

### depmod - Module Dependencies

depmod can be used to recreate the file **/lib/modules/KERNELVERSION/modules.dep** when adding custom modules to the kernel.

### Loading modules automatically

To load a module automatically, just add it's name to **/etc/modules**

### Blacklisting

You can disallow a module to be loaded automatically by using a blacklist. You can find the blacklist under **/etc/modprobe.d**, normally inside the file **blacklist.conf**.

## Regular Expressions

~~~bash
. # matches a single character
\ # escape character
.* # matches any string
$ # end of a line
[] # range
| # logical OR
[^] # logical NOT
~~~

## Wildcards

~~~bash
? # single character
* # any number of characters
[a-c] # range of characters
{} # list of items
~~~

## sed

sed is the Linux Stream Editor. It is a non-interactive Text Editor for the Console. You can run sed like this:

~~~bash
sed SED_SCRIPT FILE # general sed command
~~~

## history

The history command displays the commands you typed in as a particular user.

~~~bash
history # shows the last commands
history -c # clears the command history
~~~

## dig

This queries DNS Servers for information about host addresses, MX records, nameserver and other information.
