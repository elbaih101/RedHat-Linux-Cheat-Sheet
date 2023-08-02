
<details><summary>ACCESSING THE COMMAND LINE</summary><p>
  
# EXECUTING COMMANDS USING THE BASH SHELL

```bash
whoami    # Output The Current USERNAME.
date      # Display or set the system date and time.
su        # Switch User.
passwd    # Change user password.
whatis    # Show the command’s description in one line
man       # Command-line tool for displaying comprehensive documentation (manual pages).
--help    # Command-line option that displays a brief description of the usage and available options.

```

--------------------------------------------------------------------------------------------------
<p>
</details>

<details><summary>DESCRIBING LINUX FILE SYSTEM HIERARCHY CONCEPTS</summary><p>

## DESCRIBING LINUX FILE SYSTEM HIERARCHY CONCEPTS
--------------------------------------------------------------------------------------------------
<p align="center">

<img src="https://i.imgur.com/HoAqQ6H.png">
  
</p>

--------------------------------------------------------------------------------------------------

</p>
</details>
<details><summary>Navigating Directories</summary><p>
  
## Navigating Directories

```bash
pwd                                          # Print current directory path
ls                                           # List directories
ls -a|--all                                  # List directories including hidden
ls -l                                        # List directories in long form
ls -l -h|--human-readable                    # List directories in long form with human readable sizes
ls -t                                        # List directories by modification time, newest first
ls -lR /Directory (& or 2)> lsfile 			     # Lists all files recursively in a directory and saves the output to a file named "lsfile". Any errors that occur during the process will also be saved to the same file.
ls -lR /Directory | tee Filename | less      # Lists all files recursively in a directory, saves the output to a file named "Filename", and displays the output in the pager "less".
stat filename.txt                            # List size, created and modified timestamps for a file
stat filename.txt                            # List size, created and modified timestamps for a directory
tree                                         # List directory and file tree
tree -a                                      # List directory and file tree including hidden
tree -d                                      # List directory tree
cd Directory                                 # Go to sub-directory
cd                                           # Go to home directory
cd ~                                         # Go to home directory
cd -                                         # Go to last directory
pushd directoryname                          # Go to directoryname sub-directory and add previous directory to stack
popd                                         # Go back to directory in stack saved by `pushd`
```
--------------------------------------------------------------------------------------------------

</p>

</details>

<details><summary>Directories Commands</summary><p>

## Creating Directories

```bash
mkdir directoryname                                          # Create a directory
mkdir directoryname1 directoryname2                          # Create multiple directories
mkdir -p|--parents directoryname1/directoryname2             # Create nested directory
mkdir -p|--parents {directoryname1,directoryname2}/directory # Create multiple nested directories
mktemp -d|--directory                                        # Create a temporary directory
```
--------------------------------------------------------------------------------------------------
## Moving Directories

```bash 
cp -R|--recursive directoryname1 directoryname2                # Copy directory
mv directoryname1 directoryname2                               # Move directory

rsync -z|--compress -v|--verbose /file /directory              # Copy directory, overwrites destination
rsync -a|--archive -z|--compress -v|--verbose /file /directory # Copy directory, without overwriting destination
rsync -avz /directoryname username@hostname:/directory         # Copy local directory to remote directory
rsync -avz username@hostname:/file /directory                  # Copy remote directory to local directory
```
--------------------------------------------------------------------------------------------------
## Deleting Directories

```bash
rmdir directoryname                        # Delete empty directory
rm -r|--recursive directoryname            # Delete directory including contents
rm -r|--recursive -f|--force directoryname # Delete directory including contents, ignore nonexistent files and never prompt
```
--------------------------------------------------------------------------------------------------
</p>
</details>

<details><summary>File Commands</summary><p>
  
## Creating Files

```bash
touch filename.txt                           # Create file or update existing files modified timestamp
touch filename1.txt  filename2.txt           # Create multiple files
touch {filename1.txt,filename2.txt }.txt     # Create multiple files
touch test{1..3}                             # Create test1, test2 and test3 files
touch test{a..c}                             # Create testa, testb and testc files
touch .(file name)                           # Create hidden file
mktemp                                       # Create a temporary file
```
--------------------------------------------------------------------------------------------------
## Copy, Move & Rename Files

