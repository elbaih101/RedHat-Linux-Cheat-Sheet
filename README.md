
<details><summary>ACCESSING THE COMMAND LINE</summary><p>
whoami : to know the current user
cat (file name) : read file

## ACCESSING THE COMMAND LINE
# EXECUTING COMMANDS USING THE BASH SHELL

```bash
whoami                      # Output The Current USERNAME.
date                        # Display or set the system date and time.
su``                        # Switch User.
passwd                      # Change user password.
man                         # Command-line tool for displaying comprehensive documentation (manual pages) for other commands and utilities. 
--help                      # Command-line option that displays a brief description of the usage and available options for the specified command or utility.

```
'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'
</p>
</details>

<details><summary>DESCRIBING LINUX FILE SYSTEM HIERARCHY CONCEPTS</summary><p>
## DESCRIBING LINUX FILE SYSTEM HIERARCHY CONCEPTS

<p align="center">
<img src = 'https://imgur.com/HoAqQ6H'>
</p>

'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'
</p>
</details>
<details><summary>Navigating Directories</summary><p>
## Navigating Directories

```bash
pwd                       # Print current directory path
ls                        # List directories
ls -a|--all               # List directories including hidden
ls -l                     # List directories in long form
ls -l -h|--human-readable # List directories in long form with human readable sizes
ls -t                     # List directories by modification time, newest first
ls -lR /Directory (& or 2)> lsfile 			# Lists all files recursively in a directory and saves the output to a file named "lsfile". Any errors that occur during the process will also be saved to the same file.
ls -lR /Directory | tee Filename | less     # Lists all files recursively in a directory, saves the output to a file named "Filename", and displays the output in the pager "less".
stat foo.txt              # List size, created and modified timestamps for a file
stat foo                  # List size, created and modified timestamps for a directory
tree                      # List directory and file tree
tree -a                   # List directory and file tree including hidden
tree -d                   # List directory tree
cd foo                    # Go to foo sub-directory
cd                        # Go to home directory
cd ~                      # Go to home directory
cd -                      # Go to last directory
pushd foo                 # Go to foo sub-directory and add previous directory to stack
popd                      # Go back to directory in stack saved by `pushd`
```
'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'
</p>
</details>

<details><summary>Directories Commands</summary><p>
touch : to Create file or Edit 
touch with . (before file name) : Create hidden file


## Creating Files

```bash
touch foo.txt          # Create file or update existing files modified timestamp
touch foo.txt bar.txt  # Create multiple files
touch {foo,bar}.txt    # Create multiple files
touch test{1..3}       # Create test1, test2 and test3 files
touch test{a..c}       # Create testa, testb and testc files

mktemp                 # Create a temporary file
```
'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'
mkdir : Create directory

## Creating Directories

```bash
mkdir foo                        # Create a directory
mkdir foo bar                    # Create multiple directories
mkdir -p|--parents foo/bar       # Create nested directory
mkdir -p|--parents {foo,bar}/baz # Create multiple nested directories
mktemp -d|--directory            # Create a temporary directory
```
'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'

cp (file name) [file directory] "optional" (new file name) : copy file
mv (file name) [file directory] "optional" (new file name) : move file
mv (file name) (new file name) : rename file

## Moving Directories

```bash
cp -R|--recursive foo bar                               # Copy directory
mv foo bar                                              # Move directory

rsync -z|--compress -v|--verbose /foo /bar              # Copy directory, overwrites destination
rsync -a|--archive -z|--compress -v|--verbose /foo /bar # Copy directory, without overwriting destination
rsync -avz /foo username@hostname:/bar                  # Copy local directory to remote directory
rsync -avz username@hostname:/foo /bar                  # Copy remote directory to local directory
```


'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'


rm (file name or directory) : Delete
rmdir (directory name) : delete empty directory


## Deleting Directories

```bash
rmdir foo                        # Delete empty directory
rm -r|--recursive foo            # Delete directory including contents
rm -r|--recursive -f|--force foo # Delete directory including contents, ignore nonexistent files and never prompt
```

## Deleting Files

```bash
rm foo.txt            # Delete file
rm -f|--force foo.txt # Delete file, ignore nonexistent files and never prompt
```

'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'


## Reading Files

```bash
file                   # Determine file type
cat foo.txt            # Print all contents
more                   # view the contents of a file one page at a time.
less foo.txt           # Print some contents at a time (g - go to top of file, SHIFT+g, go to bottom of file, /foo to search for 'foo')
head foo.txt           # Print top 10 lines of file
tail foo.txt           # Print bottom 10 lines of file
open foo.txt           # Open file in the default editor
wc foo.txt             # List number of lines words and characters in the file
wc -l /etc/passwd/ 		    # all users
```

'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'


