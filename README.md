# Simple repo that covers the steps on how to create an SSH key for use with git.

Some steps have prompts, but they should be self explanatory...

```bash
ssh-keygen -t ed25519 -C "user@example.cloud"
ssh-add ~/.ssh/id_ed25519
cat ~/.ssh/id_ed25519.pub
```
Copy the line that the `cat` generates.  

In the upper-right corner of any page on GitHub, click your profile picture, then click `Settings`  
Click `SSH and GPG keys`  
Click `New SSH key or Add SSH key`  
In the "Title" field, add a descriptive label for the new key, identifying the machine/os it's used on.  
Select `Auth key`  
In the "Key" field, paste your public key (from the cat command above)  

Edit the file `~/.ssh/config` so it looks exactly like this (username must be git):
```bash
Host git.host.repository.com
  HostName git.host.repository.com
  User git
  IdentityFile ~/.ssh/id_ed25519
```

Git commands are a bit different as you need to tell it to use the SSH method for auth.
```bash
git clone ssh://git@github.com/USER/REPO
```

If needed, set globals
```bash
git config --global user.email "84707480+eakse@users.noreply.github.com"
git config --global user.name "eakse"
```
If it complains about email address, reset the author to the one set above
```bash
git commit --amend --reset-author --no-edit
```
