# Linux Commands Reference

Essential Linux commands for server management and application deployment.

---

## File & Directory Navigation/Management

### cd - Change Directory

**Syntax:**
```bash
cd [directory]
```

**Usage:**
```bash
cd /var/www          # Navigate to absolute path
cd Documents         # Navigate to relative path
cd ~                 # Go to home directory
cd -                 # Go to previous directory
cd ..                # Go up one level
cd ../..             # Go up two levels
```

---

### ls - List Files

**Syntax:**
```bash
ls [options] [directory]
```

**Usage:**
```bash
ls                   # List files in current directory
ls -l                # Long format (permissions, owner, size, date)
ls -la               # List all files including hidden (.)
ls -lh               # Human-readable sizes (KB, MB, GB)
ls -lt               # Sort by modification time
ls -lS               # Sort by file size
ls -R                # Recursive (show subdirectories)
ls -d */             # List only directories
```

**Understanding `ls -l` output:**
```
-rw-r--r-- 1 user group 4096 Jun 26 10:00 filename.txt
│└┬┘└┬┘└┬┘  │ │    │    │    │          │
│ u  g  o   │ │    │    │    │          └─ Filename
│           │ │    │    │    └─ Date/Time
│           │ │    │    └─ File size
│           │ │    └─ Group
│           │ └─ Owner
│           └─ Links
└─ File type (- file, d directory, l link)
```

---

### pwd - Print Working Directory

**Syntax:**
```bash
pwd
```

**Usage:**
```bash
pwd                  # Displays full path of current directory
# Output: /home/user/projects/myapp
```

---

### mkdir - Make Directory

**Syntax:**
```bash
mkdir [options] directory_name
```

**Usage:**
```bash
mkdir projects                # Create single directory
mkdir -p a/b/c/d              # Create nested directories (parent dirs auto-created)
mkdir -m 755 mydir            # Create with specific permissions
mkdir -v dir1 dir2 dir3       # Create multiple directories (verbose)
```

**Examples:**
```bash
mkdir -p ~/projects/{frontend,backend,docs}   # Create multiple subdirs at once
mkdir -p /var/www/html/css/js                  # Full web directory structure
```

---

### touch - Create File

**Syntax:**
```bash
touch filename
```

**Usage:**
```bash
touch file.txt                # Create empty file
touch file1.txt file2.txt     # Create multiple files
touch -t 202406261200 file    # Set specific timestamp
touch existing_file           # Update timestamp (access & modify time)
```

---

### rm - Remove Files/Directories

**Syntax:**
```bash
rm [options] file/directory
```

**Usage:**
```bash
rm file.txt                   # Delete single file
rm file1.txt file2.txt        # Delete multiple files
rm -i file.txt                # Interactive (ask before delete)
rm -f file.txt                # Force (no confirmation, no errors)
rm -r directory/              # Recursive (delete directory and contents)
rm -rf directory/             # Force recursive (DANGEROUS - no confirmation)
rm *.log                      # Delete all .log files
rm -v file.txt                # Verbose (show what's being deleted)
```

**Safety Tips:**
```bash
# Always use -i or -v when unsure
rm -iv *.tmp                  # Ask for confirmation before each delete

# Use trash-cli instead of rm for safety
sudo apt install trash-cli
trash-put file.txt            # Move to trash instead of permanent delete
```

---

### cp - Copy Files/Directories

**Syntax:**
```bash
cp [options] source destination
```

**Usage:**
```bash
cp file.txt backup.txt                # Copy file
cp file.txt /backup/                  # Copy to directory
cp -r directory/ /backup/             # Copy directory recursively
cp -p file.txt /backup/               # Preserve permissions & timestamps
cp -i source.txt dest.txt             # Interactive (ask before overwrite)
cp -v file.txt /backup/               # Verbose
cp *.txt /backup/                     # Copy multiple files
cp file.txt{,.bak}                    # Shorthand: creates file.txt.bak
```

**Examples:**
```bash
cp -rp /var/www/html /var/www/html.bak.$(date +%F)   # Backup with date
cp --no-preserve=mode file.txt dest.txt               # Don't preserve permissions
```

---

### mv - Move/Rename Files

**Syntax:**
```bash
mv [options] source destination
```

