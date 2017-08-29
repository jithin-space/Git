# Git tutorial

This tutorial is all about exploring git from basics. It is intended only for learning purposes.

## 1. Chapter 1 - Getting Started

This chapter is intended to explain why you should learn git, where it is useful and essentially what is git.


## 1.1 Version Control Systems

> Version Control is a system that records changes to a file or set of files over time so that you can recall specific versions later.

###     * Local Version Control Systems

Originally we manually maintain specific versions of a file by simply copying it into another location. But it requires constant user intervention and maintanence. 

To deal with this issue programmers long ago developed a  local VCSs that had a simple `database` that kept all the changes to files under revision control. One of such popular VCS tools was a system called RCS.

RCS works by keeping patch sets (ie the difference between files) in a special format on a disk. It can then recreate any file looked like at any point in time by adding up all patches.

###      * Centarlized Version Control Systems

Another issue is that we need to collaborate with other developers working on other systems. To deal with this problem, Centralized version control systems developed. Eg. CVS,Subversion and Perforce.

They have a central server and a number of clients that check out files form that central place. The advantage of this mode of version control systems are 
    * Everyone knows to a certain degree what everyone else on the project is doing.
    * Administrators have fine grained control over who can do what.
    * It is easier to maintain than setting up individually each client as in LVCS

This method also has some serious drawbacks including
    * Single point of failure , lose of everything.
    * If proper backups are not taken, Both LVCS and CVCS lose everything.

### * Distributed Version Control Systems
    
Inorder to solve the problems addressed above, DVCS emerged. In these systems (like Git,Mercurial,Bazaar or Darcs), client don't just check out the latest snapshot of the files : they fully mirror the repository.

Thus if any server dies, any client repositories can be copied back up to the server to restore it. Every checkout is really a full back up of all the data.

These systems deal pretty well with having several remote repositories they can work with, so you can collaborate with different groups of people in different ways simultaneously within the same project.This allows you to set up several types of workflows that aren't possible in centralized systems.
 

## 1.2 Git History

In 2002, Linux kernel project began using a proprietary DVCS called BitKeeper. In 2005, their relationship broke down and tool's free-of-charge status revoked. Thus linux development community especially Linus Torvals, the creator of linux started to develop their own tools based on their experience in using BitKeeper.Thus git was born

## 1.3 Git Features
    * Simple
    * Speed
    * Strong support for non linear development.
    * Fully distributed
    * Ability to handle large projects. (Both speed and size handling)

## 1.4 Git Basics
    
Git works differently than other systems like subversion or perforce. Therefore it is essential to understand how it works eventhough they all provide similar functionality and interfaces.

    * Main difference is in how git think about its data. Conceptually ,most other systems store information as list of file based changes. They think of the information they keep as a set of files and changes made to each file over time.

    * Instead Git thinks of its data more like a set of snapshots of a miniature filesystem. Every time you commmit or save the state of your project in git, it basically takes a picture fo what all your file look like at that moment and stores a reference to that snapshot.

    * To be efficient , if the files have not changed,it doesnot store the file again, just a link to the previous identical file it has already stored.

#### * Git thinks about its data more like a stream of snapshots.

#### * nearly every operation is local

There a little set of operations that requires you to be online. Ie you can do alot of things even if you are not connected to the server.

#### * git has integrity

Everything in Git is check-summed before it is stored and is then referred to by that checksum. This means it is impossible to change the contents of any file or directory without Git knowing about it.

It uses SHA-1 hash. This is a 40 character string composed of hexadecimal characters and calculated based on the contents of a file or directory structure in Git. 

In fact, Git stores everything in its database not by file name but by the hash value of its contents.

#### * git generally only adds data

Every operation in Git only add data to the Git database. It is hard to get the system to do anything that is not undoable or to make it erase data in any way.


#### * The three states

In git there are three main states that your files can reside in.Commited,Staged and Modified. Commited means that the data is safely stored in your local database. Modified means that you have modified the file ,but have not commited it into your database yet. Staged means you have marked a modified file in its current version to go into your next commit snapshot.

Hence , we have also three main sections of a git project: the Git Directory, the Working Directory and the Staging Area.

Git directory is where git stores its meatadata and object database for your project. It is important to git, and it is what is copied when you clone a repository from another computer.

Working directory is a single checkout of one version of the project. These files are pulled out of the compressed database in the Git directory and placed on disk for you to use or modify.

Staging area is a file, generally contained in your git directory, that stores information about what will go into your next commit. It is sometimes refered to as the `index` but it is also common to refer to it as the staging area.

#### * Git Workflow
    1. You Modify files in your working directory.
    2. You stage the files, adding the snapshots of them to your staging area.
    3. You do a commit , which takes the files as they are in the staging area and stores that snapshot permanently to your Git Directory.

commit --- modify --- stage -- commit <loop>



		Installing git
			apt-get install git
		first time git setup
			local,global,system
			your identity
				git config --global user.name "jithin"
				git config --global user.email jithin@space-kerala.org
			your editor
				vim by default
				git config --global core.editor emacs
			list your settings
				git config --list
				repeated values seen, last value often taken
				git config user.name
			getting help
				git help verb
				git <verb> help
				man git-<verb>

