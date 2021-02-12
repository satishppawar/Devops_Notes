# ﻿Git Basics

Reference ==> https://juristr.com/blog/2013/04/git-explained/
---------------------
1) Introduction
* Git stores everything in its database not by file name but by the hash value of its contents.
* Git has three main states that your files can reside in: `committed, modified, and staged:`
> Committed means that the data is safely stored in your local database. </br>
> Modified means that you have changed the file but have not committed it to your database yet.</br>
> Staged means that you have marked a modified file in its current version to go into your next commit snapshot.</br>

	Working Directory <=======> Staging Area <========> Git Directory

* Git directory is where Git stores the metadata and object database for your project
	
* The working tree is a single checkout of one version of the project. These files are pulled out of the compressed database in the Git directory and placed on disk for you to use or modify.

* The staging area is a file, generally contained in your Git directory, that stores information about what will go into your next commit. Its technical name in Git parlance is the “index”, but the phrase “staging area” works just as well.

---------
2) Git Data structure 

- Git uses trees and blobs with Key-Value pairs. 

A) Git Internals - Git Objects
-------------------
- Git is a content-addressable filesystem. 
- at the core of Git is a simple key-value data store. 
- on insert operation Git will hand you back a unique key you can use later to retrieve that content.
- COMMANDS	

```$git init test
$cd test
$find .git/objects
$find .git/objects -type f
$echo 'test content'| git hash-object -w --stdin
```

- git hash-object Git will hand you back a unique key you can use later to retrieve that content.
> The -w option then tells the command to not simply return the key, but to write that object to the database. 
> Finally, the --stdin option tells git hash-object to get the content to be processed from stdin; otherwise, the command would expect a filename argument at the end of the command containing the content to be used. 				
		
		COMMANDS
		-------------
		 $find .git/objects -type f
			
			.git/objects/d6/70460b4b4aece5915caf5c68d12f560a9fe3e4
	
		 $find .git/objects -type f .git/objects/d6/70460b4b4aece5915caf5c68d12f560a9fe3e4

		a. Create & save file to git object db
			$ echo 'version 1' > test.txt
			$ git hash-object -w test.txt
				83baae61804e65cc73a7201a7252750c76066a30

		b. Update the file content and save to git object db
			$ echo 'version 2' > test.txt
			$ git hash-object -w test.txt
				1f7a7a472abf3dd9643fd615f6da379c4acb3e3a

		c. Check the versions of the file
			$ find .git/objects -type f
				.git/objects/1f/7a7a472abf3dd9643fd615f6da379c4acb3e3a
				.git/objects/83/baae61804e65cc73a7201a7252750c76066a30
				.git/objects/d6/70460b4b4aece5915caf5c68d12f560a9fe3e4

		d. delete your local copy of that test.txt file, then use Git to retrieve, from the object database,
			$ git cat-file -p 83baae61804e65cc73a7201a7252750c76066a30 > test.txt
			$ cat test.txt
				version 1

			or the second version:

			$ git cat-file -p 1f7a7a472abf3dd9643fd615f6da379c4acb3e3a > test.txt
			$ cat test.txt
				version 2

		e. Retrieving the object type using "git cat-file -t"
			$ git cat-file -t 1f7a7a472abf3dd9643fd615f6da379c4acb3e3a
				blob

		   Note : 
			-------------
			  1. blob
			-------------  
				you aren’t storing the filename in your system —- just the content. 
				This object type is called a blob. 

	------------------
	B) Tree Objects
	---------------------
	- Tree objects in Git solves the problem of storing the filename and also allows you to store a group of files together.
	- All the content is stored as tree and blob objects, with trees corresponding to UNIX directory entries 
	  and blobs corresponding more or less to inodes or file contents. 
	
	- A single tree object contains one or more tree entries, each of which contains a SHA-1 pointer to a blob or subtree with its associated mode, type, and filename.

----

GIT First Time Set Up
-------------------------
git config :- This is utility used for git configuration

1. /etc/gitconfig file :- files storing git config for every user on system

	COMMAND :- git config --system