echo "contant" > (file name) : edit replace
echo "contant" >> (file name) : edit add new line
echo : print



## Standard Output, Standard Error and Standard Input

```bash
echo "foo" > bar.txt       # Overwrite file with content
echo "foo" >> bar.txt      # Append to file with content

ls exists 1> stdout.txt    # Redirect the standard output to a file
ls noexist 2> stderror.txt # Redirect the standard error output to a file
ls 2>&1 out.txt            # Redirect standard output and error to a file
ls > /dev/null             # Discard standard output and error

read foo                   # Read from standard input and write to the variable foo
```

'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'
</p>
</details>

<details><summary>Search</summary><p>

## Finding Files

Find binary files for a command.

```bash
type wget                                  # Find the binary
which wget                                 # Find the binary
whereis wget                               # Find the binary, source, and manual page files
```

`locate` uses an index and is fast.

```bash
updatedb                                   # Update the index

locate foo.txt                             # Find a file
locate --ignore-case                       # Find a file and ignore case
locate f*.txt                              # Find a text file starting with 'f'
```

`find` doesn't use an index and is slow.

```bash
find /path -name foo.txt                   # Find a file
find /path -iname foo.txt                  # Find a file with case insensitive search
find /path -name "*.txt"                   # Find all text files
find /path -name foo.txt -delete           # Find a file and delete it
find /path -name "*.png" -exec pngquant {} # Find all .png files and execute pngquant on it
find /path -type f -name foo.txt           # Find a file
find /path -type d -name foo               # Find a directory
find /path -type l -name foo.txt           # Find a symbolic link
find /path -type f -mtime +30              # Find files that haven't been modified in 30 days
find /path -type f -mtime +30 -delete      # Delete files that haven't been modified in 30 days

```


'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'


grep
grep -e -*(pattern) FileDirectory 


## Find in Files

```bash
grep 'foo' /bar.txt                         # Search for 'foo' in file 'bar.txt'
grep 'foo' /bar -r|--recursive              # Search for 'foo' in directory 'bar'
grep 'foo' /bar -R|--dereference-recursive  # Search for 'foo' in directory 'bar' and follow symbolic links
grep 'foo' /bar -l|--files-with-matches     # Show only files that match
grep 'foo' /bar -L|--files-without-match    # Show only files that don't match
grep 'Foo' /bar -i|--ignore-case            # Case insensitive search
grep 'foo' /bar -x|--line-regexp            # Match the entire line
grep 'foo' /bar -C|--context 1              # Add N line of context above and below each search result
grep 'foo' /bar -v|--invert-match           # Show only lines that don't match
grep 'foo' /bar -c|--count                  # Count the number lines that match
grep 'foo' /bar -n|--line-number            # Add line numbers
grep 'foo' /bar --colour                    # Add colour to output
grep 'foo\|bar' /baz -R                     # Search for 'foo' or 'bar' in directory 'baz'
grep --extended-regexp|-E 'foo|bar' /baz -R # Use regular expressions
egrep 'foo|bar' /baz -R                     # Use regular expressions
```

'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'
</p>
</details>

<details><summary>Compressing Files</summary><p>

tar (-c:create, -x:extract,f:filename) 	# Command-line tool for creating and extracting tar archives.
tar -cf archive.tar file1 file2 file3 	# Creates a tar archive named "archive.tar" containing the specified files.
tar -tf archive.tar 			# Lists the contents of a tar archive.
-z or --gzip 				# Flag for gzip compression.
-j or --bzip2 				# Flag for bzip2 compression.
-J or -xz 				# Flag for xz compression.

## Compressing Files

### zip

Compresses one or more files into *.zip files.

```bash
zip foo.zip /bar.txt                # Compress bar.txt into foo.zip
zip foo.zip /bar.txt /baz.txt       # Compress bar.txt and baz.txt into foo.zip
zip foo.zip /{bar,baz}.txt          # Compress bar.txt and baz.txt into foo.zip
zip -r|--recurse-paths foo.zip /bar # Compress directory bar into foo.zip
```

### gzip

Compresses a single file into *.gz files.

```bash
gzip /bar.txt foo.gz           # Compress bar.txt into foo.gz and then delete bar.txt
gzip -k|--keep /bar.txt foo.gz # Compress bar.txt into foo.gz
```

### tar -c

Compresses (optionally) and combines one or more files into a single *.tar, *.tar.gz, *.tpz or *.tgz file.

```bash
tar -c|--create -z|--gzip -f|--file=foo.tgz /bar.txt /baz.txt # Compress bar.txt and baz.txt into foo.tgz
tar -c|--create -z|--gzip -f|--file=foo.tgz /{bar,baz}.txt    # Compress bar.txt and baz.txt into foo.tgz
tar -c|--create -z|--gzip -f|--file=foo.tgz /bar              # Compress directory bar into foo.tgz
```

