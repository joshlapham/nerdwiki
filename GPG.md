## Example usages

### List keys

`gpg --list-keys`

### Encrypt with recipient

`gpg -e -r user@example.com file.txt`

### Encrypt as .asc

`gpg -ea -r user@example.com file.txt`

### Decrypt

`gpg -d file.txt.asc`


### Export Public Key

`gpg --export --armor $EMAIL > $EMAIL.asc`

### Import Public Key

`gpg --import $EMAIL.asc`