2. ~/.gitconfig or ~/.config/git/config : user specific git configuration

	COMMAND :- git config --global

3. config :- specific to single repository
	
	COMMAND :- git config --local

=============================================
Your Identity configuration
-----------------------------
COMMANDS:
	1. $git config --global user.name "<userName>"
	2. $git config --global user.email <emailId>

NOTE:
	1. you need to do this only once if you pass the --global option, 
	   because then Git will always use that information for anything you do on that system.
	   If you want to override this with a different name or email address for specific projects, 
	 you can run the command without the --global option when you’re in that project.

========================================
Your Editor
-------------------
$git config --global core.editor 

========================================
Checking Your Settings
-----------------------------
$git config --list

	 
=================================================================
2.1 Git Basics - Getting a Git Repository
==========================================
Contents
-------------
1. to configure and initialize a repository
2. begin and stop tracking files
3. stage and commit changes
4. set up Git to ignore certain files and file patterns
5. how to undo mistakes quickly and easily, 
6. how to browse the history of your project 
7. view changes between commits, and how to push and pull from remote repositories.


----------------------------------------
1. to configure and initialize a repository
--------------------------------------------
Two ways
	 a) by Initializing Existing project directory as a git repository 
	 b) By Cloning an Existing Repository
 
a) by making local project directory as a git repository
-----------------------------------------------------------
1. go to project directory
2. COMMAND : git init

3. Add the files to staging 
	COMMAND : git add <file names>

4. then perform the commit to the repository
	COMMAND : git commit -m "<Commit message>"



 b) By Cloning an Existing Repository
----------------------------------------

Get the copy of the  Git repository locally 
COMMAND : - git clone <remote repo URL>

==========================================================================
2. Recording Changes to the Repository
==================================================
each file in your working directory can be in one of two states: tracked or untracked. 

Tracked :- Tracked files are files that were in the last snapshot; they can be unmodified, modified, or staged. In short, tracked files are files that Git knows about.

Untracked files are everything else — any files in your working directory that were not in your last snapshot and are not in your staging area. 

Checking the Status of Your Files
------------------------------------
COMMAND :- git status


Create a new file and it will untracked because its latest contents are not present in the current snapshot of the Git
 
Tracking New Files
-------------------
To make a file ready to commit it must be added to staging area
To do so one need to run follwing command
	git add <file-name>
The git add command takes a path name for either a file or a directory; if it’s a directory, the command adds all the files in that directory recursively.

If you modify a file after you run git add, you have to run git add again to stage the latest version of the file

-------------------------
Short Status ( git status -s or git status --short)
---------------------------
Git also has a short status flag so you can see your changes in a more compact way. If you run git status -s or git status --short

you get a far more simplified output from the command:

$ git status -s
 M README
MM Rakefile
A  lib/git.rb
M  lib/simplegit.rb
?? LICENSE.txt


A --> Added to the staging area 
?? --> not tracked yet
M --> Modified but not tracked in staging area
MM --> Modified and tracked in staging area

===========================================================================
Ignoring Files
----------------------



Fetching and Pulling from Your Remotes
---------------------------------------
1. git fetch :- only downloads the data to your local repository — it doesn’t automatically merge it with any of your work 
		or modify what you’re currently working on.

2. git clone :- command automatically sets up your local master branch to track the remote master branch
		(or whatever the default branch is called) on the server you cloned from. 
		
3. git pull :- generally fetches data from the server you originally cloned from and 
	       automatically tries to merge it into the code you’re currently working on.
		git pull command to automatically fetch and then merge that remote branch into your current branch.

--------------------------------------------------------------------------
Pushing to Your Remotes
--------------------------------
$ git push origin master

---------------------------------------
Inspecting a Remote
--------------------------------------
$ git remote show origin



--------------------------------------------
Renaming and Removing Remotes
--------------------------------------------
$ git remote rename pb paul
$ git remote

you can either use git remote remove or git remote rm:

$ git remote remove paul
$ git remote
origin
==============================================================
Combining the branches
-----------------------
1. using git merge

2. using git rebase

