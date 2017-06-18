### SSH keys

Check if SSH key(s) already exist

    ls -al ~/.ssh
    
By default, the filenames of the public keys are one of the following:

    id_dsa.pub
    id_ecdsa.pub
    id_ed25519.pub
    id_rsa.pub

If you don't have an existing public and private key pair, or don't wish to use any that are available to connect to GitHub, then generate a new SSH key.

### Create a repository on GitHub

Do not initialize the new repository with README, license, or gitignore files. You can add these files after your project has been pushed to GitHub.

On the new repo page there may be instructions for what to do next. If not, copy the URL of the repo.

### On the local machine

Open a terminal window and CD into the .git repository

Enter:

    git remote add origin remote-repository-URL

    git remote -v
    
    git push -u origin master
    
Refresh the GitHub repository to check that the committed data is there.
