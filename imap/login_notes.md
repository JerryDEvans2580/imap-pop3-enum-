# IMAP Login Notes

## Incorrect Syntax

```text
LOGIN robin robin
```

## Server Response

```text
BAD First parameter in line is IMAP's command tag
```

## Correct Syntax

```text
a1 LOGIN robin robin
```

## IMAP Format

```text
<tag> <command> <arguments>
```
