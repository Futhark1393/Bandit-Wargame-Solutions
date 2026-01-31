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

