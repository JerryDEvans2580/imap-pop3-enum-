# IMAP Login Notes

## Incorrect Syntax

```text
LOGIN robin Rob2540@
```

## Server Response

```text
BAD First parameter in line is IMAP's command tag
```

## Correct Syntax

```text
a1 LOGIN robin Rob2540@
```

## IMAP Format

```text
<tag> <command> <arguments>
```