## Decompressing Files

### unzip

```bash
unzip foo.zip          # Unzip foo.zip into current directory
```

### gunzip

```bash
gunzip foo.gz           # Unzip foo.gz into current directory and delete foo.gz
gunzip -k|--keep foo.gz # Unzip foo.gz into current directory
```

### tar -x

```bash
tar -x|--extract -z|--gzip -f|--file=foo.tar.gz # Un-compress foo.tar.gz into current directory
tar -x|--extract -f|--file=foo.tar              # Un-combine foo.tar into current directory
```


'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'
</p>
</details>
<details><summary>File Permissions</summary><p>
  
chmod u[+-=](rwx)or(
chown ahmed:data data
## File Permissions

| # | Permission              | rwx | Binary |
| - | -                       | -   | -      |
| 7 | read, write and execute | rwx | 111    |
| 6 | read and write          | rw- | 110    |
| 5 | read and execute        | r-x | 101    |
| 4 | read only               | r-- | 100    |
| 3 | write and execute       | -wx | 011    |
| 2 | write only              | -w- | 010    |
| 1 | execute only            | --x | 001    |
| 0 | none                    | --- | 000    |

For a directory, execute means you can enter a directory.

| User | Group | Others | Description                                                                                          |
| -    | -     | -      | -                                                                                                    |
| 6    | 4     | 4      | User can read and write, everyone else can read (Default file permissions)                           |
| 7    | 5     | 5      | User can read, write and execute, everyone else can read and execute (Default directory permissions) |

- u - User
- g - Group
- o - Others
- a - All of the above

```bash
ls -l /foo.sh            # List file permissions
chmod +100 foo.sh        # Add 1 to the user permission
chmod -100 foo.sh        # Subtract 1 from the user permission
chmod u+x foo.sh         # Give the user execute permission
chmod g+x foo.sh         # Give the group execute permission
chmod u-x,g-x foo.sh     # Take away the user and group execute permission
chmod u+x,g+x,o+x foo.sh # Give everybody execute permission
chmod a+x foo.sh         # Give everybody execute permission
chmod +x foo.sh          # Give everybody execute permission
```

'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'
</p>
</details>
<details><summary>Symbolic Links</summary><p>
  
ln -s S.Directory D.Directory
ln S.Directory D.Directory

## Symbolic Links

```bash
ln -s|--symbolic foo bar            # Create a link 'bar' to the 'foo' folder
ln -s|--symbolic -f|--force foo bar # Overwrite an existing symbolic link 'bar'
ls -l                               # Show where symbolic links are pointing
```

'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'
</p>
</details>
<details><summary>Identifying Processes</summary><p>

  
top
htop
ps 
ls -l | grep fil
ps aux | grep 
pg
Control Jobs sleep 1000 &   list jobs | choose fg | stop Ctrl Z | run bg | Kill Ctrl C
Kill Process kill ProcessID | Force Kill kill -9 ProcessID | pkill ProcessName 
Monitor Process , uptime | 
Prioeity sudo renice (+ or - number to nice value) ProcessID

## Identifying Processes

```bash
top                    # List all processes interactively
htop                   # List all processes interactively
ps 
ps aux | grep 
ps all                 # List all processes
pg
pidof foo              # Return the PID of all foo processes

CTRL+Z                 # Suspend a process running in the foreground
bg                     # Resume a suspended process and run in the background
fg                     # Bring the last background process to the foreground
fg 1                   # Bring the background process with the PID to the foreground

sleep 30 &             # Sleep for 30 seconds and move the process into the background
jobs                   # List all background jobs
jobs -p                # List all background jobs with their PID

lsof                   # List all open files and the process using them
lsof -itcp:4000        # Return the process listening on port 4000
```

## Process Priority

Process priorities go from -20 (highest) to 19 (lowest).

```bash
nice -n -20 foo        # Change process priority by name
renice 20 PID          # Change process priority by PID
ps -o ni PID           # Return the process priority of PID
```

## Killing Processes

```bash
CTRL+C                 # Kill a process running in the foreground
kill PID               # Shut down process by PID gracefully. Sends TERM signal.
kill -9 PID            # Force shut down of process by PID. Sends SIGKILL signal.
pkill foo              # Shut down process by name gracefully. Sends TERM signal.
pkill -9 foo           # force shut down process by name. Sends SIGKILL signal.
killall foo            # Kill all process with the specified name gracefully.
```

'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'
</p>
</details>

<details><summary>Scheduled Tasks</summary><p>
  
## Scheduled Tasks

```pre
   *      *         *         *           *
Minute, Hour, Day of month, Month, Day of the week
```

```bash
crontab -l                 # List cron tab
crontab -e                 # Edit cron tab in Vim
crontab /path/crontab      # Load cron tab from a file
crontab -l > /path/crontab # Save cron tab to a file

* * * * * foo              # Run foo every minute
*/15 * * * * foo           # Run foo every 15 minutes
0 * * * * foo              # Run foo every hour
15 6 * * * foo             # Run foo daily at 6:15 AM
44 4 * * 5 foo             # Run foo every Friday at 4:44 AM
0 0 1 * * foo              # Run foo at midnight on the first of the month
0 0 1 1 * foo              # Run foo at midnight on the first of the year

at -l                      # List scheduled tasks
at -c 1                    # Show task with ID 1
at -r 1                    # Remove task with ID 1
at now + 2 minutes         # Create a task in Vim to execute in 2 minutes
at 12:34 PM next month     # Create a task in Vim to execute at 12:34 PM next month
at tomorrow                # Create a task in Vim to execute tomorrow
```

'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'
</p>
</details>
  
<details><summary>SystemD and Services</summary><p>
  
## SystemD and Services
```bash
systemctl 						# Controls the systemd system and service manager.
systemctl -t help 					# Displays help information about systemd unit types.
systemctl list-units -t service 			# Lists all active systemd services on the system.
systemctl --faild -type-service 			# Lists all failed systemd services of type "service".
systemctl start ___ 					# Starts a systemd service with the specified name.
systemctl is-active ___ 				# Checks if a systemd service with the specified name is currently active.
systemctl stop ___ 					# Stops a systemd service with the specified name.
systemctl enable ___ 					# Enables a systemd service with the specified name to start automatically at boot time.
systemctl restart ___ 					# Restarts a systemd service with the specified name.
systemctl reload ____ 					# Reloads the configuration of a systemd service with the specified name.
systemctl reload-or-restart ___ 			# Reloads the configuration of a systemd service with the specified name, or restarts it if the reload fails.
systemctl list-dependencies ___ 			# Lists the dependencies of a systemd unit with the specified name.
systemctl list-dependencies --reverse ___ 		# Lists the reverse dependencies of a systemd unit with the specified name.
systemctl status (sshd) 				# Displays the status of the "sshd" systemd service.
```

'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'
</p>
</details>
  
<details><summary>System Logging and Journaling</summary><p>
  
## System Logging and Journaling
```bash
system Logging /var/log/ 				# Directory containing system logs.
Journal entries 					# Log entries generated by the systemd journal.
```

'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'
</p>
</details>
  
<details><summary>Networking</summary>
<p>
  
## Networking
```bash
nmcli 							# Command-line tool for managing NetworkManager.
nmtui 							# Text-based user interface for managing NetworkManager.
ip addr 						# Displays network interface configuration information.
ip config 						# Displays IP configuration information.
ip route 						# Displays the system's routing table.
tracepath 						# Traces the path that a packet takes from the host system to a remote system.
ping 							# Sends ICMP echo request packets to a remote system to test connectivity.
hostname 						# Displays or sets the system's hostname.
hostnamectl						# Command-line tool for managing the system's hostname.
hostnamectl status 					# Displays the current hostname and related information.
cat /etc/sysconfig/network-scripts//ifcfg-enp0s3 	# Displays the configuration file for the "enp0s3" network interface.
cat /etc/hosts 						# Displays the system's hosts file.
cat /etc/resolv.cof					# Displays the system's DNS resolver configuration file.
```

'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'
</p>
</details>
<details><summary>Miscellaneous</summary><p>

## Miscellaneous
```bash	
acl 							# Command-line tool for managing file ACLs (Access Control Lists).
getfacl FileName 					# Displays the ACLs for the specified file.
setfacl -m u:user:(r,w,x) FileName 			# Adds or modifies the ACL for the specified file, giving the user "user" read, write, and execute permissions.
ls -laR >						# Lists all files recursively in a directory, including hidden files, and saves the output to standard output.
```

'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'
</p>
</details>
<details><summary>User and Group Managemen</summary><p>

 
## User and Group Management
```bash	
sudo usermod -aG groubname username 			# Adds the user "username" to the group "groupname".
sudo usermod -aG wheel mali 				# Adds the user "mali" to the "wheel" group, which typically grants administrative privileges.
sudo userdel 						# Command-line tool for deleting a user.
sudo useradd 						# Command-line tool for adding a new user.
id user 						# Displays information about the user with the specified username.
groups 							# Lists the groups that the current user belongs to.
cat /etc/group 						# Displays the system's group database.
umask 							# Command-line tool for setting the default permissions for new files and directories.
sudo chage -m 0 -M 90 -W 7 -I 14 user03 		# Changes the password aging settings for the user "user03".
sudo usermod -L user03 					# Locks the password for the user "user03".
sudo groupadd groupname 				# Command-line tool for creating a new group.
```
'~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~'
</p>
</details>
