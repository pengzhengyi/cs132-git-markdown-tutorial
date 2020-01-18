# Info
A tutorial on Markdown and Git  
Author: Zhengyi Peng <zhengyi_peng@brown.edu>  
[Source In Markdown](./markdown-git.md)

## Table of Contents
+ [Markdown: Syntax and Tools](#markdown)
+ [Git: Basic Usages When Working Alone](#git)

# [Markdown](https://daringfireball.net/projects/markdown/)
> Markdown is a lightweight markup language with plain text formatting syntax. 
> Its design allows it to be converted to many output formats, but the original tool by the same name only supports HTML.
> Markdown is often used to format readme files, for writing messages in online discussion forums, and to create rich text using a plain text editor.

## Syntax
+ [Official](https://daringfireball.net/projects/markdown/syntax)
+ [Github](https://help.github.com/en/articles/basic-writing-and-formatting-syntax)

## Apps and Integrations
+ [Grip: Markdown Preview In Github Flavor](https://github.com/joeyespo/grip)
    > Grip is a command-line server application written in Python that uses the GitHub markdown API to render a local readme file.
    > The styles come directly from GitHub, so you'll know exactly how it will appear.
    > Changes you make to the Readme will be instantly reflected in the browser without requiring a page refresh.
    + Install:
        + `$ pip install grip`
        + `$ brew install grip` (**MACOS**)
    + Usage:
        + `$ grip <markdown-file>`
+ [MacDown: open source Markdown editor for OS X](https://github.com/MacDownApp/macdown)
    ![app screenshot](https://github.com/MacDownApp/macdown/blob/master/assets/screenshot.png)
+ [vim-markdown](https://github.com/plasticboy/vim-markdown)
    > Syntax highlighting, matching rules and mappings for the original Markdown and extensions.

# [Git](https://git-scm.com)
> Git (/ɡɪt/) is a distributed version-control system for tracking changes in source code during software development.
> It is designed for coordinating work among programmers, but it can be used to track changes in any set of files.
> Its goals include speed, data integrity, and support for distributed, non-linear workflows.

## [GUI Clients](https://git-scm.com/downloads/guis)

## Command Line
Modeled after [Git Immersion](http://gitimmersion.com/index.html)
> A guided tour that walks through the fundamentals of Git, inspired by the premise that to know a thing is to do it.

### [Initializing a Repository in an Existing Directory](https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository)
* cd into the project folder  
  ```
  $ mkdir d3-demo
  $ cd d3-demo
  ```

* transforms a normal directory into a git directory  
  `git init`

### First Commit

```
$ touch d3-demo.html
$ git add d3-demo.html
$ git commit -m "create target file"
```

`git add <file>` add changes in files to the next commit

The string afters `-m` is the commit message, it's always a good
idea to remind yourself why this commit is necessary and what's
changed

### Check The Current Status Of The Directory
```sh
$ git status
On branch master
nothing to commit, working tree clean
```
The output says there isn't any untracked change from last commit

### Modify and Commit New Changes
##### write a skeleton HTML page
```html
<!doctype html>
<html lang="en">
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
      <title>CSCI1320: D3 Lecture Demo</title>
    </head>
    <body>
      <script>
      </script>
    </body>
</html>
```

##### git automatically finds out the changes in working directory
    
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

  modified:   d3-demo.html

no changes added to commit (use "git add" and/or "git commit -a")
```

##### stage the changes

```
$ git add d3-demo.html
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

  modified:   d3-demo.html
```

When using `git add`, changes are tracked in the staging area.
Think staging area as accepted changes. Next `git commit` will record all changes in staging area.

##### commit the staged changes
If omitting the `-m` flag, you will need to write the commit message in an editor.

You can [Change Editor](https://git-scm.com/book/eo/v1/Ekkomenci-First-Time-Git-Setup#Your-Editor).

> By default, Git uses your system’s default editor, which is generally Vi or Vim.
> If you want to use a different text editor, such as Emacs, you can do the following:
>
> `$ git config --global core.editor emacs`

```
$ git commit

(inside default editor)

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
# Changes to be committed:
# modified:   d3-demo.html
#
```

Puts commit message `created HTML template` in first line and save and exit.
For example, typing `:x` in normal mode in vim

> git works with changes, not files
> Git focuses on the changes to a file rather than the file itself.
> When you say git add file, you are not telling git to add the file to the repository. 
> Rather you are saying that git should make note of the current state of that file to be committed later.
        
### [View Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)

```
$ git log
commit 3958d73a146bce0af25fcec3781c724530875887 (HEAD -> master)
Author: pengzhengyi <zhengyi_peng@brown.edu>
Date:   Mon Apr 29 16:56:10 2019 -0400

    HTML template

commit b9b38b335a62cb70bd3681da7b536d66b39e9f7c
Author: pengzhengyi <zhengyi_peng@brown.edu>
Date:   Mon Apr 29 16:22:58 2019 -0400

    create target file
```

We can see the two commits made to this repository.
### create [alias](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases) (shorthand, abbreviations) for git commands

You can sepcify alias for git commands in `.gitconfig` file.  
Create a `.gitconfig` file in your $HOME directory to mak configuration global  
Alternatively, create a `.gitconfig` file in your current directory to make configuration local

Here is my `.gitconfig` file:
```txt
[color]
  branch = auto
  diff = auto
  status = auto
[color "branch"]
  current = yellow reverse
  local = yellow
  remote = green
[color "diff"]
  meta = yellow bold
  frag = magenta bold
  old = red bold
  new = green bold
[color "status"]
  added = yellow
  changed = green
  untracked = cyan
[filter "lfs"]
  clean = git-lfs clean -- %f
  smudge = git-lfs smudge -- %f
  process = git-lfs filter-process
  required = true
[user]
  name = <username>
  email = <email>
[pull]
  rebase = false
[alias]
  co = checkout
  ci = commit
  st = status
  br = branch
  hist = log --all --graph
  br = branch
  l = log --all --decorate --graph --pretty=oneline
  lv = log --all --decorate --graph --pretty=tformat:'commit: %C(bold red)%h%Creset %C(red)<%H>%Creset %C(bold magenta)%d %Creset%ndate: %C(bold yellow)%cd %Creset%C(yellow)%cr%Creset%nauthor: %C(bold blue)%an%Creset %C(blue)<%ae>%Creset%n%C(cyan)%s%n%Creset'
  type = cat-file -t
  dump = cat-file -p
  ignore = "!gi() { curl -L -s https://www.gitignore.io/api/$@ ;}; gi"
[core]
  autocrlf = false 
  safecrlf = false 
```

You can try `git lv` if you used the above configurations.
### Get history versions

What's a version control system good for if we cannot revert back to old versions?  
Luckily, git allows us to easily travel back and force in commit.
Think your commits as snapshots of the repository.

Using the `git log` command, you can find the hash for every commits. 
Think hash as identifier for each commit.  

Your hash might be different from what I have:
```
* 3958d73a146bce0af25fcec3781c724530875887 (HEAD -> master) HTML template
* b9b38b335a62cb70bd3681da7b536d66b39e9f7c create target file
```

```
$ git checkout b9b38b335a62cb70bd3681da7b536d66b39e9f7c
Note: checking out 'b9b38b335a62cb70bd3681da7b536d66b39e9f7c'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at b9b38b3 create target file
``` 

`git checkout <hash>`takes us back to the commit specified by the hash.

If you use `cat d3-demo.html`, you will find its an empty file as our first commit just creates this file.

If you have set the configuration, you can run `git lv`, otherwise run `git log --all --graph`

```txt
$ git lv
* commit: 3958d73 <3958d73a146bce0af25fcec3781c724530875887>  (master)
| date: Mon Apr 29 16:56:10 2019 -0400 44 minutes ago
| author: pengzhengyi <zhengyi_peng@brown.edu>
| HTML template
|
* commit: b9b38b3 <b9b38b335a62cb70bd3681da7b536d66b39e9f7c>  (HEAD)
  date: Mon Apr 29 16:22:58 2019 -0400 77 minutes ago
  author: pengzhengyi <zhengyi_peng@brown.edu>
  create target file
```

**HEAD** is where we are currently at, 
> master’ is the name of the default branch.
> By checking out a branch by name, you go to the latest version of that branch.

Use `git checkout master` to go back to latest commit.

### [Tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging) a commit
If you do not reference a commit by hash every time, you can tag it by a custom name.

Checkout the first commit and use `git tag initial` to tag the first commit as initial.

Now you can travel back and forth using `git checkout master` and `git checkout initial`  

Additionally, you can use `git tag` to view all defined tags.

### [Undoing Things](https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things)
##### [Unmodifying a Modified File](https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things#_unmodifying_a_modified_file)
First, go back to master version `git checkout master`.

If you run `git status`, git should report *working directory clean*.

Pretend we have made some unwanted changes which haven't not been staged (we have not run `git add`) yet.  
`echo "Unwanted Change" >> d3-demo.html`  
This command appends one line with string "Unwanted Change" to the end of the file.

When we run `git status` again, we will see d3-demo.html has been modified but changes have not been staged.

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

  modified:   d3-demo.html

no changes added to commit (use "git add" and/or "git commit -a")
```

As it suggests, we can use `git checkout d3-demo.html` to discard the changes we have made.  
You can confirm that the appended line has disappeared using `tail d3-demo.html`, a command to see the last lines of the file.

##### [Unstaging a Staged File](https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things#_unstaging)
Pretend we have made some unwanted changes and have staged these changes

```bash
$ echo "Unwanted Change" >> d3-demo.html
$ git add d3-demo.html
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

  modified:   d3-demo.html
```

Similarly, we can follow what the `git status` instructs us to do:  
`git reset HEAD d3-demo.html`  
Since we have checked out master branch, HEAD is equivalent to MASTER and refers to files in most recent commit.

However, we are not done yet, if you run `git status` again, you will find we end up in previous situation:
we have made some changes but have not staged these changes yet (the "Unwanted Change" line is still there).  
Run `git checkout d3-demo.html` to reset the file.

If it's okay to discard all changes (staged or unstaged), you can directly run `git checkout <hash>` to go back to a specific commit.
    
##### [Undoing  Committed Changes](http://gitimmersion.com/lab_16.html)
Pretend we have made some unwanted changes and have committed these changes

```bash
$ echo "Unwanted Change" >> d3-demo.html
$ git add d3-demo.html
$ git commit -m "unwanted changes committed"
```

To revert back, we basically create an overwriting commit.  
*You can achieve the same effect by remove unwanted changes, add the file, and commit.*  

`git revert HEAD --no-edit` 
> [git-revert](https://git-scm.com/docs/git-revert) revert the changes that the related patches introduce, and record some new commits that record them.
>
> git revert is used to record some new commits to reverse the effect of some earlier commits (often only a faulty one).
> If you want to throw away all uncommitted changes in your working directory, you should see git-reset[1], particularly the --hard option.
> If you want to extract specific files as they were in another commit, you should see git-checkout[1], specifically the git checkout <commit> -- <filename> syntax.
> Take care with these alternatives as both will discard uncommitted changes in your working directory.


### [Git Branching](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)
##### Creating A Branch
Typically, a stable version of an application is stored in the master branch. 
When we plan to make some changes, we open a new branch and store changes in the new branch.
By separating the development application and the deployment application (the stable version),
we can make changes without worrying about potentially damaging effects.

We can create a new branch using 
`git checkout -b <branchname>`

> The command is a shortcut for `git branch <branchname>` followed by a `git checkout <branchname>`.

##### Navigating Branches
You can use `git branch` to view all branches and use `git checkout <branchname>` to navigate around branches.

##### Merging Branches 

First, let us introduce a divergence -- we add a README in dev branch while make some changes to d3-demo.html in master branch.

+ changes in dev branch
  ```sh
  $ git checkout dev
  Switched to branch 'dev'
  $ echo "This is a sample project for D3 visualization" >> README.md
  $ ls
  README.md    d3-demo.html
  $ git add README.md
  $ git commit -m "Added README"
  ```

+ changes in master branch
  ```sh
  $ git checkout master
  Switched to branch 'master'
  $ ls
  d3-demo.html
  ```
  Then we add the link to latest d3 release in d3-demo.html, put it just after the body tag  
  `<script src="https://d3js.org/d3.v5.min.js"></script>`
  
  ```sh
  $ git add d3-demo.html
  $ git commit -m "include link to d3 script"
  ```

We can view the branches and how they diverge using  
```
$ git log --all --graph
* commit d3453f85b737c41d2d9cfd8399910d29fb5aa5b8 (HEAD -> master)
| Author: pengzhengyi <zhengyi_peng@brown.edu>
| Date:   Fri May 3 06:02:45 2019 -0400
|
|     include link to d3 script
|
| * commit 57a38abd6494fbeabc6e7461c15cbc02d182374a (dev)
|/  Author: pengzhengyi <zhengyi_peng@brown.edu>
|   Date:   Fri May 3 05:53:48 2019 -0400
|
|       Added README
|
* commit 808a90528cfe295eb7e44080712fccb778ee99f8
| Author: pengzhengyi <zhengyi_peng@brown.edu>
| Date:   Wed May 1 10:35:53 2019 -0400
|
|     HTML Template
|
* commit ee15e447dff6c40fa4cc5ccdf7075af27963b999 (tag: initial)
  Author: pengzhengyi <zhengyi_peng@brown.edu>
  Date:   Wed May 1 10:31:23 2019 -0400

      create target file
(END)
```

> The --all flag makes sure that we see all the branches. The default is to show only the current branch.  
> Adding the --graph option to git log causes it to draw the commit tree using simple ASCII characters. 

Often we want to merge the changes in master branch to our development branch so that the developemnt branch
is up to date with recent changes in master while keep its local changes unaffected.
Now both branches contain independent changes. We can merge the changes from the master branch by:
```
$ git checkout dev
$ git merge master
$ git log --all --graph
*   commit 25e554a9a199bd8a3bbc9167916b182d599e96be (HEAD -> dev)
|\  Merge: 57a38ab d3453f8
| | Author: pengzhengyi <zhengyi_peng@brown.edu>
| | Date:   Fri May 3 06:14:53 2019 -0400
| |
| |     Merge branch 'master' into dev
| |
| * commit d3453f85b737c41d2d9cfd8399910d29fb5aa5b8 (master)
| | Author: pengzhengyi <zhengyi_peng@brown.edu>
| | Date:   Fri May 3 06:02:45 2019 -0400
| |
| |     include link to d3 script
| |
* | commit 57a38abd6494fbeabc6e7461c15cbc02d182374a
|/  Author: pengzhengyi <zhengyi_peng@brown.edu>
|   Date:   Fri May 3 05:53:48 2019 -0400
|
|       Added README
|
* commit 808a90528cfe295eb7e44080712fccb778ee99f8
| Author: pengzhengyi <zhengyi_peng@brown.edu>
| Date:   Wed May 1 10:35:53 2019 -0400
|
|     HTML Template
|
* commit ee15e447dff6c40fa4cc5ccdf7075af27963b999 (tag: initial)
  Author: pengzhengyi <zhengyi_peng@brown.edu>
  Date:   Wed May 1 10:31:23 2019 -0400

      create target file
```

If we open the d3-demo.html, we can see changes from master branch is now included.
However, the new README.md in dev is not present if we switch to master branch.

Another way to achieve the same effect is using [rebase](https://git-scm.com/docs/git-rebase) command.
Instead of running `git merge master`, we will run `git rebase master` in dev branch.

> Merge VS Rebase
> 
> The final result of the rebase is very similar to the merge. The greet branch now contains all of its changes, as well as all the changes from the master branch. However, the commit tree is quite different. The commit tree for the greet branch has been rewritten so that the master branch is a part of the commit history. This leaves the chain of commits linear and much easier to read.
> 
> When to Rebase, When to Merge?
> 
> Don’t use rebase …
> 
> If the branch is public and shared with others. Rewriting publicly shared branches will tend to screw up other members of the team.
> When the exact history of the commit branch is important (since rebase rewrites the commit history).
> Given the above guidelines, I tend to use rebase for short-lived, local branches and merge for branches in the public repository.
> 

### Resolving Conflicts
Sadly, things do not always go smoothly. Conflicts arise when you are merging two branches with conflicting changes.

+ changes to dev branch
  + Checkout the dev branch. `git checkout dev`
  + We add a svg element to d3-demo.html immediately after the body tag.
  + Commit this change. `git add d3-demo.html` and `git commit -m "add svg element"`
+ changes to master branch
  + Checkout the master branch. `git checkout master`
  + We add a div element to d3-demo.html immediately after the body tag.
  + Commit this change. `git add d3-demo.html` and `git commit -m "add div element"`

If we try to merge two branches, we will get a merge conflict.
```sh
$ git checkout master
$ git merge dev
Auto-merging d3-demo.html
CONFLICT (content): Merge conflict in d3-demo.html
Automatic merge failed; fix conflicts and then commit the result.
```

If you open the d3-demo.html, it will look like:
```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  <title>CSCI1320: D3 Lecture Demo</title>
</head>
<body>
<<<<<<< HEAD
  <div>
  </div>
=======
  <svg>
  </svg>
>>>>>>> dev
  <script src="https://d3js.org/d3.v5.min.js"></script>
  <script>
  </script>
</body>
</html>
```

> The first section is the version on the head of the current branch (master). 
> The second section is the version on the dev branch.

We need to manually resolve the conflict. 
Some possible ways to resolve this conflict includes deleting one section and merging two sections.

For merging, we can modify the conflict part to be:
```html
<body>
  <div>
    <svg>
    </svg>
  </div>
  <script src="https://d3js.org/d3.v5.min.js"></script>
  <script>
  </script>
</body>
```

Then we can commit the conflict resolution by `git add d3-demo.html` and `git commit -m "nest svg element inside div element"`.

As it is a hassle to fix merge conflicts, it is preferable to avoid conflicts at the beginning.
This post gives out some [Recommendations to avoid merge conflicts](https://itnext.io/recommendations-to-avoid-merge-conflicts-845ec133676e)


# Thanks For Reading
