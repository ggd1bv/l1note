**Read file begin with "-"**
> cat ./-

**Read files with spaces**
> cat "spaces in this filename"

**Change Directories**
> cd .. goes to the parent directory
> cd / goes to the root directory
> cd ~ goes to the home directory (of the current user)

**Show all files (hidden)**
> ls -a 
> ll

**Read hidden file**
> cat .hiddenFile
> cat folder/.hiddenFile

**Install | Uninstall .DEB (ubuntu)**
> sudo dpkg -i DEB_PACKAGE
> sudo dpkg -r PACKAGE_NAME

**ELF Files (not human-readable)**
> �������$��$,0�%��0�'��

**Get the type for all the files**
> file -f inhere/-f*

**Find with multiple options**
- human-readable
- 1033 bytes in size
- not executable

> find . -type f -size 1033c ! -executable -exec file '{}' \; | grep ASCII
> find . -type f -readable -size 1033c ! -executable


**Find with grep and options**
> find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
- type f, because we are looking for a file
- user bandit7, to find files owned by the ‘bandit7’ user
- group bandit6, to find files owned by the ‘bandit6’ group
- size 33c, to find files of size 33 bytes
- 2>/dev/null, to 'hide' error messages (I/O redirection on the find command) 

**Check file size**
> du -b data.txt 
> ll 

**Grep command**
> cat data.txt | grep millionth

**Uniq & Sort commands**
- sort -r, in Reverse
- sort -n, sorting numerically
- uniq , filters input and writes to the output.
- uniq -c, filters for unique lines (lines that appear only ones).
- uniq -c, count
- uniq -d, only return duplicate
> sort data.txt | uniq -u


**String command**
> strings data.txt
> strings data.txt | grep ==

**Base64 command**
- base64 -d, for decoding
> base64 -d data.txt

**ROT13 command**
- base64 -d, for decoding
> tr <old_chars> <new_chars>
> cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'

**ROT13 & ROT5 command**
- base64 -d, for decoding
> alias rot13="tr 'A-Za-z' 'N-ZA-Mn-za-m'"
> alias rot5="tr '0-9' '5-90-4'"

**Hexdumps (volcados hexadecimales) & Compression**
- xxd <input_file> <output_file> creates hexdumps. 
- xxd -r , it reverts the hexdump.
- gzip (-d) | ext .gz
- bzip2 (-d) | ext .bz2
- tar -cf, to create .tar
- tar -xf, to extract .tar
- file data
```
~$ mkdir /tmp/random_dir
~$ cd /tmp/random_dir
/tmp/random_dir$
/tmp/random_dir$ cp ~/data.txt .
/tmp/random_dir$ mv data.txt data

*xxd to convert the data into its binary equivalent

/tmp/random_dir$ file binary
binary: gzip compressed data, was "data2.bin", last modified: Thu Oct  5 06:19:20 2023, max compression, from Unix, original size modulo 2^32 573

/tmp/random_dir$ mv binary binary.gz
/tmp/random_dir$ gzip -d binary.gz
/tmp/random_dir$ file binary
binary: bzip2 compressed data, block size = 900k

/tmp/random_dir$ mv binary binary.gz
/tmp/random_dir$ gzip -d binary.gz
/tmp/random_dir$ file binary
binary: bzip2 compressed data, block size = 900k

/tmp/random_dir$ mv binary binary.gz
/tmp/random_dir$ gzip -d binary.gz
/tmp/random_dir$ file binary
binary: POSIX tar archive (GNU)

/tmp/random_dir$ tar -xf binary
/tmp/random_dir$ ls
binary  data  data5.bin
/tmp/random_dir$ file data5.bin
data5.bin: POSIX tar archive (GNU)


```
**SSH Key**
- The public key is placed on the computers that should allow access (the remote host) to the user that owns the private key. Like with the password, it is important that only the user knows/owns the private key. The -i flag allows login with the private key.

- scp -P <port> <user>@<IP>:<remotefilepath> <localfilepath>

- Alternative scp is starting a simple web server with python. This is useful when you do not have ssh access. 
- On the machine where the file is you need to start the webserver with the following command: python3 -m http.server (best is to do it in the directory of the file). 
- On the receiving machine you then just have to send an HTTP request: wget http://<ip>:8000/<pathtofile>

> scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .
> ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220


**Net**
- Localhost is a hostname and its IP address is ‘127.0.0.1’. It is used to access network services on the same device that is running these services.
- nc or netcat is a command that allows to read and write data over a network connection. It can be used for TCP and UDP connections.
- Connect: nc <host> <port>
- Create a server that listens to incoming packets,  nc -l <port>

- to submit the password to port 30000 on localhost.
> nc localhost 30000
> fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq

**Net2**
- openssl s_client is the implementation of a simple client that connects to a server using SSL/TLS.

> openssl s_client -connect localhost:30001
> jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
> Correct!
> JQttfApK4SeyHwDlI9SXGR50qclOAil1

**Net3**
- Port scanning is a method to find open ports on a host. A port can be seen as an address for a specific service. Every computer has ports with the numbers 0 to 65535. Some services have standard ports, like HTTP/80 or SSH/22.

- nmap, By default, Nmap scans the top 1000 ports
- nmap -p 
- nmap -sV flag lets us do a service/version detection scan.
- nmap -p- -A <host>

> nmap -sV localhost -p 31000-32000
> The promising port seems to be port 31790, which runs an unknown service.
> openssl s_client -connect localhost:31790


**Diff**
- The diff command prints the difference between two files.

> nmap -sV localhost -p 31000-32000
> sort passwords.old passwords.new | uniq -u


**SSH Send commands**
- Desafortunadamente, alguien ha modificado .bashrc para cerrar tu sesión cuando inicias sesión con SSH.
> ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
> ssh bandit18@bandit.labs.overthewire.org -p 2220 /bin/bash
> ssh bandit18@bandit.labs.overthewire.org -p 2220 -t /bin/sh  (-t, pseudoterminal)

**Permission**
- -rw-r--r--. 1 root root  4017 Feb 24  2022 vimrc
- File type: - ( d, for directory )
- Permission settings: rw- (owner) r-- (group) r-- (others)
- Extended attributes: dot (.)
- User owner: root
- Group owner: root

- Octal values: r (read): 4 |  w (write): 2 | x (execute): 1
- Owner: rwx = 4+2+1 = 7 | Group: r-- = 4+0+0 = 4 |  Others: r-- = 4+0+0 = 4
- The results produce the three-digit value 744.

- For users, u stands for user owner, g for group owner, and o for others. For permissions, r stands for read, w for write, and x for execute.

> ls -la

- -rwsr-x---  1 bandit20 bandit19 7296 May  7  2020 bandit20-do
"""
In this case, the owner is badit20 and the group is bandit19, this with ‘-rwsr-x—’ means the user bandit19 can execute the binary, but the binary is executed as user bandit20.

Executing the binary says it simply executes another command as another user (as already explained, this user is bandit20). This means we can access the bandit20 users password file, which can only be read by the user bandit20.
"""
> ./bandit20-do cat /etc/bandit_pass/bandit20



**echo & netcat**
"""
Using ’netcat’, we can create a connection in server mode - which listens for inbound connection. To have netcat send the password, I use echo and pipe it into netcat. The -n flag is to prevent newline characters in the input. Lastly, we let the process run in the background with &.
"""

>  echo -n 'VxCazJaVykI6W36BkBU0mJTCM8rR95XT' | nc -l -p 1234 & [1] 24661

"""
Running the setuid binary with port 1234 means it will connect to our netcat server, receive the password inputted through echo and sends back the next password.
"""
> ./suconnect 1234


**Cron**
"""
cronjobs are programs running automatically at regular intervals. In Linux, there are multiple folders that can contain these cronjobs: cron.d, cron.daily, cron.hourly, cron.monthly, crontab, cron.weekly.

"""
> ls -la /etc/cron.d
> cat /usr/bin/cronjob_bandit22.sh
> cat /usr/bin/cronjob_bandit22.sh
> cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv


 mktemp -d
 cd /tmp/tmp.0iJ50mzmNe

 #!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/tmp.ljEyl6kv1M/password

chmod +rx bandit24_pass.sh
chmod 777 /tmp/tmp.0iJ50mzmNe
touch password
chmod +rwx password 
ls -la

