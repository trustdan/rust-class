## Here are the steps to generate an SSH key and encrypt it with GPG on Windows using PowerShell:
### Generate a large (8092 bit) RSA SSH key pair

```
ssh-keygen -m PEM -t rsa -b 8092
```

This will generate an RSA SSH key pair with 8092 bit keys
You will be prompted to enter a filename for the keys (press Enter for default id_rsa)
And prompted to enter a passphrase for the private key (optional, but recommended)

### Export your GPG public key

```
gpg --export --armor your_email > public.key
```

Replace your_email with the email address associated with your GPG key
This exports your public GPG key to the file public.key

### Zip up the SSH keys

```
Compress-Archive -Path id_rsa,id_rsa.pub -DestinationPath keys.zip
```

This zips the SSH private and public key into the file keys.zip
Encrypt the zip file with your GPG key

```
gpg -c -r your_email keys.zip
```

This encrypts the keys.zip file using your GPG key
And generates an encrypted file named keys.zip.gpg

### Remove the unencrypted zip file (optional)

```
Remove-Item keys.zip
```

To decrypt the keys on a new device:

###  Export your GPG key from the original device

```
gpg --export --armor your_email > key.gpg
```

### Install GPG4Win on the new device and import your key
```
gpg --import key.gpg
```

### Decrypt the encrypted file
```
gpg --output ssh_keys.zip --decrypt ssh_keys.zip.gpg
```

This will output the ssh_keys.zip file containing your unencrypted SSH keys!

You only need to export and import the specific GPG key used to encrypt the file. Not the entire GPG4Win setup.
The keys can then be decrypted on a new device as long as that GPG key is installed.