**Usage:**
```bash
# Move
mv file.txt /new/location/            # Move file to directory
mv file1.txt file2.txt /dest/         # Move multiple files

# Rename
mv oldname.txt newname.txt            # Rename file
mv /old/directory /new/directory      # Rename directory

# Options
mv -i file.txt /dest/                 # Interactive (ask before overwrite)
mv -v file.txt /dest/                 # Verbose
mv -n file.txt /dest/                 # No-clobber (don't overwrite)
```

**Examples:**
```bash
mv config.yml{,.bak}                  # Rename config.yml to config.yml.bak
mv *.jpg /home/user/Pictures/         # Move all jpg files
mv -i *.log /var/log/archive/         # Ask before overwriting
```

---

## File Content & Viewing

### cat - Concatenate/Display Files

**Syntax:**
```bash
cat [options] file(s)
```

**Usage:**
```bash
cat file.txt                          # Display entire file
cat file1.txt file2.txt               # Concatenate and display
cat -n file.txt                       # Show line numbers
cat -b file.txt                       # Number non-blank lines
cat -s file.txt                       # Squeeze multiple blank lines
cat > newfile.txt                     # Create file from keyboard input (Ctrl+D to end)
cat file1.txt >> file2.txt            # Append content to another file
```

**Examples:**
```bash
# View config files
cat /etc/nginx/nginx.conf

# Create small files quickly
cat > script.sh << 'EOF'
#!/bin/bash
echo "Hello World"
EOF

# Combine files
cat header.txt body.txt footer.txt > full_document.txt
```

---

### nano - Text Editor

**Syntax:**
```bash
nano filename
```

**Usage:**
```bash
nano file.txt                         # Open file for editing
nano +10 file.txt                     # Open at line 10
nano -T 4 file.txt                    # Set tab size to 4
```

**Keyboard Shortcuts:**
```
Ctrl+O      Save (Write Out)
Ctrl+X      Exit
Ctrl+K      Cut line
Ctrl+U      Uncut (paste)
Ctrl+W      Search
Ctrl+\      Search and Replace
Ctrl+J      Justify (reformat paragraph)
Ctrl+T      Spell check
Ctrl+G      Help
```

---

### vi/vim - Advanced Text Editor

**Syntax:**
```bash
vi filename
vim filename
```

**Modes:**
- **Normal Mode** - Navigation and commands (default)
- **Insert Mode** - Typing text (`i` to enter)
- **Visual Mode** - Selection (`v` to enter)
- **Command Mode** - Save/quit (`:` to enter)

**Essential Commands:**

| Mode | Key | Action |
|------|-----|--------|
| Normal | `i` | Enter insert mode |
| Normal | `a` | Append after cursor |
| Normal | `o` | New line below |
| Normal | `dd` | Delete line |
| Normal | `yy` | Copy line |
| Normal | `p` | Paste |
| Normal | `u` | Undo |
| Normal | `Ctrl+r` | Redo |
| Normal | `gg` | Go to start |
| Normal | `G` | Go to end |
| Normal | `:w` | Save |
| Normal | `:q` | Quit |
| Normal | `:wq` | Save and quit |
| Normal | `:q!` | Quit without saving |
| Normal | `/pattern` | Search forward |
| Normal | `n` | Next search result |
| Normal | `N` | Previous search result |
| Normal | `:%s/old/new/g` | Replace all in file |

**Example Session:**
```bash
vim script.sh
# Press i to enter insert mode
# Type your code
# Press Esc to return to normal mode
# Type :wq to save and quit
```

---

### less - View File Page by Page

**Syntax:**
```bash
less [options] filename
```

**Usage:**
```bash
less file.txt                         # Open file
less +G file.txt                      # Open at end of file
less -N file.txt                      # Show line numbers
```

**Navigation Keys:**
```
Space/Page Down    Next page
b/Page Up          Previous page
↑/↓                Scroll line by line
/                  Search forward (? for backward)
n/N                Next/previous search match
g                  Go to start
G                  Go to end
q                  Quit
h                  Help
```

**Examples:**
```bash
# View large log files
less /var/log/syslog

# Search within file
less huge_file.log
# Then type: /error
# Press n for next match

# Follow log file
less +F /var/log/syslog   # Press Ctrl+C to stop following
```

---

### head - View Beginning of File

**Syntax:**
```bash
head [options] filename
```

