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

## Bugs

Some mail threads are too deep, and jq breaks. I didn't manage to
catch that, so instead of running
```
notmuch-deduplicate '*'
```
it is rather more sensible to run something like this
```
#!/bin/bash

day=$(date -d "$2" +%F)
N="$1"
query="${@:3}"

echo "${query}"

for i in $(seq "1" "${N}"):
do
    echo "Day: ${day}"
    notmuch-deduplicate "date:${day}..${day} ${query}"
    day=$(date -d "${day} - 1 day" +%F)
done
```