```bash
cp filename.txt filedirectory "optional" newfilename.txt   # Copy file
mv filename.txt filedirectory "optional" newfilename.txt   # Move file
mv filename.txt newfilename.txt                            # Rename file
```
--------------------------------------------------------------------------------------------------
## Deleting Files

```bash
rm filename.txt            # Delete file
rm -f|--force filename.txt # Delete file, ignore nonexistent files and never prompt
```
--------------------------------------------------------------------------------------------------
## Reading Files

```bash
file                   # Determine file type
cat filename.txt       # Print all contents
more                   # view the contents of a file one page at a time.
less filename.txt      # Print some contents at a time (g - go to top of file, SHIFT+g, go to bottom of file)
head filename.txt      # Print top 10 lines of file
tail filename.txt      # Print bottom 10 lines of file
open filename.txt      # Open file in the default editor
wc filename.txt        # List number of lines words and characters in the file
wc -l /etc/passwd/ 	  # all users
```
--------------------------------------------------------------------------------------------------
## Standard Output, Standard Error and Standard Input

```bash
echo "Words" > filename.txt   # Overwrite file with content
echo "Words" >> filename.txt  # Append to file with content

ls exists 1> filename.txt     # Redirect the standard output to a file
ls noexist 2> filename.txt    # Rdirect the standard error output to a file
ls 2>&1 filename.txt          # Redirect standard output and error to a file
ls > /dev/null                # Discard standard output and error
```
--------------------------------------------------------------------------------------------------

</p>

</details>

<details><summary>Search</summary><p>

## Finding Files

Find binary files for a command.

```bash
type wget                   # Find the binary
which wget                  # Find the binary
whereis wget                # Find the binary, source, and manual page files
```

`locate` uses an index and is fast.

```bash
updatedb                     # Update the index

locate filename.txt          # Find a file
locate --ignore-case         # Find a file and ignore case
locate f*.txt                # Find a text file starting with 'f'
```

`find` doesn't use an index and is slow.

```bash
find /path -name filename.txt                # Find a file
find /path -iname filename.txt               # Find a file with case insensitive search
find /path -name "*.txt"                     # Find all text files
find /path -name filename.txt -delete        # Find a file and delete it
find /path -name "*.png" -exec pngquant {}   # Find all .png files and execute pngquant on it
find /path -type f -name filename.txt        # Find a file
find /path -type d -name directory           # Find a directory
find /path -type l -name filename.txt        # Find a symbolic link
find /path -type f -mtime +30                # Find files that haven't been modified in 30 days
find /path -type f -mtime +30 -delete        # Delete files that haven't been modified in 30 days

```


--------------------------------------------------------------------------------------------------

## Find in Files

```bash
grep 'foo' /filename.txt                          # Search for 'foo' in file 'filename.txt'
grep 'foo' /directory -r|--recursive              # Search for 'foo' in directory 
grep 'foo' /directory -R|--dereference-recursive  # Search for 'foo' in directory and follow symbolic links
grep 'foo' /directory -l|--files-with-matches     # Show only files that match
grep 'foo' /directory -L|--files-without-match    # Show only files that don't match
grep 'Foo' /directory -i|--ignore-case            # Case insensitive search
grep 'foo' /directory -x|--line-regexp            # Match the entire line
grep 'foo' /directory -C|--context 1              # Add N line of context above and below each search result
grep 'foo' /directory -v|--invert-match           # Show only lines that don't match
grep 'foo' /directory -c|--count                  # Count the number lines that match
grep 'foo' /directory -n|--line-number            # Add line numbers
grep 'foo' /directory --colour                    # Add colour to output
grep 'foo\|bar' /directory -R                     # Search for 'foo' or 'bar' in directory
grep --extended-regexp|-E 'foo|bar' /directory -R # Use regular expressions
egrep 'foo|bar' /directory -R                     # Use regular expressions
grep -e 'pattern' filename.txt                    # Use to find search patterns 
```

--------------------------------------------------------------------------------------------------
</p>
</details>

<details><summary>Compressing Files</summary><p>

  
## Compressing Files