**Usage:**
```bash
head file.txt                         # First 10 lines (default)
head -n 20 file.txt                   # First 20 lines
head -c 100 file.txt                  # First 100 bytes
head -n -5 file.txt                   # All except last 5 lines
```

**Examples:**
```bash
# Preview a CSV file
head -n 5 data.csv

# Check file headers
head -n 1 *.csv

# View first 100 lines of log
head -n 100 /var/log/syslog
```

---

### tail - View End of File

**Syntax:**
```bash
tail [options] filename
```

**Usage:**
```bash
tail file.txt                         # Last 10 lines (default)
tail -n 50 file.txt                   # Last 50 lines
tail -n +10 file.txt                  # From line 10 onwards
tail -c 200 file.txt                  # Last 200 bytes
tail -f file.txt                      # Follow (watch for new lines)
tail -f --pid=1234 file.txt           # Follow until PID 1234 exits
```

**Examples:**
```bash
# Monitor log file in real-time
tail -f /var/log/nginx/access.log

# Watch multiple files
tail -f /var/log/syslog /var/log/auth.log

# Follow with timestamps
tail -f -n 0 --pid=$! logfile.txt    # Stop when script ends

# Monitor application logs
tail -f /var/log/myapp/*.log
```

---

### grep - Search Text Patterns

**Syntax:**
```bash
grep [options] pattern [file(s)]
```

**Usage:**
```bash
grep "error" logfile.txt              # Search for pattern
grep -i "error" logfile.txt           # Case-insensitive
grep -r "TODO" src/                   # Recursive search in directory
grep -n "pattern" file.txt            # Show line numbers
grep -c "error" logfile.txt           # Count matches
grep -v "debug" logfile.txt           # Invert match (exclude pattern)
grep -l "pattern" *.txt               # Show filenames with matches
grep -A 3 "error" logfile.txt         # 3 lines after match
grep -B 2 "error" logfile.txt         # 2 lines before match
grep -C 2 "error" logfile.txt         # 2 lines before and after
grep -w "fail" logfile.txt            # Whole word only
grep -E "error|warning" logfile.txt   # Extended regex (OR)
grep -P "\d{3}" file.txt              # Perl regex
```

**Examples:**
```bash
# Find errors in logs
grep -i "error\|fail" /var/log/syslog

# Search code recursively
grep -rn "function" --include="*.js" src/

# Find which files contain a string
grep -rl "password" /etc/

# Exclude directories
grep -r "pattern" --exclude-dir={node_modules,.git} .

# Pipe with other commands
cat logfile.txt | grep "ERROR" | wc -l

# Count errors per hour
grep "2024-06-26 1[0-5]" logfile.txt | grep -c "error"
```

**Regex Basics:**
```
.        Any character
*        Zero or more of preceding
^        Start of line
$        End of line
[abc]    Character set
[^abc]   Negated set
\d       Digit [0-9]
\w       Word character [a-zA-Z0-9]
\s       Whitespace
{n}      Exactly n occurrences
{n,m}    n to m occurrences
```

---

### man - Manual Pages

**Syntax:**
```bash
man [options] command
```

**Usage:**
```bash
man ls                             # View manual for ls
man -k keyword                     # Search manuals by keyword (apropos)
man -f command                     # Quick description (whatis)
man 5 passwd                       # Section 5 (file formats)
```

**Manual Sections:**
```
1    User commands
2    System calls
3    Library functions
4    Special files
5    File formats
6    Games
7    Miscellaneous
8    System admin commands
```

**Navigation:**
```
Space/Page Down    Next page
b/Page Up          Previous page
/                  Search
n/N                Next/previous match
q                  Quit
```

---

## Permissions & Processes

### chmod - Change File Permissions

**Syntax:**
```bash
chmod [options] mode file(s)
```

**Permission Types:**
```
r (read)    = 4
w (write)   = 2
x (execute) = 1
```

**Permission Classes:**
```
u (user/owner)
g (group)
o (others)
a (all = u+g+o)
```

**Symbolic Mode:**
```bash
chmod u+x script.sh               # Add execute for owner
chmod g-w file.txt                 # Remove write for group
chmod o=r file.txt                 # Set others to read-only
chmod a+x script.sh                # Add execute for all
chmod u=rwx,g=rx,o= script.sh     # Set specific permissions
chmod +x script.sh                 # Add execute for all (shorthand)
```

