# Deduplicate Maildir using Notmuch

A simple bash-script to find duplicated mails and deduplicate them
with a hardlink.

## Requirements

 + notmuch
 + GNU/parallel
 + jq
 + pv

## Usage

Just run
```
notmuch-deduplicate <query>
```
where `<query>` is a notmuch query.
