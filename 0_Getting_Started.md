

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

    export PATH=$PATH:/usr/local/bin
    
I save and close the `.bash_profile` file, and then source it to

    source ~/.bash_profile
    
Finally, I check to ensure the path has been updated:

    echo $PATH

In my case I got back this:

    /usr/local/bin:/opt/local/bin:/opt/local/sbin:
    /usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:
    /usr/X11/bin:/Library/TeX/texbin

And there you see it, first thing.

### Configuring Git

With Git installed, it's time to configure it.

Git maintains three configuration files:

* One at the system level, called `/etc/gitconfig`
* One at the user level, usually `~/.gitconfig`
* One at the repository level, `.git/config`, a unique one of which will reside in the working directory of each repository.

These are "cascading" in the sense that configurations in each level override, or "trump", those of the previous level(s). Similar to Cascading Style Sheets in web pages.

In other words, configurations in `.git/config` will trump those in `/etc/gitconfig` and `~/.gitconfig`.

At this point you will want to add your user name and e-mail to your global

    git config --global user.name "User Name"
    git config --global user.email johndoe@example.com

### About Version Control

![Git Workflow](./graphics/GitOverview.png)