**Octal (Numeric) Mode:**
```bash
chmod 755 script.sh               # rwxr-xr-x (owner: full, others: read+execute)
chmod 644 file.txt                # rw-r--r-- (owner: read+write, others: read)
chmod 600 secret.key              # rw------- (owner only)
chmod 700 ~/scripts               # rwx------ (owner only, full access)
chmod 4755 binary                 # SUID + rwxr-xr-x
chmod 2750 shared_dir             # SGID
chmod 1777 /tmp                   # Sticky bit
```

**Recursive:**
```bash
chmod -R 755 /var/www/html        # Change all files/dirs recursively
find . -type f -exec chmod 644 {} \;     # All files to 644
find . -type d -exec chmod 755 {} \;     # All dirs to 755
```

**Quick Reference Table:**

| Octal | Binary | Permission | Description |
|-------|--------|------------|-------------|
| 0 | 000 | --- | No access |
| 1 | 001 | --x | Execute only |
| 2 | 010 | -w- | Write only |
| 3 | 011 | -wx | Write + execute |
| 4 | 100 | r-- | Read only |
| 5 | 101 | r-x | Read + execute |
| 6 | 110 | rw- | Read + write |
| 7 | 111 | rwx | Full access |

---

### ps aux - List Running Processes

**Syntax:**
```bash
ps [options]
```

**Usage:**
```bash
ps aux                              # All processes (BSD style)
ps -ef                              # All processes (Unix style)
ps aux --sort=-%cpu | head          # Top CPU consumers
ps aux --sort=-%mem | head          # Top memory consumers
ps -p 1234 -o pid,ppid,cmd,%mem,%cpu  # Specific process details
ps -u www-data                      # Processes by user
ps -C nginx                         # By command name
ps -eo pid,user,pcpu,pmem,comm --sort=-pcpu | head
ps -Lf                              # Show threads
ps -ef --forest                     # Process tree
```

**Understanding Output:**
```
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1 168892  9600 ?        Ss   Jun20   0:05 /sbin/init
│            │   │    │     │     │    │        │    │       │    │
│            │   │    │     │     │    │        │    │       │    └─ Command
│            │   │    │     │     │    │        │    │       └─ CPU time
│            │   │    │     │     │    │        │    └─ Start time
│            │   │    │     │     │    │        └─ Status
│            │   │    │     │     │    └─ Terminal
│            │   │    │     │     └─ RSS (physical memory)
│            │   │    │     └─ VSZ (virtual memory)
│            │   │    └─ Memory %
│            │   └─ CPU %
│            └─ Process ID
└─ User
```

**Process States:**
```
R    Running or runnable
S    Sleeping (interruptible)
D    Uninterruptible sleep (I/O)
T    Stopped
Z    Zombie (terminated, not reaped)
<    High priority
N    Low priority
L    Locked pages in memory
s    Session leader
```

---

### top/htop - Monitor System Performance

**top Syntax:**
```bash
top [options]
```

**Usage:**
```bash
top                                 # Interactive monitor
top -u www-data                    # Filter by user
top -p 1234,5678                   # Monitor specific PIDs
top -bn1                           # One-shot batch (for scripts)
```

**Interactive Commands (inside top):**
```
1              Show all CPU cores
M              Sort by memory
P              Sort by CPU
k              Kill a process (enter PID)
r              Renice a process
c              Show full command
H              Show threads
q              Quit
```

**htop Syntax:**
```bash
htop [options]
```

**Usage:**
```bash
htop                                # Enhanced interactive monitor
htop -u www-data                   # Filter by user
htop -p 1234                       # Monitor specific PID
```

**htop Features:**
- Mouse support
- Tree view (F5)
- Search/Filter (F4)
- Kill process (F9)
- Sort by CPU/Memory
- Color-coded CPU bars
- Vertical/Horizontal scroll

**Understanding Output:**
```
PID USER      PRI  NI  VIRT   RES   SHR S CPU% MEM%   TIME+  Command
1234 www-data  20   0  512M   45M   12M S  5.2  2.3  1:23.45 nginx: worker
```

---

### kill - Terminate Process

**Syntax:**
```bash
kill [signal] PID
```

