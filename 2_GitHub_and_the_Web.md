### SSH keys

Check if SSH key(s) already exist

    ls -al ~/.ssh
    ls -al /home/username/.ssh
    
By default, the filenames of the public keys are one of the following:

    id_dsa.pub
    id_ecdsa.pub
    id_ed25519.pub
    id_rsa.pub

If you don't have an existing public and private key pair, or don't wish to use any that are available to connect to GitHub, then generate a new SSH key.

    ssh-keygen -t rsa -C "your_email@example.com"
    
There will be a little process to go through, but it's quick and you will now know the name of the file that contains the public key.

Copy the new SSH key and paste it to GitHub. To copy, you can just run:

    cat /directory/id_rsa.pub
    
Or something like that. The key will appear in the terminal, where you can highlight and copy it.

On GitHub, click on the user icon on the front page, and then "SSH and GPG Keys". Click "New SSH Key", and then paste the key and save it.

### Create a repository on GitHub

Initialize a repository on GitHub.

Do not initialize the new repository with README, license, or gitignore files. You can add these files after your project has been pushed to GitHub.

On the new repo page there may be instructions for what to do next. If not, copy the URL of the repo. Make sure it's the URL associated with SSH keys.

### On the local machine

Open a terminal window and CD into the .git repository

Enter:

    git remote add origin remote-repository-URL

    git remote -v
    
    git push -u origin master
    
Refresh the GitHub repository to check that the committed data is there.

### Cloning to another machine

    $ git clone ssh://user@server/project.git
