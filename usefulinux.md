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


**Get the type for all the files**
> file ./*  (return all f)