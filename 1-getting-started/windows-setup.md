### enable ssh in Windows 10 / 11:
Open the Settings app (Windows key + I)
Go to Apps > Apps & features
On the left, click "Optional features"
Click "Add a feature" at the top of the page
In the list of available optional features, find and select "OpenSSH Client (Beta)"
Click "Install" to download and install the OpenSSH Client feature
Once the installation completes, you should see "OpenSSH Client (Beta)" listed under "Installed features"
Open PowerShell and run ssh -V to verify the OpenSSH client installed properly.
You should see output like:

```
OpenSSH_for_Windows_8.1p1, LibreSSL 2.6.5
```

    You can now generate SSH keys and use the ssh command to connect to SSH servers from PowerShell and CMD.



### Here are the steps to generate an SSH key and encrypt it with GPG on Windows using PowerShell:

Generate a large (8092 bit) RSA SSH key pair

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
