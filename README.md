# git tutorial

This tutorial is all about exploring git from basics. It is intended only for learning purposes.

## 1. Chapter 1 - Getting Started

This chapter is intended to explain why you should learn git, where it is useful and essentially what is git.


#About version control systems

	#Local Version Control Systems
	Centralized Version Control Systems
	Distributed Version Control Systems
short history of git
git basics
	snapshots not differences
	nearly every operation is local
	git has integrity
	git generally only adds data
	The three states
		commited,staged,modified
		repository,staging area, working directory
	The Command Line
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
		
		
		
		
		
	
		
	
