| Command | Description | Example Command | Usage |
|---------|-------------|-----------------|-------|
| `ls` | List directory contents | `ls` | List files and directories in current directory |
| | | `ls -l` | List files in long format |
| | | `ls -a` | List all files including hidden ones |
| | | `ls -lh` | List files in long format with human-readable sizes |
| `cd` | Change directory | `cd /path/to/directory` | Change to specified directory |
| | | `cd ..` | Change to parent directory |
| | | `cd ~` | Change to home directory |
| `pwd` | Print working directory | `pwd` | Display current directory path |
| `mkdir` | Make directories | `mkdir directory_name` | Create a new directory |
| | | `mkdir -p path/to/directory` | Create nested directories |
| `rm` | Remove files or directories | `rm file.txt` | Delete a file |
| | | `rm -r directory/` | Delete a directory and its contents recursively |
| `cp` | Copy files or directories | `cp file.txt newfile.txt` | Copy file to new location with new name |
| | | `cp -r directory/ newdirectory/` | Copy directory and its contents recursively |
| `mv` | Move or rename files or directories | `mv file.txt newlocation/file.txt` | Move file to new location |
| | | `mv oldname.txt newname.txt` | Rename file |
| `touch` | Create empty file | `touch file.txt` | Create a new empty file |
| `cat` | Concatenate and display files | `cat file.txt` | Display contents of file |
| | | `cat file1.txt file2.txt` | Concatenate and display contents of multiple files |
| `grep` | Search file(s) for lines matching a pattern | `grep pattern file.txt` | Search for pattern in file |
| | | `grep -r pattern directory/` | Recursively search for pattern in directory |
| `head` | Output the first part of files | `head file.txt` | Display first 10 lines of file |
| | | `head -n 20 file.txt` | Display first 20 lines of file |
| `tail` | Output the last part of files | `tail file.txt` | Display last 10 lines of file |
| | | `tail -n 15 file.txt` | Display last 15 lines of file |
| `chmod` | Change file mode bits (permissions) | `chmod 644 file.txt` | Change file permissions to rw-r--r-- |
| | | `chmod +x script.sh` | Add execute permission to a script |
| `chown` | Change file owner and group | `chown user:group file.txt` | Change owner and group of file |
| `df` | Report file system disk space usage | `df -h` | Display disk space usage in human-readable format |
| | | `df -i` | Display inode information |
| `du` | Estimate file space usage | `du -sh directory/` | Display total disk usage of directory |
| | | `du -ah` | Display disk usage of all files and directories |
| `tar` | Archive files | `tar -cvf archive.tar file1.txt file2.txt` | Create a tar archive from files |
| | | `tar -xvf archive.tar` | Extract files from tar archive |
| | | `tar -zcvf archive.tar.gz directory/` | Create a gzipped tar archive of a directory |
| | | `tar -xzvf archive.tar.gz` | Extract gzipped tar archive |
| `find` | Search for files in a directory hierarchy | `find . -name "*.txt"` | Find all .txt files in current directory and subdirectories |
| | | `find /home/user -type f -size +10M` | Find files larger than 10MB in /home/user |
| `wget` | Non-interactive network downloader | `wget https://example.com/file.zip` | Download file from URL |
| | | `wget -r -np http://example.com` | Recursively download all files from a website |
| `curl` | Transfer data from or to a server | `curl -O https://example.com/file.zip` | Download file from URL |
| | | `curl -u username:password -T file.txt ftp://ftp.example.com` | Upload file via FTP with authentication |
| `scp` | Secure copy (remote file copy program) | `scp file.txt user@remotehost:/remote/directory/` | Copy file to remote host |
| | | `scp -r directory/ user@remotehost:/remote/directory/` | Copy directory recursively to remote host |
| `rsync` | Remote file and directory synchronization | `rsync -avz /local/directory/ user@remotehost:/remote/directory/` | Sync local directory to remote directory |
| | | `rsync -avz --delete /local/directory/ user@remotehost:/remote/directory/` | Sync with deletion of extraneous files |
| `awk` | Pattern scanning and processing language | `awk '{print $1}' file.txt` | Print first column of each line in file |
| | | `awk '/pattern/ {print $2}' file.txt` | Print second column of lines matching pattern |
| `sed` | Stream editor for filtering and transforming text | `sed 's/old/new/' file.txt` | Replace first occurrence of 'old' with 'new' in file |
| | | `sed -i 's/old/new/g' file.txt` | Replace all occurrences of 'old' with 'new' in file (in place) |
| `sort` | Sort lines of text files | `sort file.txt` | Sort lines of file |
| | | `sort -r file.txt` | Reverse sort |
| `uniq` | Report or omit repeated lines | `uniq file.txt` | Print unique lines of file |
| | | `uniq -c file.txt` | Print unique lines with count of occurrences |
| `tee` | Read from standard input and write to standard output and files | `command | tee file.txt` | Redirect command output to file and standard output |
| `xargs` | Build and execute command lines from standard input | `find . -name "*.txt" | xargs rm` | Delete all .txt files found |
| `nohup` | Run a command immune to hangups | `nohup command &` | Run command in background and immune to hangups |
| `watch` | Execute a program periodically, showing output fullscreen | `watch -n 5 command` | Execute command every 5 seconds and show output |


