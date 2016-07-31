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

