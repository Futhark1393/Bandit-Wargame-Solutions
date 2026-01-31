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
ls
cat readme

Password for Level 1: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If


