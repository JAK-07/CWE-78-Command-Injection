# OS Command Injection (CWE-78) Vulnerability Research & Exploit Validation Lab

[![Cybersecurity Lab](https://img.shields.io/badge/Lab-OS%20Command%20Injection-red)](https://github.com/)
[![Target](https://img.shields.io/badge/Target-DVWA-blue)](https://github.com/)
[![PoC](https://img.shields.io/badge/PoC-Python3-green)](https://github.com/)

An educational security research project and penetration testing lab demonstrating the end-to-end lifecycle of **OS Command Injection (CWE-78)**. This repository covers vulnerability identification, source-code analysis, custom Python Proof-of-Concept (PoC) development, execution evidence, log analysis, and remediation.

---

## Table of Contents
- [Overview](#-overview)
- [Lab Environment & Architecture](#-lab-environment--architecture)
- [Vulnerability Details (CWE-78)](#-vulnerability-details-cwe-78)
- [Custom Python Exploit PoC](#-custom-python-exploit-poc)
- [Execution & Evidence](#-execution--evidence)
- [Remediation & Mitigation](#-remediation--mitigation)

---

## Overview
- **Target Application:** Damn Vulnerable Web Application (DVWA)
- **Container / Host:** Docker container (`dvwa.pc`) running Apache 2.4.10 / PHP 5.6.30 on Debian 8 Jessie.
- **Vulnerability Class:** CWE-78: Improper Neutralization of Special Elements used in an OS Command.

---

## Lab Environment & Architecture
This lab was built and executed entirely within an **isolated, authorized local security lab** running on Kali Linux via VirtualBox and Docker.

- **Host OS:** Kali Linux (VirtualBox)
- **Target Container:** `dvwa.pc` (Isolated Docker bridge network)
- **Validation Language:** Python 3 (`urllib`)

---

## Vulnerability Details (CWE-78)
OS Command Injection occurs when an application passes unsafe user-supplied data to a system shell. In DVWA (Low Security Mode), the IP input field accepts raw parameters without sanitization, allowing attackers to chain system commands using operators like `&&`.

---

## Custom Python Exploit PoC
A lightweight, automated Python script (`poc/exploit.py`) was developed to handle session authentication, bypass CSRF tokens, inject the command payload, and parse the output.

```python
import urllib.request, urllib.parse, http.cookiejar, re

base_url = "http://localhost/"
login_url = base_url + "login.php"
exec_url = base_url + "vulnerabilities/exec/"

jar = http.cookiejar.CookieJar()
opener = urllib.request.build_opener(urllib.request.HTTPCookieProcessor(jar))
# Automated session handling, authentication, and command injection...
