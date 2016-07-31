Create a repository:

First, make a directory called `project1` and `cd` into it:

    mkdir project1
    cd project1
    
Now, in the `project1` directory, initialize a repository and look at what has happened:

    git init
    ls -l -a
    
You should see something like this:

    total 0
    drwxr-xr-x   3 rwjones  staff  102 Jul 31 15:47 .
    drwxr-xr-x   9 rwjones  staff  306 Jul 31 15:45 ..
    drwxr-xr-x  10 rwjones  staff  340 Jul 31 15:47 .git

There is a hidden directory called `.git`. This contains all the information Git needs to manage your repository and the files in it. You might want to `cd` into it and look around. For now, however, we will not be discussing the contents of `.git`.

Create an empty text file. In my world I use `vim`, but you can use any text editor:

    vim file1.txt
    
And check the status of your repository:

    git status
    
You should see something like this:

    On branch master

    Initial commit

    nothing to commit (create/copy files and use "git add" to track)

We will discuss branches and master later on. For now, though, the important thing to note is the last line:

    nothing to commit (create/copy files and use "git add" to track)
    
You created a file, but that action in and of itself has relatively little value for Git. You need to `add` it, which places it in the staging area where it can be tracked. So let's do that:

    git add file1.txt
    
Check the status again:

    On branch master

    Initial commit

    Changes to be committed:
      
      (use "git rm --cached <file>..." to unstage)
    
             new file:   file1.txt
    
What changed?

Line 3 tells you that there are changes to be commited. Those changes -- the file you added -- are actually on line 5. Line 4 tells you that if you are here by mistake, you can back up with `git rm --cached file1.txt`.




