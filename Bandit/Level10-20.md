# Bandit Levels 10 to 20

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