# usage specific commands

### User Management Commands Cheat Sheet

| Command                   | Description                                            | Example Command                                         | Usage                                                     |
|---------------------------|--------------------------------------------------------|----------------------------------------------------------|------------------------------------------------------------|
| **useradd**               | Add a user to the system                               | `sudo useradd username`                                 | Adds a new user 'username' to the system                    |
| **userdel**               | Delete a user from the system                          | `sudo userdel username`                                 | Deletes the user 'username' from the system                 |
| **usermod**               | Modify a user's properties                            | `sudo usermod -aG groupname username`                  | Adds user 'username' to supplementary group 'groupname'     |
| **passwd**                | Change user's password                                 | `passwd username`                                       | Prompts to change the password for 'username'               |
| **su**                    | Switch user (superuser or another user)                | `su - username`                                         | Switches to user 'username'                                |
| **sudo**                  | Execute a command as another user                      | `sudo command`                                          | Executes 'command' with superuser privileges                |
| **chage**                 | Change user password expiry information               | `sudo chage -E 2025-12-31 username`                    | Sets password expiration date for 'username' to December 31, 2025 |
| **groupadd**              | Add a group to the system                              | `sudo groupadd groupname`                               | Adds a new group 'groupname' to the system                  |
| **groupdel**              | Delete a group from the system                         | `sudo groupdel groupname`                               | Deletes the group 'groupname' from the system               |
| **groups**                | Display groups a user is in                            | `groups username`                                       | Lists the groups that 'username' belongs to                 |
| **id**                    | Display user and group IDs                             | `id username`                                           | Shows the user and group IDs for 'username'                 |
| **whoami**                | Display current username                               | `whoami`                                                | Displays the current logged-in username                     |

### Network Commands Cheat Sheet

