============
Git & GitHub
============


===============
Version control
===============

--------------------
Why version control?
--------------------

Until now you have worked on small one, maybe two-person projects.
Managing your project that way is not too difficult - just keep it in some 
directory and keep adding changes.

But what if there are two people on the project? If multiple people write new 
code in their own versions, how do you put it together? You could send the 
changes by email, but that scales really badly and is a pain in the ass even 
for a two-member team.

----------
What is it
----------

A version control system is a program that allows multiple people to work on 
the same project and add changes to it, while keeping track of those changes 
over the project's history. Changes in the project's history can also be undone.

Historically, version control systems were centralized - there was one VCS 
server and each team member would use the VCS to synchronize with other members'
changes, and to upload ("commit") their own changes.

This created its own set of problems. 


Let's say Vlado and Robo both
work on a game project called Mafia, but Vlado works on the scripting
system, while Robo works on a better renderer. Both of them work simultaneously
and their commits interleave. Let's say Vlado finds he frakked up 5 commits ago.
Now if he wants to undo that, he needs to also undo Robo's commits. Robo won't
be pleased.

If Vlado wants to commit something while he's commuting to the daily bad guys' 
meeting, tough luck. He needs an internet connection to do that. He'll only
be able to commit once he gets home, and by that time he might have more 
unrelated changes that won't make much sense in a single commit.

If Robo wants to do something experimental in private until he's certain he can 
show it to Vlado, he can't use the VCS for that.

If the main server has a hard drive failure, FUUUUU....


----------------------
Some centralized VCS's
----------------------

* RCS - Ancient history
* CVS - Something like COBOL
* SVN - CVS done not quite as horribly
* Perforce - Pay for a VCS? Windows Text File?


===========================
Distributed version control
===========================

In distributed version control, there is no such thing as a central server.
Every team member has their own VCS repository and they can perform any 
operations, e.g. commits, on their own machine. These are then usually 
synchronized with some "main project repository", although that is not required.

When you add changes in a DVCS, you commit to a repository on your own machine.
You can then "push" those changes to a remote repository and, similarly, "pull"
other peoples' changes. You don't need an internet connection to commit, and you
can do experimental changes, even rewrite history, before you push to the 
outside world.
You can also work on your own changes without intefering with other people's 
commits, freely undo them, and only push once the feature is complete.


-------------
DVCS approach
-------------

The ability to commit without working with a central server leads to a
completely different philosophy. Commits are frozen states when your code works,
and you can return to them and undo them. You can think of them as of game 
saves. Since you don't need to connect to a server, you don't need to commit 
all changes at once. 

The DVCS philosophy is to keep commits as small as possible, but indivisible. 
The project should always work after a commit. If you added a new, 1000-line 
class *NewWorldOrder*, and for that class, you improved a 5-line utility 
function *loveAndPeace()*, which is used by *NewWorldOrder*, but independent,
you commit *loveAndPeace()* first and then you commit *NewWorldOrder* 
separately. It might make sense to undo *NewWorldOrder* without undoing 
*loveAndPeace()*.

Note that each commit should represent a **stable** snapshot of your program.
It is a good idea to review all changes ("diffs") in a you're about to commit 
right before committing. It is also a good idea to review changes in other 
team members' commits to find bugs. Hosting services such as GitHub make this
easy.


----------------------
Some distributed VCS's
----------------------
* Git - Most popular and powerful, very fast, hardest to use. The Future.
* Mercurial - Second most popular (by a large margin). Not so fast or powerful, easier to use.
* Bazaar - Similar to Mercurial, even easier to use. Mostly Ubuntu projects.
* Darcs - Not very successful, might be more popular in future.


===
Git
===

Git is the most commonly used DVCS that is currently steamrolling SVN in the 
open source community and also making inroads into corporate environments.
Compared to other distributed VCS's, it's not quite as easy to use, but not too
hard either. That said, even if you prefer, say, Mercurial or Bazaar, Git is 
almost certainly what you'll end up using in practice.

