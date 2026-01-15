# Linux Shell – Fundamentals (TryHackMe)

This document contains a complete and structured overview of the Linux Shell fundamentals covered in the TryHackMe Linux Shell section.  
It serves as a practical reference for daily usage, security labs, and future red team / blue team activities.

---

## Basic Navigation and File System Interaction

Linux is built around a hierarchical file system. Knowing how to move and inspect it is essential.

### pwd
Displays the current working directory.
pwd

###ls
Lists files and directories.

ls
ls -l
ls -la
-l → long format

-a → include hidden files

###cd
Changes the current directory.

cd /etc
cd ..
cd ~
File and Directory Management

###touch
Creates empty files.

touch file.txt

###mkdir
Creates directories.

mkdir test
mkdir -p parent/child

###cp
Copies files or directories.

cp file.txt backup.txt
cp -r dir1 dir2

###mv
Moves or renames files.

mv old.txt new.txt
mv file.txt /tmp/

###rm
Deletes files or directories.

rm file.txt
rm -r folder
rm -rf folder
⚠️ rm -rf is dangerous and irreversible.

###Viewing and Reading Files
cat
Displays file contents.

cat file.txt

###less
Views files page by page.

less file.txt

head / tail
Shows the beginning or end of a file.

head file.txt
tail file.txt
tail -n 20 file.txt

###Searching and Filtering Data
grep
Searches for patterns inside files or command output.

grep "root" /etc/passwd
ls | grep ".txt"
Common flags:

-i → ignore case

-r → recursive search

###Users, Permissions and Ownership
###Linux uses permissions to control access.

ls -l output
text

-rwxr-xr--
Read (r)

Write (w)

Execute (x)

###chmod
Changes permissions.


chmod 755 script.sh
chmod +x script.sh

###chown
Changes file owner.


chown user:user file.txt

###Environment and System Information
whoami
Displays the current user.

whoami
id

###Shows user ID and groups.

id

uname
###Displays system information.

uname -a

df
###Shows disk usage.

df -h

###free
###Displays memory usage.

free -h


###Processes and System Monitoring
ps
Displays running processes.

ps
ps aux

###top
Real-time process monitoring.

top

###kill
Terminates a process.

kill PID
kill -9 PID

###Networking Basics
ip
Displays network information.

ip a
ip route

###ping
Tests network connectivity.

ping google.com

###Redirection and Pipes
Linux allows chaining commands and redirecting output.
Output redirection

echo "test" > file.txt
echo "append" >> file.txt

###Pipes

ls | grep ".log"
cat file.txt | grep "error"
ps aux | grep root
Pipes pass the output of one command as input to another.

###Find and File Discovery
find
Searches for files and directories.

find / -name file.txt
find /home -type f
Very useful for:

Privilege escalation
File enumeration

Log discovery
 History

###history
Displays previously executed commands.

history
Re-run commands

!5
!!

###Shell Scripting Basics script example

#!/bin
echo "Hello World"

###Make it executable:


chmod +x script.sh
./script.sh
Key Takeaways


######Linux is command-line driven

Everything is a file

Permissions are critical for security

Pipes and redirection enable powerful workflows

Linux shell skills are essential for cybersecurity roles

Progress
✔ Linux Shell Fundamentals (TryHackMe)
✔ Cyber Security 101 – Ongoing