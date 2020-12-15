# Multiple SSH Keygen Configuration
If you have multiple **git** accounts it can be hard to push and pull from repositories with different credentials. 

To do it the right way, we create an SSH key and configure it to the git account. But when you have multiple accounts like one in **github.com** and one in **bitbucket.org**, you cannot use one SSH key in both the accounts. So here is the solution,

1. Create SSH keys for each github.com account and bitbucket.org account
2. Register the correct SSH keys with the correct github.com account and bitbucket.org account
3. Create a git config file

### Creating SSH Keys
You create a new key by running the following command, substituting for your own email address:
```
 cd ~
 mkdir .ssh
 cd ~/.ssh
 ssh-keygen -t rsa -b 4096 -C “your_email@example.com”
```
You’ll be prompted to **“Enter file in which to save the key”**. So let’s assume you need to make accounts for a personal SSH key and a work one. You can create as many SSH keys as you like.

Call the first key *rsa_personal*, next secure the key with a passphrase. Now repeat the steps to create a new SSH key for your work account, name the file *rsa_work* and secure the key with a passphrase.

### Listing all SSH Keys
To view all the SSH Keys generated and the one already present in system, go to folder `~/.ssh` using following command:
```
 cd ~/.ssh
 ls
```
You will get below results
```
 rsa_personal rsa_personal.pub rsa_work rsa_work.pub
```

### Registering all SSH Keys
Copy keys and register SSH keys to github.com or bitbucket.org. To copy ssh key run below command:
```
 pbcopy < ~/.ssh/rsa_personal.pub
```
Paste the public key into SSH configuration in git account. Repeat that for all the keys.

### Create git config
Now let's create a git configuration file in `~/.ssh` folder, so when we try to access keys ssh will know which one to use. Go to folder `~/.ssh` using following command:

```
 cd ~/.ssh
 touch config
 nano config
```
Add the following configure for each SSH Key:
```
 #github account configuration
 Host github.com
        HostName ssh.github.com
        Port 443
        User git
        IdentityFile ~/.ssh/rsa_personal

 #bitbucket account
 Host bitbucket.org
        HostName altssh.bitbucket.org
        Port 443
        User git
        IdentityFile ~/.ssh/rsa_work
```

### Conclusion
If you followed along you hopefully now have everything you need to painlessly manage multiple projects hosted across different git accounts (github.com or bitbucket.org).
