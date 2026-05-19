# IMAP Mailbox Enumeration

## Initial Enumeration

```text
1 LIST "" *
```

Result:

```text
* LIST (\Noselect \HasChildren) "." DEV
* LIST (\Noselect \HasChildren) "." DEV.DEPARTMENT
* LIST (\HasNoChildren) "." DEV.DEPARTMENT.INT
* LIST (\HasNoChildren) "." INBOX
```

---

# Mailbox Analysis

## DEV

```text
(\Noselect \HasChildren)
```

- Cannot be selected directly
- Contains nested mailboxes

---

## DEV.DEPARTMENT.INT

```text
(\HasNoChildren)
```

- Selectable mailbox
- Terminal mailbox

---

# Mailbox Selection

Incorrect:

```text
SELECT DEV.DEPARTMENT.INT
```

Correct:

```text
1 SELECT DEV.DEPARTMENT.INT
```

Result:

```text
* 1 EXISTS
1 OK [READ-WRITE] Select completed
```