| Command                   | Description                                            | Example Command                                         | Usage                                                     |
|---------------------------|--------------------------------------------------------|----------------------------------------------------------|------------------------------------------------------------|
| **ifconfig**               | Configure a network interface                       | `ifconfig eth0 192.168.1.5 netmask 255.255.255.0 up`     | Configures interface eth0 with IP address and netmask       |
| **ip**                    | Show/manipulate routing, devices, policy routing      | `ip addr show eth0`                                      | Displays IP addresses assigned to interface eth0            |
| **ping**                  | Send ICMP ECHO_REQUEST to network hosts               | `ping -c 4 google.com`                                   | Sends 4 ICMP packets to google.com and prints results       |
| **traceroute**            | Print the route packets take to network host          | `traceroute google.com`                                  | Traces the route to google.com                              |
| **netstat**               | Print network connections, routing tables, interface statistics | `netstat -tuln`                                      | Displays listening sockets and their states                 |
| **ss**                    | Utility to investigate sockets                        | `ss -tuln`                                               | Displays TCP, UDP, and UNIX sockets and their states         |
| **dig**                   | DNS lookup utility                                     | `dig google.com`                                         | Performs DNS lookup for google.com                          |
| **nslookup**              | Query Internet name servers interactively             | `nslookup google.com`                                    | Queries DNS servers about host information                  |
| **wget**                  | Non-interactive network downloader                   | `wget http://example.com/file.zip`                        | Downloads file.zip from example.com                         |
| **curl**                  | Transfer data from or to a server                    | `curl -O http://example.com/file.zip`                     | Downloads file.zip from example.com                         |
| **scp**                   | Secure copy (remote file copy program)               | `scp file.txt user@host:/remote/directory/`               | Copies file.txt to remote directory on host using SSH        |

### File System Commands Cheat Sheet

| Command                   | Description                                            | Example Command                                         | Usage                                                     |
|---------------------------|--------------------------------------------------------|----------------------------------------------------------|------------------------------------------------------------|
| **ls**                    | List directory contents                               | `ls -l /path/to/directory`                               | Lists files and directories with details in the directory   |
| **cd**                    | Change directory                                      | `cd /path/to/directory`                                  | Changes current directory to /path/to/directory              |
| **pwd**                   | Print name of current/working directory               | `pwd`                                                    | Shows the current working directory                         |
| **mkdir**                 | Make directories                                      | `mkdir newdir`                                           | Creates a new directory 'newdir'                            |
| **rmdir**                 | Remove empty directories                              | `rmdir emptydir`                                         | Deletes the empty directory 'emptydir'                       |
| **cp**                    | Copy files and directories                            | `cp file.txt /path/to/destination/`                      | Copies file.txt to /path/to/destination/                     |
| **mv**                    | Move/rename files and directories                     | `mv file.txt newname.txt`                                | Renames file.txt to newname.txt or moves it to a new location |
| **rm**                    | Remove files or directories                           | `rm file.txt`                                            | Deletes file.txt                                           |
| **chmod**                 | Change file mode bits (permissions)                   | `chmod 644 file.txt`                                     | Sets read/write permissions for owner and read permissions for group and others for file.txt |
| **chown**                 | Change file owner and group                           | `chown username:groupname file.txt`                      | Changes owner to 'username' and group to 'groupname' for file.txt |
| **find**                  | Search for files in a directory hierarchy             | `find /path/to/search -name "*.txt"`                     | Searches for .txt files in /path/to/search directory         |
| **grep**                  | Print lines matching a pattern                        | `grep "pattern" file.txt`                                | Searches for 'pattern' in file.txt                          |
| **tar**                   | Archive files                                         | `tar -cvf archive.tar file1 file2`                       | Creates a tar archive 'archive.tar' with file1 and file2     |

### Process Management Commands Cheat Sheet

| Command                   | Description                                            | Example Command                                         | Usage                                                     |
|---------------------------|--------------------------------------------------------|----------------------------------------------------------|------------------------------------------------------------|
| **ps**                    | Report a snapshot of current processes                | `ps aux | grep processname`                               | Lists all processes with 'processname' in the output          |
| **top**                   | Display Linux tasks                                   | `top`                                                    | Displays dynamic real-time view of running tasks             |
| **htop**                  | Interactive process viewer                            | `htop`                                                   | Interactive process viewer with sorting and tree view        |
| **kill**                  | Send a signal to a process                            | `kill -9 PID`                                            | Terminates the process with PID                              |
| **killall**               | Kill processes by name                                | `killall processname`                                    | Terminates all processes named 'processname'                 |
| **nice**                  | Execute a command with modified scheduling priority   | `nice -n 10 command`                                     | Runs 'command' with a priority of 10 (lower priority)         |
| **renice**                | Alter priority of running processes                   | `renice -n 10 PID`                                       | Changes priority of process with PID to 10                   |
| **bg**                    | Run jobs in the background                            | `bg %1`                                                  | Puts job number 1 in the background                          |
| **fg**                    | Bring job to foreground                               | `fg %1`                                                  | Brings job number 1 to the foreground                        |
| **nohup**                 | Run a command immune to hangups                      | `nohup command &`                                        | Runs 'command' immune to hangups and sends output to nohup.out |


