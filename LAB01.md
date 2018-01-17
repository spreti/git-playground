# Lab 01 - Setup and Basic git moves

## Install Git on your system

You are going to need a working git client on your system, be it Linux, Mac OS X or Linux. 

If you don't have it installed yet, follow the instructions for your operating system here: [Getting Started - Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

## Create a Github user and make sure you have a public key

* Register or login to Github.
* Add your commit info to git config. Open terminal (git bash on Windows) and run the following commands with your real details:

```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

* Open the [SSH and GPG keys settings page](https://github.com/settings/keys).
* Press `Add new SSH key`.
* Give the new SSH key a title.
* Open a terminal window.
* Follow the SSH key creation instructions on [Git on the Server - Generating Your SSH Public Key](https://git-scm.com/book/en/v2/Git-on-the-Server-Generating-Your-SSH-Public-Key).
* Copy and paste the SSH key into the Key text box and press `Add SSH Key`

Your terminal is ready for working with Github.

## Fork and clone this repository

* On Github, make sure you are signed in. If you need to sign up, please do it now and go on after you are logged in. 
* Make sure you are on the [master branch of the git-playground repository](https://github.com/tailorvj/git-playground/tree/master).
* Press the Fork button to create your own fork of this repo.
* Press the `Clone or Download` button and copy the git URL you see there.
* Open a terminal window and `$ cd` to your work folder. I have a Github folder under Documents on my Macbook. 
* Clone the forked repo you've just created to your local system.

**In the following example, I'm using my own repo SSH URL. Please use your own repo SSH URL instead.**

```
$ git clone git@github.com:tailorvj/git-playground.git
```

Done. You should have a working copy of your repo on your local machine.

Let's see which branch we are on:

```
$ git branch
```

Notice that the branch you are on in marked with an asterisk *. 

Which branch are you on? 

If the answer is `master`, you have done well so far. Keep on going!

## Checkout the lab01 branch

This repo has many branches, you are now going to checkout the lab01 branch. 

``` 
$ git checkout lab01
$ git branch
```

the `git branch` command should show you that you are on the `lab01` branch. 

## The .gitignore file

The .gitignore file is a special hidden file that holds rules for ignoring specific files or files that match a certain pattern.

For example, the following .gitignore ruleset tells git to ignore various well-known operating system files. 

```
# Example .gitignore file #
# OS generated files #
######################
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db
```

Take a look at some more [examples for .gitignore](https://gist.github.com/octocat/9257657)

Let's edit the `.gitignore` file

**On Mac or Linux** bash (I'm using nano because it is the simplest text editor and hard to get into trouble with it, unlike vi or emacs):

```
$ nano .gitignore
```

**On Windows**, nano isn't available, so first let's setup notepad++ as your editor (I'm assuming you have notepad++ installed)

```
$ git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -nosession"
$ notepad++ .gitignore
```

Add the following line to your .gitignore file:

```
ignoreme.txt
```

* Save .gitignore and exit it.
* Create a file named ignoreme.txt

```
$ touch ignoreme.txt
```

Now let's see what's happened to our branch

```
$ git status
```

As a result of the above command, you should see that .gitignore has changed, but ignoreme.txt isn't mentioned. It worked!

## Staging and committing

Now we finally get to the useful stuff ;)

Let's first make sure you are still on the lab01 branch

```
$ git branch
```

As you've seen just before this, when you typed `$ git status`, git answered that .gitignore has changed. 

In order to make that stick, there are 2 steps:

**Step 1: We need to add .gitignore to the staging area, or the stage.**

It is possible to specify the file name, like this:

```
$ git add .gitignore
```

or simply add all modified files in the current folder, like so:

```
$ git add .
```

Since we are using .gitignore, we should usually use the latter option. It saves time when you have multiple files changed. Anyway, use `git status` every now and then, to see what's going on with the changed in your branch, and used `git branch` to know which branch you are editing.

**Step 2: We need to commit our changes in the current branch**

The git commit command is followed by -m and a message from you to your future self and/or other developers right after it, just like that:

```
$ git commit -m 'added a rule to .gitignore'
```

Run a `$ git status` to see the difference.

Now run the following command:

```
$ git log
```

Pay attention to the information provided to you by the git `status` and `log` commands.

**What have you just done? A comparison of add vs. commit**

It usually takes some time to understand why 2 different commands are needed in order to make changes stick, so this may be a good point for a short explanation. You can read the complete explanation later. For now, it may be too much information anyway.

`git add` is simply an intention, while a `git commit` is actually saved as part of your repo and contains a lot of data and information that helps the system manage versions. 

Once you commit, a snapshot of the current state of your code is saved in the Git repository and will be part of it's life as long as the branch exists.

This usually includes 2 or more hidden files that represent the state of your code during a specific commit, and the files changed between this commit and the previous one it is based upon. 

Again, you don't have to fully understand this at the moment, just remember that `add` is an intention, while `commit` is becoming part of the history of your files in the repository. 

## Push your changes to Github

As you may recall, we've actually cloned the repo you are working on locally, from your forked Github repository. 

Each one of these repositories has a life of its' own, but there is an ongoing connection between them, that is documented in your local repository, and helps you push and fetch changes to/from the server, respectively.

Run the following command to see this information in your terminal:

```
$ git remote -v
``` 

You should get a list of two items: one for fetch and the other for push. Fetching means you can retrieve changes from that remote repository, while push means you can also send the commits you've made in your local repo to that remote repo. 

Your local repository may be linked to multiple remove servers. By default though, after you clone a repository from a server (which is what you did in this case), your local repository automatically has a remote connected to it for fetch, and if you have write privileges on the remote, you will also have a remote push entry connected to your local repo. 

Now, let's push the commit you've made in the lab01 branch to the Github repo:

```
$ git push origin lab01
```

This should push your changes to the lab01 branch on your Github fork. 

## Let's get back to our master branch and merge changes

As you may recall, we are currently in the lab01 branch. It's time to get back to our master branch and put the changes we've made into effect in it, too.

First, let's get back to work on the master branch:

```
$ git checkout master
```

Which branch are we on and what's our status?

```
$ git branch
$ git status
```

Read carefully the result of each one of the above commands. 

### Merging branch lab01 into master

In order to merge the changes made to the .gitignore file on the lab01 branch, just run the following command:

```
$ git merge lab01
```

## Final touch: push to Github

As you may recall, we have a Github push remote connected to our local repository, so let's push the changes from the local master repo to the remote master repo:

```
$ git push origin master
```

That's it! Now is a good time to open your forked repo on Github, open the .gitignore file in the web interface and have a look inside. 

Do you see the change you've made?

Your .gitignore file on both the master and lab01 branches should read:

```
# Example .gitignore file #
# OS generated files #
######################
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db
ignoreme.txt
```

## Further exploration

* Read about the various options from .gitignore

* If you feel confident enough in bash, add the following lines to your ~/.bash_profile to display the current branch you are on during work on git-enabled projects.

```
parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\u@\h \[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "
```

* Fork another project on Github, clone it locally, commit changes to it, then push origin master back to your forked repo on Github. 

* Checkout lab01 again, add new files to it, add them to the stage, commit, git push origin lab01 and locate the changes to that branch on Github.com

* Share your experience and repo on Twitter and mention @tailorvj and #100DaysOfCode, so I can see what you've done.


This was lab01 of the [git-playground](https://github.com/tailorvj/git-playground/)

I hope you've found it useful. Drop me a line on Twitter [@tailorvj](https://www.twitter.com/tailorvj) to tell me what you think.

Cheers,
Tailor Vijay

