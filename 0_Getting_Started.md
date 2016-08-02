

### Downloading and Installing Git

The starting point on your Git journey is the [Git web site](https://git-scm.com/). There you can [download](https://git-scm.com/downloads) the version of Git that is suited for your particular operating system: Mac, Linux, or Windows.

Download it and install it.

A word of warning: I use a Mac, and this guide has a Mac bias. If you are using Linux you probably don't need this guide anyway. But if you are a Windows user, I think there are some quirks you'll need to deal with. I'll try to address those as we go along, but I cannot promise anything.

Once its' installed, check to make sure your version matches the latest version listed on the web site:

    git -version

Now you want to add Git to your environment. Here's how I do it...

First, I check to find out where it's installed:

    which git
    
I get back something like this:

    /usr/local/bin/git

Note that depending on your OS X version you might have a slightly different path.

Then, I open my `.bash_profile` file...

    vim .bash_profile
    
And add this:

    export PATH=$PATH:/usr/local/bin/git
    
I save and close the `.bash_profile` file, and then source it to

    source ~/.bash_profile
    
Finally, I check to ensure the path has been updated:

    echo $PATH

### Configuring Git



### About Version Control

![Git Workflow](./graphics/GitOverview.png)