**Signal Types:**
```bash
kill -15 PID                       # SIGTERM (default) - graceful shutdown
kill -9 PID                        # SIGKILL - force kill (last resort)
kill -1 PID                        # SIGHUP - reload config
kill -2 PID                        # SIGINT - interrupt (Ctrl+C)
kill -3 PID                        # SIGQUIT - quit with core dump
kill -18 PID                       # SIGCONT - continue stopped process
kill -19 PID                       # SIGSTOP - stop process
kill -0 PID                        # Check if process exists (no signal)
```

**Examples:**
```bash
# Graceful shutdown
kill 1234

# Force kill (only if graceful fails)
kill -9 1234

# Reload nginx configuration
kill -HUP $(cat /var/run/nginx.pid)

# Kill by name
killall nginx                      # Kill all nginx processes
pkill -f "python app.py"           # Kill by pattern match

# Kill multiple processes
kill 1234 5678 9012

# Kill all processes of a user
pkill -u www-data
```

**When to Use Each:**
- **SIGTERM (15):** Default, allows cleanup, try first
- **SIGKILL (9):** Immediate death, no cleanup, last resort
- **SIGHUP (1):** Reload config without restart (for daemons that support it)

---

## Networking & System Utilities

### echo - Print Text/Variables

**Syntax:**
```bash
echo [options] [string(s)]
```

**Usage:**
```bash
echo "Hello World"                  # Print text
echo $PATH                          # Print environment variable
echo $HOME                          # Print home directory
echo $(date)                        # Print command output
echo -e "Line1\nLine2"              # Enable escape sequences (\n, \t)
echo -n "No newline"                # No trailing newline
echo "text" > file.txt              # Write to file
echo "text" >> file.txt             # Append to file
```

**Examples:**
```bash
# Display system info
echo "Hostname: $(hostname)"
echo "User: $(whoami)"
echo "Date: $(date)"

# Create files
echo "Hello" > greeting.txt

# Append to files
echo "New line" >> logfile.txt

# Print environment
echo "PATH=$PATH"
echo "HOME=$HOME"
echo "USER=$USER"

# Escape sequences
echo -e "Name\tAge\nJohn\t25\nJane\t30"
```

**Escape Sequences:**
```
\n      Newline
\t      Tab
\\      Backslash
\"      Double quote
\$      Dollar sign
\a      Alert (bell)
\b      Backspace
```

---

### curl - Transfer Data

**Syntax:**
```bash
curl [options] URL
```

**Basic Usage:**
```bash
curl https://api.example.com/users               # GET request
curl -X POST https://api.example.com/users        # POST request
curl -I https://example.com                       # Headers only (HEAD)
curl -o file.zip https://example.com/file.zip     # Download with custom name
curl -O https://example.com/file.zip              # Download with original name
```

**Headers & Data:**
```bash
# Set headers
curl -H "Content-Type: application/json" https://api.example.com
curl -H "Authorization: Bearer TOKEN" https://api.example.com

# Send JSON data
curl -X POST -H "Content-Type: application/json" \
  -d '{"name":"John","age":25}' https://api.example.com/users

# Send form data
curl -X POST -d "username=john&password=secret" https://api.example.com/login

# Send file
curl -X POST -F "file=@/path/to/file.pdf" https://api.example.com/upload
```

**Options:**
```bash
curl -L URL                         # Follow redirects
curl -v URL                         # Verbose output
curl -s URL                         # Silent mode
curl -k URL                         # Skip TLS verification (dev only)
curl -u user:pass URL               # Basic authentication
curl --connect-timeout 5 URL        # Connection timeout (seconds)
curl --max-time 30 URL              # Maximum request time
curl -w "%{http_code}\n" URL        # Print status code
curl -x http://proxy:8080 URL       # Use proxy
```

**Examples:**
```bash
# Test API endpoint
curl -s https://api.example.com/health | jq .

# Check HTTP status code
curl -s -o /dev/null -w "%{http_code}" https://example.com

# Download with progress
curl -L -O https://example.com/large-file.zip

# Test with custom user agent
curl -A "Mozilla/5.0" https://example.com

# Check response time
curl -s -o /dev/null -w "Time: %{time_total}s\n" https://example.com
```

---

### wget - Download Files

**Syntax:**
```bash
wget [options] URL
```

