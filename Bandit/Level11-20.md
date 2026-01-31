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

---

## Level 13 -> 14
**Goal:** The password for the next level is stored in `/etc/bandit_pass/bandit14` and can only be read by user `bandit14`. We are provided with an SSH private key (`sshkey.private`) to log in.

**Commands Used:** `ssh`, `cat`, `chmod`, `cp`

### Solution
We found an SSH private key named `sshkey.private`.
1. Since the private key requires strict permissions (read-only by owner), I copied it to a temporary directory in `/tmp` and set permissions to `600`.
2. Connecting to `localhost` with a key can sometimes cause host verification errors. I used specific SSH flags to force the connection using the key and bypass the host check.

```bash
# 1. Prepare the key
mkdir /tmp/kemal13
cp sshkey.private /tmp/kemal13/mysshkey
chmod 600 /tmp/kemal13/mysshkey

# 2. Connect to bandit14
# -i: Identity file
# -o StrictHostKeyChecking=no: Ignore host key verification
# -o IdentitiesOnly=yes: Force using only the provided key
ssh -i /tmp/kemal13/mysshkey -o StrictHostKeyChecking=no -o IdentitiesOnly=yes bandit14@127.0.0.1 -p 2220

# 3. Retrieve the password (once logged in)
cat /etc/bandit_pass/bandit14
# Output: MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```
Password for Level 14: MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS

---

---

## Level 14 -> 15
**Goal:** Submit the password of the current level to port 30000 on localhost to retrieve the password for the next level.
**Commands Used:** `nc`

### Solution
The `nc` (Netcat) command is used to read from and write to network connections using TCP or UDP. I connected to localhost on port 30000 and sent the current password.

```bash
nc localhost 30000
# Input: MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
# Output:
# Correct!
# 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

Password for Level 15: 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

---

---

## Level 15 -> 16
**Goal:** Submit the password of the current level to port 30001 on localhost using SSL encryption.
**Commands Used:** `openssl`

### Solution
Port 30001 expects an SSL/TLS encrypted connection, so standard `netcat` won't work. I used `openssl s_client` to establish a secure connection.

```bash
# Connect using SSL
openssl s_client -connect localhost:30001

# (Once connected, paste the current password)
# Input: 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
# Output:
# Correct!
# kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

Password for Level 16: kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

---


