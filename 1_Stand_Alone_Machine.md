<< Previous: [Getting Started](https://github.com/vmsmith/LearningGit/blob/master/0_Getting_Started.md)

### Section Overview

In this section you will learn how to:  
  * Create a repository
  * Stage and commit files to the repository  
  * Manage the repository

### Create a Repository

First, make a directory called `project1` and `cd` into it:

    mkdir project1
    cd project1
    
Now, in the `project1` directory, create (or *initialize*) a repository with `init` and look at what has happened:

    git init
    ls -l -a
    
You should see something like this:

    total 0
    drwxr-xr-x   3 rwjones  staff  102 Jul 31 15:47 .
    drwxr-xr-x   9 rwjones  staff  306 Jul 31 15:45 ..
    drwxr-xr-x  10 rwjones  staff  340 Jul 31 15:47 .git

There is a hidden directory called `.git`. This contains all the information Git needs to manage your repository and the files in it. You might want to `cd` into it and look around. For now, however, we will not be discussing the contents of `.git`.

### Stage and Commit a File

Create an empty text file and call it `file1.txt`. In my world I use the `touch` command, but you can do it with any text editor:

    touch file1.txt
    
Now check the status of your repository:

    git status
    
You should see something that looks like this (it may look slightly different, but don't worry about it):

    On branch master

    Initial commit

    nothing to commit (create/copy files and use "git add" to track)

We will discuss branches and master later on. For now, though, the important thing to note is the last line:

    nothing to commit (create/copy files and use "git add" to track)
    
You created a file, but that action in and of itself has relatively little value for Git. You need to place it in the staging area where it can be tracked. You do that with the `add` command.

#### Stage a File    

    git add file1.txt
    
Check the status again:

    On branch master

    Initial commit

    Changes to be committed:
      
      (use "git rm --cached <file>..." to unstage)
    
             new file:   file1.txt
    
What changed?

Line 3 tells you that there are changes to be commited. Those changes -- the file you added -- are actually on line 5. (Line 4 tells you that if you are here by mistake, you can back up with `git rm --cached file1.txt`. We will discuss that -- and related topics -- later.)

#### Commit a File

Let's make our first commit:

    git commit file1.txt 
    
You will almost certainly get some sort of message you were not expecting that will begin something like this:

    Please enter the commit message for your changes... 
    
When you `commit` a file, you *need* to include a "commit message." This is a little message associated with that commit that explains the reason for the commit. This, in turn, let's you review the history of your commits later on so you can reach back in time and use an earlier version of your code if you want to.

So let's try it again. Get yourself back to the command line and enter:

    git commit file1.txt -m "initial commit"
    
That `-m` is called a flag, and it told Git that you were going to make a commit message. Again, Git commit messages are hugely important. In time you will want to get more sophisticated in your messages, and in fact you might want to bookmark this article for future reference: [How to Write a Git Commit Message](http://chris.beams.io/posts/git-commit/). For now we'll keep the commit messages simple, but you should get into the habit of writing meaningful commit messages whenever you commit. And by convention, the very first message is "initial commit".
    
After the `commit` you should see something like this:

    [master (root-commit) 7fdadf7] initial commit
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 file1.txt

Here's what it means (although don't worry about memorizing this):

* Line 1: *master* refers to the branch you are working on, and we will discuss branches later;  
          `7fdadf7` is the first seven characters of this commit's signature, and we will discuss that shortly;  
          *initial commit* is your commit message
* Line 2: This says that you made a change, but did not add or delete anything.
* Line 3: This is a technical way of saying you created file1.txt in mode 100644, which is an internal representation of file type and file permissions.

Again, don't feel compelled to memorize this, just know that it exists and has meaning.

### Manage the repo

#### Add some *data*

Before we proceed, let's flesh out the project.

Go to this link and copy the entire Robert Frost poem, [Stopping by the Woods on a Snowy Evening](https://www.poetryfoundation.org/poems-and-poets/poems/detail/42891). Then, in your `project1` directory, create a text file called `data1.txt` and paste the Frost poem in it. Then save it. Now copy the Robert Frost poem, [The Road Not Taken](https://www.poetryfoundation.org/resources/learning/core-poems/detail/44272), and save it in `project1` as `data2.txt`. **Note:** Do not copy the poems' titles or author name; just copy the poems themselves.

Since this is a code-agnostic article, we're going to use text (in the form of poems) in our exercises to update our files. Put differently, the poems are going to function sort of like project *data*.

But we have a problem. We do not want to be committing and managing the Frost poems. We only want to have them around to use as *data*. So we need to make the files `data1.txt` and `data2.txt` invisible to the Git commands.

#### Ignore the *data*

So in your `project` directory, create a hidden file called `.gitignore`:

    vim .gitignore
    
And in it, just write `data1` on the first line and `data2` on the second line. Then save `.gitignore`. From now on, Git will ignore both poem files when doing adds and commits.

### Make Some Changes

Now you're ready to start seeing what version control is all about.

Copy the first stanza of `data1` and paste it in `file1.txt`. Then save the file and add it.

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

We will talk about `reset` and `HEAD` later. For now we want to notice two things...

First, that `files1.txt` has been modified.

Second, that `.gitignore` is not being tracked.  Although we made some changes to it (and hence, the repository) earlier, we forgot to add and commit them.

One way to mitigate that is to use a `.` with the `add` command. This tells Git to add *all* files in the repository (except those in `.gitignore`) to the staging area. Try it...

    git add .
    
Now when we check the status we see:

    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	  new file:   .gitignore
	  modified:   file1.txt

Great...time to commit.

But now we have a problem. We have two files in the staging area, and we want commit messages for each. How do we do that?

For now we will do them separately.

    git commit .gitignore -m "initial commit"
    
Which gave back (for me) this:

    [master ea3bcac] initial commit
    1 file changed, 2 insertion(+)
    create mode 100644 .gitignore

Notice "2 insertions". This refers to the two data files -- each on its own line -- in the `.gitignore` file.

And:

    git commit file1.txt -m "added first stanza"
    
Which gave back:

    [master d8dd3bd] added first stanza
    1 file changed, 4 insertions(+)

Again, the "4 insertions" refers to the four lines in the stanza you added.

Notice that in the first line of each feedback message there is a square bracket with `[master nnnnnnn]`, with those seven `n`s being  what looks like some hexidecimal text. That is the key to version control.

When you make a commit, Git creates something called a [SHA1 hash](https://en.wikipedia.org/wiki/SHA-1). The SHA1 hash function takes some data as input and generates a unique 40 hexidecimal character string from it. By "unique," we mean that no other input should ever produce the same 40 character output. But...the same input data should *always* produce the exact same hash output.

Those seven characters in the square brackets after "master" are the first seven characters of the 40 character SHA1 output associated with that commit.

And this is the key to being able to track your versioning and roll back to earlier versions of your work.

### Checking History

At this point, you have made three changes:

* The initial commit of `file1.txt`
* The initial commit of `.gitignore`
* The addition of the first stanza to `file1.txt`

You can take a look at this history with `git log`:

    git log
    
And you should get something like this:

    commit cd59fd116b78e92c4de8444ab98d177bd0a2f208
    Author: vmsmith <redditor.vmsmith@gmail.com>
    Date:   Sun Jul 31 16:40:44 2016 -0400

        added first stanza

    commit 22116f81f244f637dc1b659cfc346e1651d453e3
    Author: vmsmith <redditor.vmsmith@gmail.com>
    Date:   Sun Jul 31 16:40:17 2016 -0400

        initial commit

    commit 6b38f0bee17c1db419e223bedf10eca6f4b85dd9
    Author: vmsmith <redditor.vmsmith@gmail.com>
    Date:   Sun Jul 31 16:02:42 2016 -0400

        initial commit

This is a reverse history (i.e., most recent on top) of what you have done. And nothing should look too strange other than the very long sequence of letters and numbers after the word "commit". What does this mean?

That number is the full [SHA-a hash](https://en.wikipedia.org/wiki/SHA-1) of your commit. You can read about hashes in general, and SHA-1 in particular, through the Wikipedia link. The short version, however, is that every time you commit, Git using a special cryptographic function to compute a hash of your commit. This is an alphanumeric string that is unique to the input that was provided. In this case, the input was your commit. 

One of the features of a good hash function is that it will always produce the same output (that alphnumeric string) if you use the same input. But if you make even the tiniest change, the output will be different. So that output can actually serve as the signature, or name, of your commit. 

And if you go back and look at the very first commit, you'll see these seven characters: `6b38f0b`. Note that these are the first seven characters of the entire hash output. 

### Recalling Earlier Commits

OK, let's add another stanza to the poem, then add and commit.

    [master 2e78d29] added second stanza
     1 file changed, 4 insertions(+)
     
Notice that the seven character string has changed. That's because the file changed and what you committed is different.

Now take a look at the history:

    git log
    
And you'll see that this is not the top entry:

    commit 2e78d290de87c1c324a86f62447d19f8e7778392
    Author: vmsmith <redditor.vmsmith@gmail.com>
    Date:   Wed Aug 17 08:59:21 2016 -0400

        added second stanza

Suppose that, for whatever reason, you wanted to bring up an earlier version of file1.txt. Suppose you wanted to bring up a version of the file with only the first stanza.

<< Previous: [Getting Started](https://github.com/vmsmith/LearningGit/blob/master/0_Getting_Started.md) || Next: [GitHub and the Web](https://github.com/vmsmith/LearningGit/blob/master/2_GitHub_and_the_Web.md) >>