chapter 2..Git Basics
	creating a git directory
		git init
	adding files to staging area
		git add <filename>
	commit to the repository
		git commit -m 'my initial commit'
	cloning an existing repository
		git clone http://url <new folder name>
	recording changes to the git repository
		untracked ( not in the last snapshot) and tracked
		untracked  not modified modified staged.
	checking the status of files
		git status
	staging modified files
		every modified files needs to be added to the staging state using
		git add command
		changes to be commited
		changes not staged for commit
	short status
		git status -s or --short
		two columns and filename
		?? untracked
		MM modified(staged) modified(non staged)
		A  added to staged
	ignoring files
		using .gitignore
		the file that need not be tracked and listed.
	view your staged and unstaged status
		git status
		see what you’ve changed but not yet staged,(non staged ---staged)
		 	git diff
		see what changes you commit ( staged to commit)
			git diff --staged
	committing your changes
		git commit
			def editor will pop up and  show how the commit should be stored
		git commit -v
	skipping the staging area
		git commit -a -m 'commiting without staging)
	removing files from git
		remove from git
			git rm <filename> remove from both git and working
			git commit
		remove only from git
			git rm --cached <filename>
			it will be then in untracked files
	moving files
		rename
		git mv abc.text cde.text
		git status
	viewing the commit history
		git log
		git log -p ( shows the difference induced in each commit)
		git log -2 ( last two commits)
		git log --stat
		git log --pretty=oneline
		limiting the length of log
			git log --since=2.months
			more options like --untill -S
	undoing things
		git commit --amend
		this command uses your current staging area and uses it for the commit
		eg git commit -m 'first'
		   git add forgotten.txt
		   git commit -amend -m 'first_replaced';
	unstaging a staged file
		reset back to staging after you add them to staging area
		git reset HEAD  tutorial.txt
		git status		
	unmodifying a modified file
		git checkout -- filename

	dealing with remote repositories
		git clone http://github.com/someproject/tcp
		cd tcp
		git remote ---------------shows origin--default server name
		git removte -v
			shows origin http://github.com/someproject/tcp
		if we have more contributors and remotes
			it will list all 
		adding remote repository
			git remote add <short-name> url
		using that contribution
			git fetch <short-name>
		fetching and pulling from remotes
			fetch --means get the data from remote not merge to your current working directory---have to merge manually
	
			pull --get the data and automatically merges 
			git fetch origin..get the latest updates from the remote server since you have cloned or last fetched.
			git pull origin..get and merge

If you have a branch set up to track a remote branch you can use the git pull command to automatically fetch and then merge a remote branch into your current branch.

by default, the git clone command automatically
sets up your local master branch to track the remote master branch (or whatever the default branch is called) on the
server you cloned from. (git pull )

	pushing to your remotes
		git push <remote-name> <branch-name>
		git push origin master
		** works if you cloned from a remote server having write acess and nobody pushed during the meantime
	**two points skipped on remote..


Tagging..
-------------------
	listing tags
		git tag
	serch for tags
		git tag -l 'abc*'
	creating tags
		two type..lightweight and annotated..
		git tag -a v1.0 -m 'message1'
		git show v1.0
	lightweight tag
		git tag v3.0
		git show v3.0 ( only commited info..no tagger info)
	git tagging later
		git log --pretty=oneline
		git tag -a v0.0 5117 <part> -m 'message'
	sharing tags
		tags not loaded to server on push
		git push origin v1.0
		git push origin --tags <for all tags created>
	git aliases
		creating aliases for git commands
		git config --global alias.ci commit
		git ci
	
conflict resolved	

Git Branching
--------------------------
	create a new branch
		git branch testing
	switching branches
		git checkout testing
	for viewing all commits including other branches
		git log --oneline --decorate --graph --all
	creating and switching at the same time
		git checkout -b testing
	simple merge
		git merge testing ( while on master)
		simple moves the head ptr to next
	three way merge
		merge point..current head point ...common ancestor
	basic merge conflicts
		git merge testing
		git status (if conflicts)
		git add conflict_file ( add to staging )
		open the file (special indication)
		manually resolve
		git commit 
	branch management
		git branch (list all)
		git branch -v (list all with last commits on each brach)
		git branch --merged (and --non-merged)
		git branch -d testing (delete testing)
	branching workflows
	Remote branches
		no server interaction all this time
		each brach has a remote brach when it last commuicated.it is immutable ...named remote/branch
		git fetch origin (loads remote/origin to our repo not merge)
		useful when using multiple remotes ( git fetch remote2)
	pushing
		git push remote brach
		git push remote localbranchname:remotebranchname
		
	tracking branches
		checking out a localbranch from a remote branch creates
		tracking branches or upstream branches
		git checkout --track origin/serverfix
		git branch -u origin/serverfix (--set-upstream ,specify explicitely)
		@u shortand for upstream ( git merge @u / origin/master)
		git branch -vv ( for viewing tracking branch details)
		(ahead and behind )
		get current updation git fetch --all
	pulling
		fetch + merge = pull
	delete a remote branch
		git push origin --delete serverfix
	Rebasing
		merge or rebase
		take the patch on a branch and reapply it on other branch
		rebasing is for a cleaner history ( looks linear)
Git Server
	we can serve git server 
	locally
	ssh
	http/https
	git protocols
	pros and cons of each is discussed in the book...
		
		
		
		
		
	
		
	
