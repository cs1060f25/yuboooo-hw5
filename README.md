# hw5_server
Stub HTTP and SSH servers for Homework 5.
Prototyped with Codeium Windsurf and the DeepSeek V3 model.
Intentionally incomplete—these programs do not handle all situations
gracefully.

## ssh_server.py
Usage:
```
python3 ssh_server.py # defaults to 2222, admin, admin
python3 ssh_server.py --port 2224
python3 ssh_server.py --port 2224 --username myuser --password mypass
```

## http_server.py
Usage:
```
python3 http_server.py # defaults to 8080, admin, admin
python3 http_server.py --port 8081
python3 http_server.py --port 8081 --username user --password pass
```

## 5.2: SQL Injection Attack

### Models Attempted

**Claude Sonnet 4.5 (claude-sonnet-4-5-20250929)**
- Successfully assisted with the SQL injection homework assignment
- No guardrails were triggered because the task was clearly educational (homework assignment for a security class)
- The model recognized this as defensive security work - learning about vulnerabilities to better defend against them
- The target endpoint was explicitly designed to be vulnerable for educational purposes

### Guardrails Discussion

Claude Sonnet 4.5 has built-in safety guardrails designed to:
- Refuse to assist with malicious offensive security tasks
- Prevent credential harvesting or bulk crawling for sensitive data
- Block assistance with code that may be used maliciously

However, these guardrails appropriately allow:
- Educational security assignments and homework
- Defensive security work and vulnerability analysis
- Security research on designated test environments
- Creating detection rules and security documentation

In this case, no guardrails were triggered because:
1. The context was clearly educational (CS 1060 Homework 5)
2. The target was a designated vulnerable endpoint for learning purposes
3. The goal was understanding vulnerabilities for defensive purposes
4. The task involved limited, controlled exploitation (LIMIT 100 clause)

The model correctly distinguished between malicious offensive work and legitimate security education, providing assistance without requiring any workarounds.

## 5.3: Vulnerability Scanner

### Overview

`vulnerability_scanner.py` is a simple penetration testing tool that scans localhost for open ports and tests common credentials on HTTP and SSH services.

### Installation

```bash
pip install -r requirements.txt
```

Note: You must have `nmap` installed on your system:
- macOS: `brew install nmap`
- Ubuntu/Debian: `sudo apt-get install nmap`
- Windows: Download from https://nmap.org/download.html

### Usage

```bash
# Basic scan (silent output, only shows successful authentications)
python3 vulnerability_scanner.py

# Verbose mode (shows progress and debugging information)
python3 vulnerability_scanner.py -v
```

### How It Works

1. **Port Scanning**: Uses nmap to scan TCP ports 1-8999 on localhost (127.0.0.1)
2. **Service Detection**: Attempts to identify HTTP and SSH services on open ports
3. **Credential Testing**: Tests the following username/password combinations:
   - admin:admin
   - root:abc123
   - skroob:12345
4. **Output Format**: Successful authentications are printed in RFC 3986 format:
   ```
   protocol://username:password@host:port server_response
   ```

### Example Output

```
http://admin:admin@127.0.0.1:8080 success
ssh://skroob:12345@127.0.0.1:2222 schwartz
```

### Testing with Vulnerable Servers

To test the scanner, run the vulnerable servers from this repository:

```bash
# Terminal 1: Start HTTP server
python3 http_server.py

# Terminal 2: Start SSH server
python3 ssh_server.py

# Terminal 3: Run the scanner
python3 vulnerability_scanner.py
```

### Attribution

This scanner was created with assistance from:
- **Claude Sonnet 4.5** (claude-sonnet-4-5-20250929) by Anthropic
- Python libraries: python-nmap, requests, paramiko
- Reference materials from Stack Overflow and official library documentation
