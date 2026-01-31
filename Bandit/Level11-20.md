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