### LVM (Logical Volume Manager) Commands Cheat Sheet

| Command                   | Description                                            | Example Command                                         | Usage                                                     |
|---------------------------|--------------------------------------------------------|----------------------------------------------------------|------------------------------------------------------------|
| **pvcreate**              | Initialize physical volume for use with LVM            | `sudo pvcreate /dev/sdb1`                               | Creates a physical volume on /dev/sdb1                      |
| **pvdisplay**             | Display attributes of physical volume(s)               | `sudo pvdisplay /dev/sdb1`                              | Shows details about the physical volume /dev/sdb1            |
| **pvremove**              | Remove a physical volume from LVM                      | `sudo pvremove /dev/sdb1`                               | Removes physical volume /dev/sdb1 from LVM                   |
| **vgcreate**              | Create a volume group                                 | `sudo vgcreate myvg /dev/sdb1 /dev/sdc1`                | Creates a volume group 'myvg' with /dev/sdb1 and /dev/sdc1   |
| **vgdisplay**             | Display attributes of volume group(s)                  | `sudo vgdisplay myvg`                                    | Shows details about the volume group 'myvg'                  |
| **vgextend**              | Extend a volume group                                 | `sudo vgextend myvg /dev/sdd1`                           | Adds physical volume /dev/sdd1 to volume group 'myvg'         |
| **vgreduce**              | Reduce a volume group                                 | `sudo vgreduce myvg /dev/sdd1`                           | Removes physical volume /dev/sdd1 from volume group 'myvg'    |
| **lvcreate**              | Create a logical volume                               | `sudo lvcreate -L 1G -n mylv myvg`                       | Creates a 1GB logical volume 'mylv' in volume group 'myvg'   |
| **lvdisplay**             | Display attributes of logical volume(s)               | `sudo lvdisplay /dev/myvg/mylv`                          | Shows details about the logical volume '/dev/myvg/mylv'      |
| **lvextend**              | Extend a logical volume                               | `sudo lvextend -L +500M /dev/myvg/mylv`                  | Extends logical volume '/dev/myvg/mylv' by 500MB             |
| **lvreduce**              | Reduce a logical volume                               | `sudo lvreduce -L 500M /dev/myvg/mylv`                   | Reduces logical volume '/dev/myvg/mylv' to 500MB             |
| **lvremove**              | Remove a logical volume                               | `sudo lvremove /dev/myvg/mylv`                           | Removes logical volume '/dev/myvg/mylv'                     |

### `wall` Command Cheat Sheet

| Command                   | Description                                            | Example Command                                         | Usage                                                     |
|---------------------------|--------------------------------------------------------|----------------------------------------------------------|------------------------------------------------------------|
| **wall**                  | Send a message to all logged-in users                 | `echo "Emergency maintenance in 10 minutes!" \| wall`    | Sends the message to all users logged into the system       |
| **wall -n**               | Suppresses the newline character                      | `echo "System will reboot at 1 PM." \| wall -n`          | Sends the message without appending a newline character    |
| **wall -g**               | Send message to all users in a specified group        | `echo "Meeting in conference room A." \| wall -g admins` | Sends the message to all users in the 'admins' group        |
| **wall -h**               | Display help information for the wall command         | `wall -h`                                                | Displays help information for the `wall` command            |

