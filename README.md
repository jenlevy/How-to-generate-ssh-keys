# How-to-generate-ssh-keys
How to generate ssh keys for your github account on newer Macs! Also how to generate and store multiple ssh keys for multiple github accounts :D

**Generate SSH key**
email should be the email of ur github  
ssh-keygen -t ed25519 -C "whatever_your_email_is@email.com"

**Start the SSH agent**
eval "$(ssh-agent -s)"

**Add the SSH private key to your agent and macOS keychain**
ssh-add --apple-use-keychain ~/.ssh/id_ed25519

**Copy the public key to your clipboard**
pbcopy < ~/.ssh/id_ed25519.pub

 **Go to GitHub → Settings → SSH and GPG keys → New SSH key**  
Paste and save your key

**Test the connection**
ssh -T git@github.com


## Add a Second GitHub Account Using SSH Alias ##

**Generate a second SSH key**
ssh-keygen -t ed25519 -C "yourotheremail@example.com" -f ~/.ssh/id_ed25519_alias  
(choose whatever name for the alias u want!)

**Add the new key to the SSH agent**
ssh-add --apple-use-keychain ~/.ssh/id_ed25519_alias

**Copy the new public key to your clipboard**
pbcopy < ~/.ssh/id_ed25519_alias.pub

**Add it to your second GitHub account (Settings → SSH and GPG Keys → New SSH Key)**  

**Edit SSH config**
nano ~/.ssh/config

**Paste the following:**
# Personal GitHub
Host github.com-personal
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519
  UseKeychain yes
  AddKeysToAgent yes

**Other GitHub**
Host github.com-other
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_alias
  UseKeychain yes
  AddKeysToAgent yes

**Clone repos using aliases**
Personal:  
git clone git@github.com-personal:yourusername/repo.git
Work:  
git clone git@github.com-alias:yourworkusername/repo.git