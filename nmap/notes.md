# Nmap Enumeration Notes

## Services Identified

- POP3 - 110/tcp
- IMAP - 143/tcp
- IMAPS - 993/tcp
- POP3S - 995/tcp

## Backend Software

- Dovecot pop3d
- Dovecot imapd

## Interesting Findings

- Internal hostname disclosed through TLS certificate:
  - dev.inlanefreight.htb

- Internal email discovered in certificate:
  - cto.dev@dev.inlanefreight.htb

## IMAP Capabilities

- IMAP4rev1
- STARTTLS
- AUTH=PLAIN
- SASL-IR
- IDLE
- LITERAL+

## POP3 Capabilities

- USER
- SASL / SASL(PLAIN)
- UIDL
- PIPELINING
- TOP
- CAPA

## Security Relevance

The Nmap scan confirmed that the target exposes multiple mail services.  
Certificate metadata and protocol capabilities helped identify further enumeration paths, including manual TLS interaction, banner grabbing, and IMAP mailbox traversal.
