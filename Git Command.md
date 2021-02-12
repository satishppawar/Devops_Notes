# CONTENTS
--------------
A) GIT CONFIGURATION

B) WORKING LOCALLY WITH GIT
- creating local repo
- Adding files
- commiting changes
- Viewing history
- Viewing a diff
- Working copy, staging and repository
- Deleting files
- Cleaning working copy
- ignoring files with .gitignore

-----

A) GIT CONFIGURATION
  
1. System Level
> git config --system & /etc/gitconfig

2. User level
> git config --global #located in ~/.gitconfig

3. Repository level
> git config #located in .git

4. git config --global --list

5. git config --global user.name "Sam"

6. git config --global user.email "pawar.satish2345@gmail.com"

7. git config --global --list

8. git config --global help.autocorrect 1
> performs the autocorrect option on git

9. git config --global color.ui auto

10. git config --global core.autocrlf 

> autocrlf -> carrier return line feed. 3 values
		true (Use for windows) -> CRLF(Windows) to SLF (Repository) on text files
		false (Windows only)-> not used with cross plaforms.Uses CRLF only
		input (Linux and Mac)-> Convert CRLF
		

git config --global --list
or cat ~/.gitconfig

> Note :- User level settings overwrite the System level config
	and repository level settings overwrite the User level config

git config user.name "Sam"
git config --list

-----

## Unsetting the config
-----

- git config core.autocrlf true

a) USING git config --unset
 git config --unset core.autocrlf 

b) By EDITING config files directly
	e.g vim ./git/config

----

B) WORKING LOCALLY WITH GIT
-------

### creating local repository, Adding files and commiting changes

1. INITIALIZING DIRECTORY AS A GIT repository
> git init

2. Adding files to git staging

```
ls -la
echo "Hello,Git" > readme.txt
git status
git add readme.txt
git status
```

3. Commit the changes

 `git commit`

4. git log

5. Update file readme.txt by Adding 2nd line as hello again
	
6. Updated changes to the file in git repository only

```
git add -u #not valid for adding new file from staging area to git repo
git status

```

------
### Viewing history and diffs
----------------------------------------------------------
1. git log
> two commits in reverse chronological order i.e. recent at top and latter at bottom

2. Usinfg git diff

```
git diff <latter commit>..<recent commit>
git diff HEAD~1..HEAD
git diff HEAD~1  (2nd commit is referred as HEAD by default)
```

3. LATEST commit is referred as HEAD in git
> One commit back from latest commit is  HEAD~1

4. Adding All files
```
git add -A
git commit -m "Added cool new feature"

```

5. Git diff HEAD~1

-----
### Staging changes as multiple commits
------

1. Update file1.txt and readme.txt
   There are 2 changes

git add file1.txt
git commit "fixed bug*1234"

git add readme.txt
git commit -m "Fixed typo in readme.txt added additional information about other features"


### Deleting and renaming files
------------------------------------------------
1. Remove file from disk

```
rm file2.txt
git status
````

2. Staging removed files

```
git add -u
git status
```

3. Perform another operations

```
git add file3.txt
git status
```

4. Rename the file

```
mv file1.txt new_file_name.txt
git status
git add -A
git commit -m "reorganized the feature"
git log
```

----
### Undoing changes to the working copy
---------------------------------------
1. Open readme.txt and delete everything from it

```
git status
```

2. to undo deleted changes checkout changes from repo

```
git checkout readme.txt
git status
cat readme.txt
```

3. Open readme.txt and delete eveything from it

```
remove new_file_name.txt
vim readme.txt
rm new_file_name.txt
git status

```

4. performing git reset to redo on multiple changes

```
git reset --hard
git status

```

-----
### Undoing/redoing changes in the repository
-------------------------------------------
git log

git rest --soft HEAD~1

git status

git commit -m "Reorganised files for feature"

git log

git reset --hard HEAD~1

git status


-----
### Cleaning the working copy
----------------------------------------
1. Create a temp files

```
touch temp1.txt temp2.txt
git status
```

2. clear new files

```
git clean -n
git clean -f
git status
```

-----
### Ignoring files with .gitignore
-----------------------------------------

1. Consider that you have a log directory

```
mkdir logs
touch logs/log.txt
git status
```


2. Logs changes over the time and we do not need these changes
	
3. create a gitignore and add entries of files to be ignores

```
vim .gitignore
/log/*txt

```

4. Commit gitignore

```
git add .gitignore
git commit -m "Added .gitignore"
```

> Happy Learning :)
