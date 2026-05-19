# IMAP Protocol Notes

## Useful Commands

### Capabilities

```text
a1 CAPABILITY
```

### List Mailboxes

```text
a2 LIST "" "*"
```

### Select Mailbox

```text
a3 SELECT INBOX
```

### Search Emails

```text
a4 SEARCH ALL
```

### Read Email

```text
a5 FETCH 1 BODY[]
```

### Read Body Text Only

```text
a6 FETCH 1 BODY[TEXT]
```
