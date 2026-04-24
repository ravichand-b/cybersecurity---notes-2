# 🐧 Linux Commands Cheat Sheet
**Author:** Ravichand B  
**Date:** 24 April 2026  
**Purpose:** Quick reference for cybersecurity work  

---

## 📁 FILE & DIRECTORY COMMANDS

| Command | What it does | Example |
|---------|-------------|---------|
| `ls` | List files in folder | `ls` |
| `ls -la` | List all files with permissions | `ls -la` |
| `cd` | Change directory | `cd /home` |
| `pwd` | Show current location | `pwd` |
| `mkdir` | Create new folder | `mkdir myfolder` |
| `rm` | Delete file | `rm file.txt` |
| `rm -rf` | Delete folder completely | `rm -rf folder` |
| `cp` | Copy file | `cp file.txt /dest` |
| `mv` | Move or rename file | `mv old.txt new.txt` |
| `touch` | Create empty file | `touch file.txt` |
| `find` | Find files | `find / -name "*.txt"` |
| `tree` | Show folder structure | `tree /home` |

---

## 👀 FILE VIEWING COMMANDS

| Command | What it does | Example |
|---------|-------------|---------|
| `cat` | Show file contents | `cat file.txt` |
| `less` | Read file page by page | `less file.txt` |
| `head` | Show first 10 lines | `head file.txt` |
| `tail` | Show last 10 lines | `tail file.txt` |
| `tail -f` | Watch file live updates | `tail -f /var/log/syslog` |
| `wc -l` | Count lines in file | `wc -l file.txt` |
| `grep` | Search text in file | `grep "password" file.txt` |
| `grep -r` | Search recursively | `grep -r "admin" /var` |

---

## 🔐 PERMISSIONS & USERS

| Command | What it does | Example |
|---------|-------------|---------|
| `whoami` | Show current username | `whoami` |
| `id` | Show user ID and groups | `id` |
| `sudo -l` | List sudo permissions | `sudo -l` |
| `sudo su` | Switch to root | `sudo su` |
| `chmod +x` | Make file executable | `chmod +x script.sh` |
| `chmod 777` | Full permissions | `chmod 777 file` |
| `chown` | Change file owner | `chown user file` |
| `cat /etc/passwd` | List all users | `cat /etc/passwd` |
| `cat /etc/shadow` | Password hashes (root only) | `cat /etc/shadow` |
| `adduser` | Create new user | `adduser newuser` |
| `passwd` | Change password | `passwd username` |

---

## 🌐 NETWORKING COMMANDS

| Command | What it does | Example |
|---------|-------------|---------|
| `ifconfig` | Show network interfaces | `ifconfig` |
| `ip a` | Show IP addresses | `ip a` |
| `ping` | Test connection | `ping 8.8.8.8` |
| `netstat -tulnp` | Show open ports | `netstat -tulnp` |
| `ss -tulnp` | Modern netstat | `ss -tulnp` |
| `ssh` | Connect to remote machine | `ssh user@192.168.1.5` |
| `wget` | Download file | `wget https://url` |
| `curl` | Fetch URL content | `curl https://url` |
| `nc` | Netcat — connect/listen | `nc -lvnp 4444` |
| `traceroute` | Show network path | `traceroute google.com` |
| `nslookup` | DNS lookup | `nslookup google.com` |
| `cat /etc/hosts` | View hostname mappings | `cat /etc/hosts` |

---

## ⚙️ PROCESS & SYSTEM COMMANDS

| Command | What it does | Example |
|---------|-------------|---------|
| `ps aux` | Show all processes | `ps aux` |
| `top` | Live process monitor | `top` |
| `htop` | Better process monitor | `htop` |
| `kill -9` | Force kill process | `kill -9 1234` |
| `uname -a` | Show kernel/OS info | `uname -a` |
| `history` | Show command history | `history` |
| `env` | Show environment variables | `env` |
| `df -h` | Show disk usage | `df -h` |
| `free -h` | Show RAM usage | `free -h` |
| `crontab -l` | List scheduled tasks | `crontab -l` |
| `uptime` | Show system uptime | `uptime` |

---

## 🔍 SEARCH & TEXT COMMANDS

| Command | What it does | Example |
|---------|-------------|---------|
| `grep` | Search text | `grep "error" log.txt` |
| `grep -i` | Case insensitive search | `grep -i "ERROR" log.txt` |
| `grep -v` | Exclude matches | `grep -v "info" log.txt` |
| `sort` | Sort output | `sort file.txt` |
| `uniq` | Remove duplicates | `sort file.txt \| uniq` |
| `cut` | Extract columns | `cut -d: -f1 /etc/passwd` |
| `awk` | Text processing | `awk '{print $1}' file.txt` |
| `sed` | Find and replace | `sed 's/old/new/g' file.txt` |
| `\|` | Pipe — combine commands | `ps aux \| grep apache` |
| `>` | Save output to file | `ls > output.txt` |
| `>>` | Append to file | `echo "text" >> file.txt` |

---

## 🛡️ CYBERSECURITY SPECIFIC

| Command | What it does | Example |
|---------|-------------|---------|
| `find / -perm -4000` | Find SUID files (privesc) | `find / -perm -4000 2>/dev/null` |
| `sudo -l` | Check sudo rights (privesc) | `sudo -l` |
| `cat /etc/crontab` | Check scheduled tasks | `cat /etc/crontab` |
| `ss -tulnp` | Find open ports | `ss -tulnp` |
| `cat /var/log/auth.log` | Check login attempts | `cat /var/log/auth.log` |
| `last` | Show last logins | `last` |
| `who` | Show logged in users | `who` |
| `w` | Show active users | `w` |
| `iptables -L` | Show firewall rules | `iptables -L` |

---

## 💡 USEFUL SHORTCUTS

| Shortcut | What it does |
|----------|-------------|
| `Ctrl + C` | Stop running command |
| `Ctrl + Z` | Pause running command |
| `Ctrl + L` | Clear terminal screen |
| `Tab` | Auto complete command |
| `↑ Arrow` | Previous command |
| `!!` | Repeat last command |
| `clear` | Clear screen |
| `exit` | Exit terminal/session |

---

## 📚 What I Learned
- Linux is the backbone of cybersecurity tools
- File permissions control who can read/write/execute
- Networking commands help with reconnaissance
- Process commands help with post-exploitation
- SUID files and sudo rights are key for privilege escalation

---

*Written by: Ravichand B*  
*GitHub: github.com/ravichand-b/cybersecurity-notes*  
*Learning Path: Cybersecurity — 15 Day Challenge*