### tar 
```bash
tar (-c:create, -x:extract, -t:list, f:filename) 	# Command-line tool for creating and extracting tar archives.
tar -cf archive.tar file1 file2 file3 	            # Creates a tar archive named "archive.tar" containing the specified files.
tar -tf archive.tar 		                	         # Lists the contents of a tar archive.
-z or --gzip 	.tar.gz			                     # Flag for gzip compression.
-j or --bzip2 	.tar.bz2			                     # Flag for bzip2 compression.
-J or -xz 		.tar.xz	                      	   # Flag for xz compression.
```

### tar -c

Compresses (optionally) and combines one or more files into a single *.tar, *.tar.gz, *.tpz or *.tgz file.

```bash
tar -c|--create -z|--gzip -f|--file=Cfilename.tar /file1.txt /file2.txt # Compress file1.txt and file2.txt into Cfilename.tar
tar -c|--create -z|--gzip -f|--file=Cfilename.tar /{file1,file2}.txt    # Compress file1.txt and file2.txt into Cfilename.tar
tar -c|--create -z|--gzip -f|--file=Cfilename.tar /file                 # Compress directory bar into Cfilename.tar
```

### zip

Compresses one or more files into *.zip files.

```bash
zip Cfilename.zip /file.txt                     # Compress file.txt into Cfilename.zip
zip Cfilename.zip /file1.txt /file2.txt         # Compress file1.txt and file2.txt into Cfilename.zip
zip Cfilename.zip /{file1,file2}.txt            # Compress file1.txt and file2.txt into Cfilename.zip
zip -r|--recurse-paths Cfilename.zip /directory # Compress directory into Cfilename.zip
```

### gzip

Compresses a single file into *.gz files.

```bash
gzip /file.txt Cfilename.gz              # Compress file.txt into Cfilename.gz and then delete bar.txt
gzip -k|--keep /bafiler.txt Cfilename.gz # Compress file.txt into Cfilename.gz
```

## Decompressing Files

### tar -x

```bash
tar -x|--extract -z|--gzip -f|--file=Cfilename.tar.gz # Un-compress Cfilename.tar.gz into current directory
tar -x|--extract -f|--file=Cfilename.tar              # Un-combine Cfilename.tar into current directory
```

### unzip

```bash
unzip Cfilename.zip          # Unzip Cfilename.zip into current directory
```

### gunzip

```bash
gunzip Cfilename.gz           # Unzip Cfilename.gz into current directory and delete Cfilename.gz
gunzip -k|--keep Cfilename.gz # Unzip Cfilename.gz into current directory
```


--------------------------------------------------------------------------------------------------

</p>
</details>

<details><summary>User Administration</summary>
<p>

