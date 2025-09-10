# OverTheWire — Bandit Wargames

**Completed Levels:** 1 → 34 (all finished 🎉)  

## Skills Learned
- SSH connections & key authentication  
- Linux navigation, file manipulation, and permissions  
- Handling compressed & encoded files (`tar`, `gzip`, `bzip2`, `base64`, `xxd`)  
- Searching & parsing: `find`, `grep`, `sort`, `uniq`, `strings`  
- Networking basics with `nc` and `openssl`  
- Automating with cron jobs and shell scripting  
- Escaping restricted shells via `vim`  
- Git fundamentals: cloning repos, branches, commits, tags, stashes  

## Highlights
- **Level 12 → 13 (the “nightmare”)**: Iteratively decoded nested formats using `file`, `mv`, `gunzip`, `bunzip2`, and `tar`. Learned to trust `file` output and extract layer by layer.  
- **Level 14 → 15**: Used `openssl`/`nc` to connect to a local SSL service and send the current password to retrieve the next one.  
- **Level 23 → 24 (cron job scripting)**: Discovered a cron job running every minute. Created my first shell script that copied the Bandit24 password into `/tmp`. This level was a big milestone — my first real script execution in a capture-the-flag environment.  
- **Level 25 → 26 (restricted shell bypass)**: Faced a tricky login with a custom shell (`/usr/bin/showtext`) that immediately logged me out. By resizing the terminal, I forced `more` into interactive mode, escaped into `vim`, and launched a real `/bin/bash` shell. Huge learning experience on escaping restricted environments.  
- **Level 27 → 32 (Git mastery)**: The remaining levels focused on Git. I practiced:  
  - Cloning repos with SSH keys  
  - Exploring commit history (`git log`)  
  - Checking hidden branches (`git branch -a`)
  - Pushing to a remote repository (`git push origin master`)  
  - Reading commit diffs (`git show`)  
  - Inspecting tags (`git tag`, `git show <tag>`)  
  - Working with stashes (`git stash list`, `git stash show -p`)  
  These challenges gave me strong hands-on Git experience beyond just version control basics.
- **Level 32 → 33 (uppercase shell escape)**: On login, I was placed in a restricted shell that automatically converted all commands to uppercase, making them invalid. By executing `$0`, I spawned a proper `/bin/sh` shell, confirmed I was running as `bandit33`, and retrieved the password. This taught me how environment variables and shell behaviors can be leveraged to escape restrictions.  


## Proof of Work
- **LinkedIn Post:** *(link here)*  
- **Screenshots related to this lab can be found [here](../../assets/images/OverTheWire-Images/)**  
  - [Level 12 → 13 — multi-layer extraction](../../assets/images/OverTheWire-Images/level13.png)  
  - [Level 14 → 15 — using `nc` with password](../../assets/images/OverTheWire-Images/level14.png)  
  - [Level 23 → 24 — cron job shell script](../../assets/images/OverTheWire-Images/level23.png)  
  - [Level 25 → 26 — escaping restricted shell](../../assets/images/OverTheWire-Images/smallscreen.png)  
  - [Level 27 → 31 Git exploration](../../assets/images/OverTheWire-Images/level29.png)
  - [Level 32 → 33 uppercase shell escape](../../assets/images/OverTheWire-Images/level33.png)  


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

# Cron scripting (Bandit 23 → 24)
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/rand/password

# Escaping restricted shell (Bandit 25 → 26)
# Resize terminal -> more interactive -> press 'v' -> vim -> :set shell=/bin/bash -> :shell

# Git exploration (Bandit 27 → 34)
git clone ssh://bandit29-git@localhost/home/bandit29-git/repo
git log
git push origin master
git branch -a
git show <commit/tag>
git stash list
git stash show -p

# Shell path bypass (Bandit 32 → 33)
$0
ls -la
cat /etc/bandit_pass/bandit33
```
## Final Reflection
Finishing the Bandit wargame (Levels 1 → 34) was a huge step in my cybersecurity journey. The progression forced me to:  
- Build confidence in **Linux command-line navigation**  
- Think creatively when faced with **restricted environments**  
- Automate tasks with **scripts and cron jobs**  
- Deepen my understanding of **networking and Git** in real scenarios  

This challenge not only sharpened my technical skills but also taught me persistence and problem-solving — qualities that are just as critical as tools in cybersecurity.  

---


