<< Previous: [Getting Started](https://github.com/vmsmith/LearningGit/blob/master/0_Getting_Started.md)

### Create a repository

First, make a directory called `project1` and `cd` into it:

    mkdir project1
    cd project1
    
Now, in the `project1` directory, initialize a repository with `init` and look at what has happened:

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

Create an empty text file. In my world I use [`vim`](https://en.wikipedia.org/wiki/Vim_(text_editor)), but you can use any text editor:

    vim file1.txt
    
Now check the status of your repository:

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

    git commit file1.txt -m "initial commit"
    
Note that the `-m` flag told Git that you were going to make a commit message. Git commit messages are hugely important. In time you will want to get more sophisticated in your messages, and in fact you might want to bookmark this article for future reference: [How to Write a Git Commit Message](http://chris.beams.io/posts/git-commit/). For now we'll keep the commit messages simple, but you should get into the habit of writing meaningful commit messages whenever you commit. And by convention, the very first message is "initial commit".
    
Anyway, after the `commit` you should see something like this:

    [master (root-commit) 6b38f0b] initial commit
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 file1.txt

Here's what it means (although don't worry about memorizing this):

* Line 1: *master* refers to the branch you are working on, and we will discuss branches later  
          `6b38f0b` is the first seven characters of this commit's signature, and we will discuss that shortly  
          *initial commit* is your commit message
* Line 2: 
* Line 3:

Again, don't feel compelled to memorize this, just know that it exists and has meaning.

### Manage the repo

#### Add *data*

Before we proceed, go to this link and copy the entire Robert Frost poem, [Stopping by the Woods on a Snowy Evening](https://www.poetryfoundation.org/poems-and-poets/poems/detail/42891). Then, in your `project1` directory, create a text file called `poem.txt` and paste the Frost poem in it. Then save it.

Since this is a code-agnostic article, we're going to use that poem in our exercises to update our text file, `file1.txt`. Put differently, the poem is going to function as our *data*.

But we have a problem. We do not want to be committing and managing the Frost poem. We only want to have it around to use as *data*. So we need to make the file `poem.txt` invisible to the Git commands.

#### Ignore the *data*

So in your `project` directory, create a hidden file called `.gitignore`:

    vim .gitignore
    
And in it, just write `poem.txt` then save it. From now on, Git will ignore `poem.txt` when doing adds and commits.

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

We will talk about `reset` and `HEAD` later. For now we want to notice that `.gitignore` did not get added. We had made some changes to it (and hence, the repository) earlier, but we forgot to add and commit them.

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

When you make a commit, Git creates something called a [SHA1 hash](https://en.wikipedia.org/wiki/SHA-1). The SHA1 hash function takes some data as input and generates a unique 40 character string from it. By "unique," we mean that no other input should ever produce the same 40 character output. But...The same input data should *always* produce the exact same hash output.

Those seven or so characters in the square brackets after "master" are the first seven characters of the 40 character SHA1 output associated with that commit.

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

This is a reverse history (i.e., most recent on top) of what you have done. And nothing should look to strange other than the very long sequence of letters and numbers after the word "commit". What does this mean?

That number is the [SHA-a hash](https://en.wikipedia.org/wiki/SHA-1) of your commit. You can read about hashes in general, and SHA-1 in particular, through the Wikipedia link. The short version, however, is that every time you commit, Git using a special cryptographic function to compute a hash of your commit. This is an alphanumeric string that is unique to the input that was provided. In this case, the input was your commit. 

One of the features of a good hash function is that it will always produce the same output (that alphnumeric string) if you use the same input. But if you make even the tiniest change, the output will be different. So that output can actually serve as the signature, or name, of your commit. 

And if you go back and look at the very first commit, you'll see these seven characters: `6b38f0b`. Note that these are the first seven characters of the entire hash output. 

### Recalling Earlier Commits

OK, let's add another stanza to the poem, then add and commit.

    [master 2e78d29] added second stanza
     1 file changed, 4 insertions(+)
     
Notice that seven character string has changed. That's because the file changed and what you committed is different.

Now take a look at the history:

    git log
    
And you'll see that this is not the top entry:

    commit 2e78d290de87c1c324a86f62447d19f8e7778392
    Author: vmsmith <redditor.vmsmith@gmail.com>
    Date:   Wed Aug 17 08:59:21 2016 -0400

        added second stanza

Suppose that, for whatever reason, you wanted to bring up an earlier version of file1.txt. Suppose you wanted to bring up a version of the file with only the first stanza.

<< Previous: [Getting Started](https://github.com/vmsmith/LearningGit/blob/master/0_Getting_Started.md) || Next: GitHub and the Web >>