## User and Group Management
`User Management`
```bash
useradd -g itadmin -c "DB User" -u 1135 -s "/bin/sh" -d /home/techguy1 
# In the above command, we are creating the new user with custom options as simple "#useradd <user>" will create with default setting. The -g (group) -c (description) -u (user id) -s (which shell to be assigned) -d (landed home dir)
sudo useradd -g <primary group> -G <secondary group> username # assign the user primary and secondary group
usermod -aG groubname username                                # Adds the user "username" to the group "groupname".
usermod -aG wheel username			                              # Adds the user "username" to the "wheel" group, which typically grants administrative privileges.
usermod -L username                                           # locking user
usermod -U username                                           # unlocking user
userdel username						                                  # Command-line tool for deleting a user, leaves his home directory intact.
userdel -r username                                           # Command-line tool for deleting a user and also deletes his home directory.
id user 						                                          # Displays information about the user with the specified username.
umask 							                                          # Command-line tool for setting the default permissions for new files and directories.
```
`Group Management`
```bash
groups 							                                          # Lists the groups that the current user belongs to.
cat /etc/group 						                                    # Displays the system's group database.
groupadd groupname 				                                    # Command-line tool for creating a new group.
groupdel groupname                                            # removes an existing group
```
`Password Management`
```bash
chage                                                         # set password expiry
chage -m 0 -M 90 -W 7 -I 14 user03                            # Changes the password aging settings for the user "user03".
passwd -l username                                            # locking password of user
passwd -u username                                            # unlocking password of user
passwd -e username                                            # expire password
passwd -x -1 username                                         # Turnoff password expiry
echo 'myPassword123' | sudo passwd --stdin username
```
--------------------------------------------------------------------------------------------------

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
ls -l /file.sh            # List file permissions
chmod +100 file.sh        # Add 1 to the user permission
chmod -100 file.sh        # Subtract 1 from the user permission
chmod u+x file.sh         # Give the user execute permission
chmod g+x file.sh         # Give the group execute permission
chmod u-x,g-x file.sh     # Take away the user and group execute permission
chmod u+x,g+x,o+x file.sh # Give everybody execute permission
chmod a+x file.sh         # Give everybody execute permission
chmod +x file.sh          # Give everybody execute permission
chown USER file.sh        # Change the owner
```

--------------------------------------------------------------------------------------------------
</p>
</details>

<details><summary>Access Control Lists (ACLs)</summary><p>

## Access Control Lists (ACLs)
```bash	
getfacl FileName 					      # Displays the ACLs for the specified file.
setfacl -m u:user:(r,w,x) FileName  # Adds or modifies the ACL for the specified file, giving the user "user" read, write, and execute permissions.
setfacl -m u:priya:rw <file>        # Assiging the a new user 'priya' with read/write permission on the file. -m (modifying) -u (user)
setfacl -d -m u:priya:rw <dir>      # Setting ACL for directory
getfacl -R <dir> > permissions.acl  # BackUp ACL's in file having all info related ownership/dir inside the dir,subdir,files
setfacl --restore=permissions.acl   # Restore the Permissions/Ownership
ls -laR >						         # Lists all files recursively in a directory, including hidden files, and saves the output to standard output.
```
--------------------------------------------------------------------------------------------------

</p>
</details>

<details><summary>Symbolic Links</summary><p>

## Symbolic Links

```bash
ln -s|--symbolic S.Directory D.Directory              # Create a link 'D.Directory ' to the 'S.Directory' folder
ln -s|--symbolic -f|--force S.Directory D.Directory   # Overwrite an existing symbolic link 'D.Directory '
ls -l                                                 # Show where symbolic links are pointing
```

--------------------------------------------------------------------------------------------------

</p>
</details>
<details><summary>Identifying Processes</summary><p>

## Identifying Processes

```bash
top                    # List all processes interactively
htop                   # List all processes interactively
ps 
ps aux | grep 
ps all                 # List all processes
pg
pidof PName              # Return the PID of all PName processes

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
nice -n -20 PName      # Change process priority by name
renice 20 PID          # Change process priority by PID
ps -o ni PID           # Return the process priority of PID
```

## Killing Processes

```bash
CTRL+C                 # Kill a process running in the foreground
kill PID               # Shut down process by PID gracefully. Sends TERM signal.
kill -9 PID            # Force shut down of process by PID. Sends SIGKILL signal.
pkill PName            # Shut down process by name gracefully. Sends TERM signal.
pkill -9 PName         # force shut down process by name. Sends SIGKILL signal.
killall PName          # Kill all process with the specified name gracefully.
```

--------------------------------------------------------------------------------------------------
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

* * * * * PName            # Run PName every minute
*/15 * * * * PName         # Run PName every 15 minutes
0 * * * * PName            # Run PName every hour
15 6 * * * PName           # Run PName daily at 6:15 AM
44 4 * * 5 PName           # Run PName every Friday at 4:44 AM
0 0 1 * * PName            # Run PName at midnight on the first of the month
0 0 1 1 * PName            # Run PName at midnight on the first of the year

at -l                      # List scheduled tasks
at -c 1                    # Show task with ID 1
at -r 1                    # Remove task with ID 1
at now + 2 minutes         # Create a task in Vim to execute in 2 minutes
at 12:34 PM next month     # Create a task in Vim to execute at 12:34 PM next month
at tomorrow                # Create a task in Vim to execute tomorrow
```

--------------------------------------------------------------------------------------------------

</p>
</details>
  
<details><summary>SystemD and Services</summary><p>
  