**Basic Usage:**
```bash
wget https://example.com/file.tar.gz              # Download file
wget -O custom_name.zip https://example.com/file   # Custom output name
wget -c https://example.com/large-file.zip         # Resume partial download
wget -q https://example.com/file.tar.gz            # Quiet mode
wget -b https://example.com/file.tar.gz            # Background download
```

**Advanced Usage:**
```bash
# Mirror website
wget -r -np -k https://example.com/docs/          # Recursive, no parents, convert links

# Limit bandwidth
wget --limit-rate=200k https://example.com/file

# Retry options
wget --tries=3 --waitretry=5 URL

# Download to specific directory
wget -P /tmp/downloads/ https://example.com/file

# Accept specific file types
wget -r -A "*.pdf" https://example.com/docs/

# Exclude patterns
wget -r --reject="*.mp4,*.zip" https://example.com/
```

**Options:**
```bash
-r              Recursive
-l N            Depth level (default 5)
-np             No parent
-nc             No clobber (don't overwrite)
-N              Timestamping (only newer)
-A patterns     Accept patterns
-R patterns     Reject patterns
--convert-links # Convert links for local viewing
--page-requisites # Download page assets
```

**Examples:**
```bash
# Download Linux kernel
wget https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.9.tar.xz

# Resume interrupted download
wget -c https://example.com/very-large-file.iso

# Download multiple files
wget -i urls.txt                    # URLs from file

# Mirror documentation site
wget --mirror --convert-links --page-requisites https://docs.example.com
```

**curl vs wget:**
| Feature | curl | wget |
|---------|------|------|
| Protocols | HTTP, HTTPS, FTP, SMTP, etc. | HTTP, HTTPS, FTP |
| Output | stdout | File |
| Resume | -C - | -c |
| Recursive | No | Yes (-r) |
| Authentication | More options | Basic |
| Best for | APIs, scripting | Downloads, mirroring |

---

### apt install - Package Management

**Syntax:**
```bash
apt [options] [command] [package(s)]
```

**Basic Commands:**
```bash
sudo apt update                    # Update package list
sudo apt upgrade                   # Upgrade installed packages
sudo apt install package_name      # Install package
sudo apt install package1 package2 # Install multiple packages
sudo apt remove package_name       # Remove package (keep config)
sudo apt purge package_name        # Remove package + config
sudo apt autoremove                # Remove unused dependencies
sudo apt clean                     # Clean downloaded packages
```

**Search & Info:**
```bash
apt search keyword                 # Search packages
apt show package_name              # Package details
apt list --installed              # List installed packages
apt list --upgradable            # List upgradeable packages
dpkg -l | grep package_name      # Check if installed
dpkg -L package_name             # List files in package
dpkg -S /path/to/file            # Find which package owns file
```

**Examples:**
```bash
# Install common tools
sudo apt update
sudo apt install -y nginx git curl wget htop

# Install specific version
sudo apt install nginx=1.18.0-0ubuntu1

# Install .deb file
sudo dpkg -i package.deb
sudo apt install -f              # Fix broken dependencies

# Hold package version
sudo apt-mark hold nginx         # Prevent upgrade
sudo apt-mark unhold nginx       # Allow upgrade again
```

**Options:**
```bash
-y              Automatic yes to prompts
-f              Fix broken dependencies
--no-install-recommends  Skip recommended packages
-d              Download only (don't install)
-s              Simulate (don't actually install)
```

**Other Package Managers:**

| Distro | Command |
|--------|---------|
| Debian/Ubuntu | `apt`, `apt-get`, `dpkg` |
| RHEL/CentOS/Fedora | `dnf`, `yum`, `rpm` |
| Alpine | `apk` |
| Arch | `pacman` |
| openSUSE | `zypper` |

---

### ss - Socket Statistics

**Syntax:**
```bash
ss [options] [filter]
```

**Basic Usage:**
```bash
ss                                # Show all sockets
ss -t                             # TCP sockets only
ss -u                             # UDP sockets only
ss -l                             # Listening sockets
ss -a                             # All sockets
ss -n                             # Don't resolve names
ss -p                             # Show process using socket
```

