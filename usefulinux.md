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


