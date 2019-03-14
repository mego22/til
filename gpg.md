GPG
----
A tool to provide digital encryption and signing services using the OpenPGP standard


## Encrypting
### Encrypting a file
This will encrypt FILE in ASCII armored output.

```
gpg --armour --encrypt --trust-model always --recipient UID --output FILE.gpg FILE
```

### Encrypting output from a command
This will encrypt `testing123` in ASCII armored output.

```
echo testing123 | gpg --armour --encrypt --trust-model always --recipient UID --output FILE.gpg
```

### Decrypting a file
```
gpg --decryp FILE.gpg --output FILE
```

## Importing keys
### Import public keys from a url
```
curl URL | gpg --import
```

### Import public keys from a file
```
cat FILE | gpg --import

```

### Trust imported public key
When prompted provide the email/uid of the key you want to trust

```
read KEY && echo $(gpg --list-keys --fingerprint | grep "${KEY}" -B 1 | head -1 | tr -d '[:space:]' | awk 'BEGIN { FS = "=" } ; { print $2 }'):6: | gpg --import-ownertrust
```

## List UIDs of imported GPG keys
```
gpg --list-keys  | grep uid | awk '{sub(/</,"")} {sub(/>/,"")}1 {print $NF}'
```
