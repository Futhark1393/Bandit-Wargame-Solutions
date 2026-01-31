# Bandit Levels 0 to 10

## Level 0 -> 1
**Goal:** connect to the server and read the `readme` file.
**Commands Used:** `ssh`, `ls`, `cat`

### Solution
1. Connected to the server using SSH.
2. Listed the files to find the readme.
3. Read the content of the file.

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
# Password: bandit0
ls
cat readme
```

Password for Level 1: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

---

## Level 1 -> 2
**Goal:** Read the file named `-` located in the home directory.
**Commands Used:** `cat`

### Solution
The file is named `-`, which is a special character for STDIN. To read it as a file, we need to specify the path using `./-`.

```bash
ls
# Output: -
cat ./-
```

Password for Level 2: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

---

## Level 2 -> 3
**Goal:** Read a file named `spaces in this filename` located in the home directory.
**Commands Used:** `cat`

### Solution
The filename contains spaces, so the terminal interprets it as multiple arguments. To read it as a single file, we need to wrap the name in quotes or escape the spaces.

```bash
ls
# Output: spaces in this filename
```

# Method 1: Using quotes
```bash
cat "spaces in this filename"
```

# Method 2: Using Tab completion (escapes spaces automatically)
```bash
cat spaces\ in\ this\ filename
```

Password for Level 3: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

---

## Level 3 -> 4
**Goal:** The password for the next level is stored in a hidden file in the inhere directory.
**Commands Used:** `ls -la` `cd` `nano`

### Solution 
The password file is located inside the `inhere` directory but is hidden. In Linux, files starting with a dot (`.`) are hidden. We use the `-a` or `-la` to see them.

```bash
ls
# Output: inhere

cd inhere
ls
# Output: (empty)

ls -la
# Output: ...Hiding-From-You

nano ...Hiding-From-You
```
Password for Level 4: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

---

## Level 4 -> 5
**Goal:**  Fİnd the only human-readable file in the `inhere` directory.
**Commands Used:** `ls`, `cd`, `file`, `nano`

### Solution

The directory contains many files named with a leading dash (`-`). Using `nano` on binary files produces garbage output. The `file` command reveals the data type of each file. We are looking for ""ASCII text".

```bash
cd inhere
file./x
# Result: ./-file07: ASCII text

# Since the filename starts with a dash, we use ./ prefix
nano ./-file07
```

Password for Level 5: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

---

## Level 5 -> 6
**Goal:** Find a file in the `inhere` directory that matches three specific properties:
1. Human-readable
2. 1033 bytes in size
3. Not executable

**Comands Used:** `ls`, `cd`, `find`, `nano`

### Solution
The `inhere` directory contains many subdirectories. Checking them manually is inefficient. I used the `find` command with specific flags to filter for the file matching the criteria.

* `-type f`: Look for files only.
* `-size 1033c`: Filters for files exactly 1033 bytes in size.
* `-not -executable`: Excludes executable files.
* `|| grep ASCII`: Filters for files which is Human-readable.

```bash
ls
cd inhere/
man find
find . -type f -size 1033c -not -executable || grep ASCII
# Output: ./maybehere07/.file2

nano ./maybehere07/.file2
```

Password for Level 6: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

---

---

## Level 6 -> 7
**Goal:** Find a file stored somewhere on the server that matches 3 properties:
1. Owned by user `bandit7`
2. Owned by group `bandit6`
3. 33 bytes in size

**Commands Used:** `find`, `grep`, `cat`

### Solution
Since we need to search the entire system, we start searching from root (`/`). Running `find` on the whole system causes many "Permission denied" errors. We redirect these errors to `/dev/null` to see a clean output.

* `-user bandit7`: Filters by owner.
* `-group bandit6`: Filters by group.
* `-size 33c`: Filters by size.
* `2>/dev/null`: Hides error messages (Standard Error).

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
# Output: /var/lib/dpkg/info/bandit7.password: ASCII text

cat /var/lib/dpkg/info/bandit7.password
```

Password for Level 7: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

---

## Level 7 -> 8
**Goal:** The password is stored in the file `data.txt` next to the word "millionth".
**Commands Used:** `ls`, `grep`

### Solution
The file contains thousands of lines. Reading it manually is impossible. I used `grep` to search for the specific keyword "millionth" within the file.

```bash
ls
# Output: data.txt

grep "millionth" data.txt
# Output: millionth     dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

Password for Level 8: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

---

---

## Level 8 -> 9
**Goal:** The password is the only line of text that occurs only once in `data.txt`.
**Commands Used:** `sort`, `uniq`

### Solution
The file contains many repeating lines. The `uniq` command can filter out duplicates, but it only works if the duplicate lines are adjacent (next to each other). Therefore, we must first sort the file using `sort` and then pipe (`|`) the output to `uniq -u`.

* `sort data.txt`: Sorts all lines alphabetically.
* `uniq -u`: Filters and shows only unique lines.

```bash
sort data.txt | uniq -u
# Output: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

Password for Level 9: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

---

---

## Level 9 -> 10
**Goal:** The password is a human-readable string in `data.txt`, preceded by several `=` characters.
**Commands Used:** `strings`, `grep`

### Solution
The file `data.txt` is a binary file containing mostly unreadable characters. Using `cat` directly would mess up the terminal. The `strings` command extracts all printable character sequences from a binary file. I piped the output to `grep` to look for the `=` markers.

```bash
strings data.txt | grep "=="
# Output: ========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

Password for Level 10: FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

---

## Level 10 -> 11
**Goal:** The password is stored in `data.txt`, which contains base64 encoded data.
**Commands Used:** `base64`, `cat`

### Solution
The content of the file `data.txt` is encoded using Base64. I used the `base64` command with the `-d` (decode) flag to reverse the encoding and reveal the password.

```bash
ls
# Output: data.txt

base64 -d data.txt
# Output: The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```
Password for Level 11: dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