Git is *extremely* powerful. If you can think of any obscure VCS feature, Git 
can almost certainly do it, and it can do a lot of things nothing else can do.
(It was written by Linus Torvalds, duh).


------
GitHub
------
GitHub is a site that hosts Git repositories. It provides a user-friendly 
interface to a hosted Git repository. Users can browse source files, view 
project history, upload downloadable files, view code statistics and so on.
It also provides some nice features on top of Git, such as pull requests. 
GitHub is free for open source projects. Proprietary projects must pay for 
hosting.

GitHub is not the only such hosting site. Similar, but less popular, is 
Gitorious. Other Git hosting sites include Bitbucket, repo.or.cz, SourceForge 
and many more.


------------------
Using Git & GitHub
------------------

First, you need a GitHub account.
Go to `GitHub <http://github.com>`_, click *Signup and Pricing* and then click 
*Create a free account*.

Do the usual stuff you do when you create an account somewhere.


`Set up Git with GitHub <help.gihub.com/set-up-git-redirect/>`_
`Create a Repository <help.gihub.com/create-a-repo/>`_

The Windows Git package contains a nice minimalistic GUI::

   Start -> All Programs -> Git -> Git GUI 

On Debianoid Linuxes, we can use *git-cola*::
    
   sudo apt-get install git-cola 

Note that neither of these is the "best" Git GUI. However, they both are 
minimalistic and easy to use.


Try doing stuff with the GUI:

* Adding, staging and committing:

  **Git-GUI**

  Click at an icon left of a file in *Unstaged Changes* to stage it.

  **Git-Cola**

  Select files to stage, right click, and click *Stage Selected*.

  **Both**

  Using this, you can split changes into multiple commits.

  Create or change some files and commit them in separate commits,
  bu first staging some files, clicking commit, then other files,
  and clicking commit again.

 
* Amending last commit 

  Click *Amend Last Commit* to add some more changes to the last commit.  

* Viewing history:

  **Git-GUI**::

     Repository -> Visualize master's history

  **Git-Cola**::

     Branch -> Visualize Current Branch ...

* Ignoring files:

  You might have various files in your directory that you never want to commit.
  To make git ignore those files, create a file called ``.gitignore``.
  Every line in that file is a file name or file name pattern to ignore.

  Example .gitignore::

     *.sw*
     *.sv*
     *~
     dsss.last
     dsss_objs/
     ice-debug
     ice-no-contracts
     ice-release
     wrapper
     glxtrace.so
     oprofile/
     user_data/main/screenshots/
     user_data/main/logs/
     cdc
     *.out
     *.o
     *.tbp.dir
     *.ebp.dir
     *.caw
     *.bkp

  Among others, this ignores a directory called ``oprofile/``, a file called 
  ``ice-debug`` and any file with the ``.bkp`` extension.
  
* Stashing:
   
  Let's say you're in the middle of working on Feature A.
  Suddenly, for some reason, you need to immediately fix bug B.
  Your repository is a work-in-progress that you cannot commit.

  Stashing solves exactly this kind of problem.

  The ``git stash`` command resets the repository to the last commit and
  "stashes away" your changes since then.

  This allows you to fix Bug B without interfering with Feature A.

  Once you fix the bug, you can use the ``git stash pop`` command to restore 
  your work on Feature A, and continue working on it. 

  How to do this:

  **Git-GUI**::

     //Setting up a GUI command
     Tools -> Add... -> enter "stash" as name, "git stash" as command
     Tools -> Add... -> enter "unstash" as name, "git stash pop" as command
     //Stashing 
     Tools -> stash
     //Unstashing
     Tools -> unstash

  **Git-Cola**::
     
     //Stashing
     Stash... -> Save
     //Unstashing
     Stash... -> select stash to apply -> Apply

GitHub forks:

`Fork a Repository <help.gihub.com/fork-a-repo/>`_

.. especially try updating from upstream
.. and maybe a pull request
.. mention branches and submodules, don't show them
