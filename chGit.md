# HOW TO GIT

## SMR
 [Base cmds](#base-commands)
 [Branches](#branches)
 [Turning back](#turn-back)
 [GITFLOW](#gitflow)    

## Base commands
- git init
creates local git repo at current location

- git remote
to set links between local and remote repos
git remote add [name][link]
git remote add upstream[link]

git remote -v

- git add
select files for staging

- git pull (fromwho)(towhichbranch)
retrieve state of source to keep up to date AND **merges it to the workspace**
##### options:
    - **merge** : combines both the origin and the local histories, keeping both fully BUT will create a merge commit which muddies up the LOGS
    - **rebase** : MOVES the child branch to now start where the modified main branch ends, all commit history of main now incorporated into CHILDBRANCH as it gets rewritten. it makes cleaner linear logs. //!\\ it needs to be done CLEANLY else it will completely muddy up the collaborative history.


- git commit -m "message following convention"
finalises the changes added to the staging

- git push (towhom)(whichbranch)
feeds the commits to the source

## BRANCHES  

- git checkout -b [branchname]
Moves to a branch, creating it if it doesn't exist.

- git merge [branchname]
Merges the modifications of the branch onto the main branch.

**fast forward** is an option --ff or --no-ff, it also merges the history of two branches that have no divergeant history changes in between the [ftbranch] and [mainbranch], simplifying the project history. 

- git branch -d [branchname]
deletes a branch

## TURN BACK

### Git reset
Hard "turn back" on a small scale. 
    - Discards commits
    - Throws away uncommited edits
    - Unstages a file in staging area

--soft -> doesnt touch the staging and working areas
--mixed -> no reset of the working dir, but staged files are aligned to the commit being reset to
--hard -> everything is updated to be aligned to the commit being reset to

### Git revert
Soft "turn back" useful for public branches.
    - creates a new commit that indicates the "turn back"

### Git checkout
Inspection tool for commits + discards edits on file level

RESET + CHECKOUT on whole commit by default, need parametres to specify smaller scales.
REVERT only applies to commits, not files, thus needs no specifying parametre.


## GITFLOW

Gitflow is a tool that streamlines the project workflow.

- git flow init
alike git init, but includes settings specifics to git flow, definable on init
Upon init, it'll ask for names of different branch types (feature, bugfix, etc) which can be used later to create clean branches, readable in the logs.

- git flow [branchtype] start [NAME]
will create a branch of a set type under the registered name and move to it as working branch.

- git flow [branchtype] finish [NAME]
merges back into the main (develop) branch, deletes the [NAME] branch, and switches to develop.

- git flow [branchtype] publish [NAME]
sends the branch onto the remote server to be accessed by other collaborators

- git flow [branchtype] pull origin [NAME]
grabs a branch published by a collaborator to be on your local

- git flow [branchtype] track [NAME]
tracks a branch on origin

