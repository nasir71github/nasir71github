
# OverTheWire — Bandit Progress

**Completed Levels:** 1 → 15  
**Current Level:** 16 (in progress)

## Skills Learned
- SSH connections & key authentication
- Linux navigation, file manipulation, and permissions
- Handling compressed & encoded files (`tar`, `gzip`, `bzip2`, `base64`, `xxd`)
- Searching & parsing: `find`, `grep`, `sort`, `uniq`, `strings`
- Networking basics with `nc` and `openssl`

## Highlights
- **Level 12 → 13 (the “nightmare”)**: Iteratively decoded/decoded nested formats using `file`, `mv`, `gunzip`, `bunzip2`, and `tar`. Learned to trust `file` output and extract layer by layer.
- **Level 14 → 15**: Used `openssl`/`nc` to connect to a local SSL service and send the current password to retrieve the next one.

## Proof of Work
- **LinkedIn Post:** *(add your link here)*  
- **Screenshots related to this lab can be found [here](../../assets/images/)**  
  - [Level 12 → 13 — multi-layer extraction](../..//assets/images/overTheWire-Images/level13.png)  
  - [Level 14 → 15 — using `nc` with password](../../assets/images/overTheWire-Images/level14.png)
    
## Useful Commands I Practiced
```bash
# SSH, key perms
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
chmod 600 sshkey.private

# Search & parse
grep "millionth" data.txt
sort data.txt | uniq -u
strings data.txt

# Decoding & extraction
base64 -d data.txt
xxd -r data.txt decoded
file decoded
mv decoded decoded.gz && gunzip decoded.gz
mv decoded decoded.bz2 && bunzip2 decoded.bz2
mv decoded decoded.tar && tar -xf decoded.tar

# Networking
echo "<password>" | nc localhost 30000
