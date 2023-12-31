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
bandit12@bandit:~$ mkdir /tmp/random_dir
bandit12@bandit:~$ cd /tmp/random_dir
bandit12@bandit:/tmp/random_dir$
bandit12@bandit:/tmp/random_dir$ cp ~/data.txt .
bandit12@bandit:/tmp/random_dir$ mv data.txt data

*xxd to convert the data into its binary equivalent

bandit12@bandit:/tmp/random_dir$ file binary
binary: gzip compressed data, was "data2.bin", last modified: Thu Oct  5 06:19:20 2023, max compression, from Unix, original size modulo 2^32 573

bandit12@bandit:/tmp/random_dir$ mv binary binary.gz
bandit12@bandit:/tmp/random_dir$ gzip -d binary.gz
bandit12@bandit:/tmp/random_dir$ file binary
binary: bzip2 compressed data, block size = 900k

bandit12@bandit:/tmp/random_dir$ mv binary binary.gz
bandit12@bandit:/tmp/random_dir$ gzip -d binary.gz
bandit12@bandit:/tmp/random_dir$ file binary
binary: bzip2 compressed data, block size = 900k

bandit12@bandit:/tmp/random_dir$ mv binary binary.gz
bandit12@bandit:/tmp/random_dir$ gzip -d binary.gz
bandit12@bandit:/tmp/random_dir$ file binary
binary: POSIX tar archive (GNU)

bandit12@bandit:/tmp/random_dir$ tar -xf binary
bandit12@bandit:/tmp/random_dir$ ls
binary  data  data5.bin
bandit12@bandit:/tmp/random_dir$ file data5.bin
data5.bin: POSIX tar archive (GNU)


```

