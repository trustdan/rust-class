# SSH Setup for GitHub on Mac   

## 1. Check for Existing SSH Keys      

Before you add a new SSH key to your GitHub account, you should check whether you have any existing SSH keys.      

Open a terminal and run:   

```bash
ls -al ~/.ssh  

If you see a file named id_rsa.pub, you already have an SSH key.
2. Generate a New SSH Key

If you don't already have an SSH key (or you want to create a new one), you can generate one by running:
bash

ssh-keygen -t ed25519 -C "your_email@example.com"         

Replace your_email@example.com with the email address you used to sign up for GitHub.

When you're prompted to "Enter a file in which to save the key," press Enter to accept the default location. It's recommended you enter a strong passphrase.
3. Add the SSH Key to the ssh-agent

Ensure the ssh-agent is running:
bash

eval "$(ssh-agent -s)"          

Add your SSH private key to the ssh-agent:
bash

ssh-add ~/.ssh/id_ed25519          

If you created your key with a different name, or if you're using a legacy key, the path to the key will be different.
4. Add the SSH Key to Your GitHub Account

Copy the SSH key to your clipboard:
bash

pbcopy < ~/.ssh/id_ed25519.pub

Go to the GitHub website, navigate to your account settings, click on "SSH and GPG keys," and click on "New SSH key." Paste your SSH key into the field and click "Add SSH key."
5. Test the SSH Key

To make sure everything is working, try to SSH to GitHub. You should see a message like "Hi username! You've successfully authenticated."
bash

ssh -T git@github.com          

6. Use SSH URLs for Git Repositories

Finally, when you're cloning Git repositories (like the course repository), use the SSH URL, which looks like git@github.com:username/repo.git.

It's a good idea to backup your SSH keys in case you lose access to them.
For more info on SSH keys, see GitHub's guide: https://help.github.com/en/articles/generating-an-ssh-key
