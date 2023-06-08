# SSH Setup for GitHub on Debian / Fedora Linux   

## 1. Check for Existing SSH Keys      

Before you add a new SSH key to your GitHub account, you should check whether you have any existing SSH keys.      

Open a terminal and run:

```bash 
sudo ls -al ~/.ssh   
```

If you see a file named id_rsa.pub, you already have an SSH key.

### Generating an SSH key 

```
sudo apt -f install ssh -y
``` 

Generate a large (8092 bit) RSA SSH key pair

```
sudo ssh-keygen -t rsa -b 8092
```

This will generate an RSA SSH key pair with 8092 bit keys

You will be prompted to enter a filename for the keys (press Enter for default id_rsa)

And prompted to enter a passphrase for the private key (optional, but recommended)

### using gnupg to encrypt your ssh files

```
sudo apt install gnupg
```

```
sudo gpg --gen-key
```

Export your GPG public key

```
sudo gpg --export --armor your_email > public.key
```

Replace your_email with the email address associated with your GPG key
This exports your public GPG key to the file public.key

Zip up the SSH keys

```
sudo zip keys.zip id_rsa id_rsa.pub
```

This zips the SSH private and public key into the file keys.zip

Encrypt the zip file with your GPG key

```
sudo gpg -c -r your_email keys.zip
```

This encrypts the keys.zip file using your GPG key
And generates an encrypted file named keys.zip.gpg

Remove the unencrypted zip file (optional)

```
sudo rm keys.zip
```

You can remove the original unencrypted keys.zip file if you want

To decrypt the keys on a new device:

Export your GPG key from the original device using 

```
sudo gpg --export --armor your_email > key.gpg
```

Install GnuPG on the new device and import your key using 

```
sudo gpg --import key.gpg
```

Decrypt the encrypted file using 

``` 
sudo gpg --output ssh_keys.zip --decrypt ssh_keys.zip.gpg
```

This will output the ssh_keys.zip file containing your unencrypted SSH keys!

You only need to export and import the specific GPG key used to encrypt the file. Not the entire GnuPG setup
The keys can then be decrypted on a new device as long as that GPG key is installed.