## SystemD and Services
```bash
systemctl 						                # Controls the systemd system and service manager.
systemctl -t help 					          # Displays help information about systemd unit types.
systemctl list-units -t service 			    # Lists all active systemd services on the system.
systemctl --faild -type-service 			    # Lists all failed systemd services of type "service".
systemctl start ___ 					          # Starts a systemd service with the specified name.
systemctl is-active ___ 				       # Checks if a systemd service with the specified name is currently active.
systemctl stop ___ 					          # Stops a systemd service with the specified name.
systemctl enable ___ 					       # Enables a systemd service with the specified name to start automatically at boot time.
systemctl restart ___ 				          # Restarts a systemd service with the specified name.
systemctl reload ____ 					       # Reloads the configuration of a systemd service with the specified name.
systemctl reload-or-restart ___ 			    # Reloads the configuration of a systemd service with the specified name, or restarts it if the reload fails.
systemctl list-dependencies ___ 			    # Lists the dependencies of a systemd unit with the specified name.
systemctl list-dependencies --reverse ___  # Lists the reverse dependencies of a systemd unit with the specified name.
systemctl status sshd.service				    # Displays the status of the "sshd" systemd service.
```

--------------------------------------------------------------------------------------------------

</p>
</details>
  
<details><summary>System Logging and Journaling</summary><p>
  
## System Logging and Journaling
```bash
system Logging /var/log/ 	   # Directory containing system logs.
Journal entries 					# Log entries generated by the systemd journal.
```

--------------------------------------------------------------------------------------------------

</p>
</details>
  
<details><summary>Networking</summary>
<p>
  
## Networking
```bash
nmcli 							                        # Command-line tool for managing NetworkManager.
nmtui 							                        # Text-based user interface for managing NetworkManager.
ip addr 						                           # Displays network interface configuration information.
ip config 						                        # Displays IP configuration information.
ip route 						                        # Displays the system's routing table.
tracepath 						                        # Traces the path that a packet takes from the host system to a remote system.
ping 							                           # Sends ICMP echo request packets to a remote system to test connectivity.
hostname 						                        # Displays or sets the system's hostname.
hostnamectl						                        # Command-line tool for managing the system's hostname.
hostnamectl status 					                  # Displays the current hostname and related information.
cat /etc/sysconfig/network-scripts//ifcfg-enp0s3 	# Displays the configuration file for the "enp0s3" network interface.
cat /etc/hosts 						                  # Displays the system's hosts file.
cat /etc/resolv.cof					                  # Displays the system's DNS resolver configuration file.
```
## Network Troubleshooting

```bash
ping example.com            # Send multiple ping requests using the ICMP protocol
ping -c 10 -i 5 example.com # Make 10 attempts, 5 seconds apart

ip addr                     # List IP addresses on the system
ip route show               # Show IP addresses to router

netstat -i|--interfaces     # List all network interfaces and in/out usage
netstat -l|--listening      # List all open ports

traceroute example.com      # List all servers the network traffic goes through

mtr -w|--report-wide example.com                                    # Continually list all servers the network traffic goes through
mtr -r|--report -w|--report-wide -c|--report-cycles 100 example.com # Output a report that lists network traffic 100 times

nmap 0.0.0.0                # Scan for the 1000 most common open ports on localhost
nmap 0.0.0.0 -p1-65535      # Scan for open ports on localhost between 1 and 65535
nmap 192.168.4.3            # Scan for the 1000 most common open ports on a remote IP address
nmap -sP 192.168.1.1/24     # Discover all machines on the network by ping'ing them
```
## HTTP Requests

```bash
curl https://example.com                               # Return response body
curl -i|--include https://example.com                  # Include status code and HTTP headers
curl -L|--location https://example.com                 # Follow redirects
curl -o|--remote-name foo.txt https://example.com      # Output to a text file
curl -H|--header "User-Agent: Foo" https://example.com # Add a HTTP header

wget https://example.com/file.txt .                            # Download a file to the current directory
wget -O|--output-document foo.txt https://example.com/file.txt # Output to a file with the specified name
```

## DNS

```bash
host example.com            # Show the IPv4 and IPv6 addresses

dig example.com             # Show complete DNS information

cat /etc/resolv.conf        # resolv.conf lists nameservers
```
--------------------------------------------------------------------------------------------------

</p>
</details>