**Common Combinations:**
```bash
ss -tuln                          # TCP/UDP listening, no DNS
ss -tulpn                         # With process names
ss -tan                           # All TCP connections
ss -s                             # Summary statistics
ss -t state established           # Established TCP connections
ss -t state time-wait            # Time-wait connections
ss dst 192.168.1.100             # Connections to specific destination
ss src :80                        # Connections to port 80
ss -o state established '( dport = :ssh )'  # SSH connections with timers
```

**Filters:**
```bash
# State filters
ss state established
ss state listening
ss state time-wait
ss state close-wait

# Address filters
ss dst 10.0.0.1
ss src 10.0.0.1
ss dport = :80
ss sport = :443

# Combined
ss '( dport = :80 or dport = :443 )'
ss state established dst 10.0.0.1
```

**Output Interpretation:**
```
Netid  State    Recv-Q  Send-Q  Local Address:Port  Peer Address:Port
tcp    ESTAB    0       0       192.168.1.10:22     192.168.1.20:54321
│       │       │       │            │                   │
│       │       │       │            │                   └─ Peer (remote)
│       │       │       │            └─ Local (our) address
│       │       │       └─ Send queue bytes
│       │       └─ Receive queue bytes
│       └─ Connection state
└─ Socket type
```

**Useful One-liners:**
```bash
# Count connections by state
ss -tan | awk 'NR>1 {print $1}' | sort | uniq -c | sort -rn

# Find connections to specific IP
ss -tan dst 10.0.0.5

# Show connections with process info
ss -tulpn

# Monitor connections in real-time
watch -n 1 'ss -s'
```

---

### uptime - System Uptime

**Syntax:**
```bash
uptime [options]
```

**Usage:**
```bash
uptime                              # Show uptime and load average
uptime -p                           # Pretty format (human readable)
uptime -s                           # System boot time
uptime -V                           # Version
```

**Output Explanation:**
```
 10:30:45 up 14 days,  3:22,  2 users,  load average: 0.50, 0.75, 1.00
│         │              │       │              │         │       │
│         │              │       │              │         │       └─ 15 min avg
│         │              │       │              │         └─ 5 min avg
│         │              │       │              └─ 1 min avg
│         │              │       └─ Currently logged in users
│         │              └─ Current time
│         └─ Uptime duration
└─ Current time
```

**Load Average:**
- **1 min, 5 min, 15 min** averages of processes in runnable/uninterruptible state
- **Low** (< number of CPU cores): System not busy
- **Equal to cores**: System fully utilized
- **Higher than cores**: System overloaded

**Examples:**
```bash
# Check if server needs attention
uptime
# If load > CPU cores * 2, investigate

# Pretty output
uptime -p
# Output: up 2 weeks, 3 days, 5 hours

# When did server last reboot?
uptime -s
# Output: 2024-06-12 07:08:22

# Check load in scripts
load=$(uptime | awk -F'load average:' '{print $2}' | cut -d',' -f1)
if (( $(echo "$load > 2.0" | bc -l) )); then
    echo "High load detected: $load"
fi
```

---

## Quick Reference Cheat Sheet

| Task | Command |
|------|---------|
| Navigate to directory | `cd /path/to/dir` |
| List files with details | `ls -la` |
| Show current path | `pwd` |
| Create nested directories | `mkdir -p a/b/c` |
| Create empty file | `touch file.txt` |
| Delete file | `rm file.txt` |
| Delete directory recursively | `rm -rf dir/` |
| Copy file | `cp src dest` |
| Copy directory | `cp -r src dest` |
| Move/rename | `mv old new` |
| View file content | `cat file.txt` |
| View first 20 lines | `head -n 20 file.txt` |
| View last 50 lines | `tail -n 50 file.txt` |
| Follow log file | `tail -f /var/log/syslog` |
| Search in file | `grep "pattern" file` |
| Recursive search | `grep -r "pattern" dir/` |
| Make script executable | `chmod +x script.sh` |
| View all processes | `ps aux` |
| Kill process | `kill -15 PID` |
| Force kill | `kill -9 PID` |
| Monitor system | `top` or `htop` |
| Check disk space | `df -h` |
| Check memory | `free -h` |
| Test connectivity | `ping -c 4 host` |
| Download file | `wget URL` or `curl -O URL` |
| View manual | `man command` |
| Check listening ports | `ss -tulpn` |
| System uptime | `uptime` |
