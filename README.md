# 📧 IMAP & POP3 Enumeration and Exploitation

## 📌 Target Information

- Target IP: `10.129.54.139`
- Environment: HTB Academy Lab
- Scope: Mail Services Enumeration

---

# 🧠 Executive Summary

During the assessment, multiple mail services were identified, including:

- POP3
- IMAP
- IMAPS
- POP3S

Manual interaction with the services revealed:

- internal hostname disclosure
- version disclosure
- accessible internal mailboxes
- sensitive information exposure

The assessment resulted in successful extraction of:

- IMAP banner flag
- mailbox flag
- internal mailbox data

---

# 🔍 Service Enumeration

## Nmap Scan

```bash
sudo nmap 10.129.54.139 -sV -p110,143,993,995 -sC
```

## Key Findings

- Dovecot mail infrastructure identified
- IMAP supports AUTH=PLAIN
- POP3 supports USER authentication
- Internal hostname exposed:
  - `dev.inlanefreight.htb`

See:

```text
nmap/initial_scan.txt
```

---

# 🔐 TLS Certificate Analysis

Certificate metadata exposed:

```text
CN = dev.inlanefreight.htb
emailAddress = cto.dev@dev.inlanefreight.htb
```

---

# 🚨 IMAPS Banner Disclosure

## Connection

```bash
openssl s_client -connect 10.129.54.139:993
```

## Result

Sensitive information was exposed directly in the IMAP banner before authentication.

See:

```text
imap/imaps_banner.txt
```

---

# 📬 POP3S Enumeration

## Connection

```bash
openssl s_client -connect 10.129.54.139:995
```

## Result

```text
+OK InFreight POP3 v9.188
```

See:

```text
pop3/pop3s_banner.txt
```

---

# 🔑 IMAP Authentication

IMAP requires command tags.

Example:

```text
a1 LOGIN robin robin
```

See:

```text
imap/login_notes.md
```

---

# 📂 Mailbox Enumeration

Recursive enumeration revealed nested mailboxes:

```text
DEV
DEV.DEPARTMENT
DEV.DEPARTMENT.INT
```

See:

```text
imap/mailbox_enum.md
```

---

# 🎯 Internal Mailbox Access

Mailbox accessed:

```text
DEV.DEPARTMENT.INT
```

Commands used:

```text
a2 SELECT DEV.DEPARTMENT.INT
a3 SEARCH ALL
a4 FETCH 1 BODY[]
```

---

# 🔥 Flags Extracted

## Banner Flag

```text
HTB{983uzn8jmfgpd8jmof8c34n7zio}
```

## Mailbox Flag

```text
HTB{983uzn8jmfgpd8jmof8c34n7zio}
```

See:

```text
imap/mailbox_loot.txt
```

---

# 🧠 Attack Path

```text
Nmap Scan
→ Mail Service Enumeration
→ TLS Certificate Analysis
→ IMAPS Banner Disclosure
→ POP3S Version Enumeration
→ IMAP Authentication
→ Mailbox Traversal
→ Internal Mailbox Access
→ Email Retrieval
→ Flag Extraction
```

---

# ⚠️ Security Findings

## 1. Information Disclosure via IMAP Banner

Sensitive information exposed before authentication.

---

## 2. POP3 Version Disclosure

Service version disclosed through banner grabbing.

---

## 3. TLS Metadata Leakage

Internal hostname and email metadata exposed.

---

## 4. Internal Mailbox Exposure

Nested mailboxes accessible after authentication.

---

# 🧰 Tools Used

- Nmap
- OpenSSL
- Manual IMAP interaction

---

# 📚 Lessons Learned

- Manual protocol interaction is critical
- IMAP requires command tags
- Recursive mailbox enumeration exposes hidden mailboxes
- TLS certificates may leak internal infrastructure
- Service banners should always be inspected

---

# ✅ Conclusion

The target exposed multiple information disclosure vectors within its mail services.

Through manual interaction and recursive IMAP mailbox traversal, sensitive information and flags were successfully extracted.
