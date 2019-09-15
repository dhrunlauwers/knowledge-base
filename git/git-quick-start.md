# Linux Academy: Git Quick-Start

## Introduction and Architecture
The git program is a source control tool created by Linus Torvalds.
	
Git manages content snapshots, checksums, and metadata to keep track of changes in files.
	
Some basic terminology:
- Each state (change) is known as a **commit**
- The current commit is known as the **head** 
	- The commit we are actively working on
- Commits are affiliated with **repositories** and **branches**
- The head may be moved between commits
	
	


## Install and Configure Git
Install using the following commands.
>sudo apt-get install git*	- On Linux
Google and install Git Bash -	On Windows

Git configuration may be managed using git config
> *git config --global user.name \<username>*	
- Useful for identification when doing source control
>*git config --global user.email \<email_addr>*
-	Useful for identification when doing source control
>*git config --system core.editor vim*
- Useful when you prefer using a particular text editor by default

Alternatively, you may assign system-wide configurations in the config files
* *etc/gitconfig* | corresponds to --system
* *~/gitconfig* OR *~/.config/git/config* | corresponds to --global
* *.git/config* | in a repository corresponds to --local


## Working with Repositories in Git
A repository is a collection of content related to a specific purpose or project.
>*git init \<repo-directory>* 
- Create or 'initialize' a new repository in the specific directory
- Creates a .git directory in the repository used for git metadata
>*git add \<filename>*
- Used to indicate relevant files for tracking in the repository
>*git add .*
- Track everything in current working directory
>*git rm \<filename>*
- Remove tracking from specific files
>*git status*
- Obtain tracking information on files
>*git commit -m "text describing changes"*
- Commit or update the change in the repository
>*git commit -a -m "text describing changes"*
- Automatically picks up all untracked changes in the commit (shortcut so you can skip *git add \<filename>*


## Managing What is Tracked with .gitignore
Sometimes there are artifacts in your project which are transient or do not otherwise need to be tracked in source code. There is a mechanism to have certain files disregarded for source control purposes.

The file .gitignore (local to a repository or system global) may contain a list of file names or patterns which git will ignore.

Create the .gitignore file and enter a file name, file pattern or directory:
>*nano .gitignore*
*pic.jpg*
*.jpg*
*temp/*

It's best practice to track your .gitignore file in the repository with the source code

It's also possible to exclude certain paths using the following command:
>*git config --global core.excludesfile \<path>*


## Cloning Repositories
Typically, the repository of record is not used for 'working' purposes. Changes to source are managed either in a separate branch or a remote repository.

Cloning repositories allows you to copy an existing repository to a new location. 
>*git clone \<path_of_original> \<clone_repo_location>*
- Cloning in the local file system
>*git / systemuser@hostname:\<orig_repo_path_relative_to_user_home> / <local_repo_path>*
- Cloning over SSH
>*git clone https://github.com/username/reponame \<local_repo_path>*
- Cloning over HTTPS (GitHub)

When cloning from GitHub, the git config will keep track of the origin url and master branch to be used when pushing changes. Check it out with 
>*git config -l*

The cloned repository keeps repository logs separately, making the origin repository log less cluttered.

After local work is complete, the changes may be pushed back to the origin repository using the following command:
>*git push origin master*

Branching achieves a similar effect within a single repository (more information in branching section).


## Understanding Git Logging
Git logs keep track of all commits in sequence. Use the following command to print information regarding commits and changes within the repository:
>*git log*
- Regular log
>*git log --oneline*
- Abbreviated log
>*git log -p*
- Detailed log
>*git log -- \<filename>*
- Log for a single file
>*git log --oneline \<filename>*
- Abbreviated log for a single file
>*git log --graph --decorate*
- Graphical representation of commit history (pipe diagram)

**Tip:** use forward slash '/' to search git log

## Working with Branches in Git
Branching allows you to create an effective copy of the master branch within the repository that can be worked on without interfering with the master. This declutters the master branch.

Branches can be merged back into the master branch when work is complete
>*git branch \<new branch>*
- Create a new branch
>*git checkout \<branch>*
- Begin working with a new branch
>*git checkout -b \<new branch>*
- Create a new branch and begin working with it


## Merging and Pushing Changes in Git
Branches may be pushed to remote sources, just like master. Remote sources are logged in git config. If you cloned a repository, the origin represents the original repository.
>*git push origin --all*
- Push branches to origin
>*git push origin \<branch>*
- Pushes specific branch to origin
>*git merge \<target branch>*
-	Merge to bring branches together

Merging branches where files may have changed in diverging ways is called a merge conflict. Start by checking out the branch you want to merge into, and then use git merge to merge another branch in.