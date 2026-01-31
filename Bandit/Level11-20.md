# Bandit Levels 11 to 20

## Level 11 -> 12
**Goal:** The password is stored in `data.txt`, where all letters are rotated by 13 positions (ROT13 cipher).
**Commands Used:** `cat`, `tr`

### Solution
ROT13 is a simple substitution cipher. To decrypt it, we need to shift every character back by 13 places. The `tr` command is used to translate characters. We map `A-Z` to `N-Z` followed by `A-M` (and same for lowercase).

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
# Output: The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

Password for Level 12: 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4

---

---

## Level 12 -> 13
**Goal:** The password is stored in `data.txt`, which is a hexdump of a file that has been repeatedly compressed.
**Commands Used:** `mkdir`, `cp`, `xxd`, `file`, `mv`, `gzip`, `bzip2`, `tar`

### Solution
This level required reversing a hexdump and then decompressing the file multiple times. Since we don't have write permissions in the home directory, I created a temporary workspace in `/tmp`.

The file was compressed like a "Matryoshka doll" using `gzip`, `bzip2`, and `tar` repeatedly. I used the `file` command to identify the compression type at each step, renamed the file with the correct extension, and decompressed it until I reached an ASCII text file.

```bash
# Setup workspace
mkdir /tmp/kemal_cozum
cp data.txt /tmp/kemal_cozum/
cd /tmp/kemal_cozum

# Reverse Hexdump
xxd -r data.txt > data

# Decompression Loop (Summary of steps)
# 1. Identify file type: file <filename>
# 2. Rename with extension: mv <filename> <filename.ext>
# 3. Decompress: gzip -d, bzip2 -d, or tar -xf

# After roughly 8 layers of decompression:
ls
# Output: data8

file data8
# Output: data8: ASCII text

cat data8
# Output: The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

Password for Level 13: FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn

---



