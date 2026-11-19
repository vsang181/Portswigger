# Useful commands

Once you identify an OS command injection vulnerability, it is useful to run a few basic enumeration commands to gather information about the underlying operating system, user privileges, network configuration, and active processes.

## Linux vs. Windows Enumeration Cheat Sheet

| Purpose of Command | Linux | Windows |
|---|--|---|
| Name of current user | `whoami` | `whoami` |
| Operating system & version | `uname -a` | `ver` |
| Network configuration | `ifconfig (or ip a)` | `ipconfig /all` |
| Active network connections | `netstat -an (or ss -tulnp)` | `netstat -an` |
| Running processes | `ps -ef (or ps aux)` | `tasklist` |

Why These Commands Matter During Exploitation

- **`whoami` (Privilege Level)**: Confirms which user account the web application is running as (e.g., `www-data` vs. `root` on Linux, or `IIS APPPOOL\DefaultAppPool` vs. `NT AUTHORITY\SYSTEM` on Windows). This determines what files you can read and what actions you can perform.

- **`uname -a` / `ver` (OS & Kernel Version)**: Identifies the exact operating system distribution, architecture, and kernel/build version useful for spotting outdated systems vulnerable to local privilege escalation.

- **`ifconfig` / `ipconfig /all` (Network Interfaces)**: Reveals internal IP addresses and subnets attached to the server, helping you map out internal networks for pivoting.

- **`netstat -an` (Network Connections & Listening Ports)**: Shows active connections and internal services listening on local ports (such as databases or admin panels bound to `127.0.0.1`).

- **`ps -ef` / `tasklist` (Running Processes)**: Lists active services, background jobs, and security software (such as antivirus or EDR agents) running on the host.
  
