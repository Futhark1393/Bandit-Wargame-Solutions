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
