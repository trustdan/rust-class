# HOW-TO for getting your Mac terminal set up for communication with Github or Gitlab
### If you delete / can't unencrypt your ssh keys ever, you should be able to just go back into Github or Gitlab in your browser and put a new key in there, since the old one isn't useful to you anymore (locked / lost).
## When in doubt ask Claude+ / Poe Sage / ChatGPT.

# Enable ssh in macOS:

### SSH is installed by default on macOS. You can verify it is enabled by opening Terminal and running:
bash

```
ssh -V
``` 

You should see output like:

```
OpenSSH_7.9p1, LibreSSL 2.7.3
```

This indicates the OpenSSH SSH client is installed and enabled.

### Here are the steps to generate an SSH key and encrypt it with GPG on macOS:

Generate a large (8092 bit) RSA SSH key pair
bash

```
ssh-keygen -t rsa -b 8092
```

This will generate an RSA SSH key pair with 8092 bit keys

You will be prompted to enter a filename for the keys (press Enter for default id_rsa)
And prompted to enter a passphrase for the private key (optional, but recommended)

### Add the SSH key to the SSH agent:
bash

```
ssh-add -K ~/.ssh/id_rsa 
```

### Add the SSH key to GitHub:
(Follow the steps in the previous response)

Test your SSH connection:
bash

```
ssh -T git@github.com
```

You should see a success message.

Your SSH key is now set up and ready to use with GitHub!


### Generate a GPG key to encrypt your ssh key

```
gpg --full-gen-key
```

## Export your GPG public key
bash

```
gpg --export --armor your_email > public.key
```

Replace your_email with the email address associated with your GPG key

This exports your public GPG key to the file public.key

## Zip up the SSH keys
bash

```
zip keys.zip id_rsa id_rsa.pub 
```

This zips the SSH private and public key into the file keys.zip

### Encrypt the zip file with your GPG key
bash

```
gpg -c -r your_email keys.zip  
```

This encrypts the keys.zip file using your GPG key
And generates an encrypted file named keys.zip.gpg

Remove the unencrypted zip file (optional)
bash

```
rm keys.zip  
```

### To decrypt the keys on a new device:

Export your GPG key from the original device using
bash

```
gpg --export --armor your_email > key.gpg
```

### Install GPG Suite on the new device and import your key using
bash

```
gpg --import key.gpg  
```

Decrypt the encrypted file using
bash

```
gpg --output ssh_keys.zip --decrypt ssh_keys.zip.gpg  
```

This will output the ssh_keys.zip file containing your unencrypted SSH keys!

You only need to export and import the specific GPG key used to encrypt the file. Not the entire GPG Suite setup.
The keys can then be decrypted on a new device as long as that GPG key is installed.
