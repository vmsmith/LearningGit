### Create a repository

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

### Create, add, and commit a file

#### Create

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
    
#### Add    
    
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

#### Commit

Let's make our first commit:

    git commit -m "initial commit"
    
Notice that you did not specify a file to commit. Git committed everything that was in the staging area.    

Also, the `-m` flag told Git that you were going to make a commit message. Git commit messages are hugely important. In time you will want to get more sophisticated in your messages, and you might want to bookmark this article for future reference: [How to Write a Git Commit Message](http://chris.beams.io/posts/git-commit/). For now we'll keep the commit messages simple, but you should get into the habit of writing meaningful commit messages whenever you commit. And by convention, the very first message is "initial commit".
    
Anyway, after the `commit` you should see something like this:

    [master (root-commit) 6b38f0b] initial commit
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 file1.txt

Here's what it means....

### Manage the repo

#### Add *data*

Before we proceed, go to this link and copy the entire Robert Frost poem, [Stopping by the Woods on a Snowy Evening](https://www.poetryfoundation.org/poems-and-poets/poems/detail/42891). Then, in your `project1` directory, create a file called `poem.txt` and paste the Frost poem in it. Then save it.

Since this is a code-agnostic article, we're going to use that poem in our exercises to update our text file, `file1.txt`. Put differently, the poem is going to function as our *data*.

But we have a problem. We do not want to be committing and managing the Frost poem. We only want to have it around to use as *data*. So we need to make the file `poem.txt` invisible to the Git commands.

#### Ignore the *data*

So in your `project` directory, create a hidden file called `.gitignore`:

    vim .gitignore
    
And in it, just write `poem.txt` then save it.

### Make Some Changes

Now you're ready to start seeing what version control is all about.

Copy the first stanza of the Frost poem, and paste it in `file1.txt`. Then save the file and add it.

    git add file1.txt
    
Check the status:

    git status

And...

    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	     modified:   file1.txt

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    .gitignore

We will talk about `reset` and `HEAD` later. For now we want to notice that `.gitignore` did not get added. We had made some changes to the repository earlier, and had then forgotten them.

One way to mitigate that is to use a `.` when you do adds. This tells Git to add *all* files in the repository to the staging area.

    git add .
    
Now when we check the status we see:

    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	  new file:   .gitignore
	  modified:   file1.txt

Great. Now let's commit...

But now we have a problem. We have two files in the staging area, and we want commit messages for each. How do we do that?

For now we will do them separately.

    git commit .gitignore -m "initial commit"
    
Which gave back:

    [master 22116f8] initial commit
    1 file changed, 1 insertion(+)
    create mode 100644 .gitignore
    
And:

    git commit file1.txt -m "added first stanza"
    
Which gave back:

    [master cd59fd1] added first stanza
    1 file changed, 5 insertions(+)

I would point out that even though the first stanza of the poem only has four lines, my commit shows 5 insertions. This is because I added a carriage return at the end.

Notice that in the first line of each feedback message there is a square bracket with `[master _____]` and what looks like some hexidecimal text. That is the key to version control.

When you commit something, Git gives it a SHA-1


