# HOW TO GIT

## SMR
- [Base cmds](#base-commands)  
- [Branches](#branches)  
- [Turning back](#turn-back)  
- [Git Log](#git-log)  
    - [Report size](#detailing-the-reports)  
    - [Filtering](#filtering)  
    - [File history](#history-of-a-file)  
- [GITFLOW](#gitflow)    
- [GitCLI](#gitcli)

## Base commands
- git init
creates local git repo at current location
___

- git remote
to set links between local and remote repos
git remote add [name][link]
git remote add upstream[link]
___

git remote -v
___

- git add
select files for staging
____

- git pull (fromwho)(towhichbranch)
retrieve state of source to keep up to date AND **merges it to the workspace**
##### options:
- **merge** : combines both the origin and the local histories, keeping both fully BUT will create a merge commit which muddies up the LOGS

- **rebase** : MOVES the child branch to now start where the modified main branch ends, all commit history of main now incorporated into CHILDBRANCH as it gets rewritten. it makes cleaner linear logs. //!\\ it needs to be done CLEANLY else it will completely muddy up the collaborative history.
___


- git commit -m "message following convention"
finalises the changes added to the staging
____

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

#### Git bisect
when a bug has been introduced but its original commit is unknown, bisect allows to automate a binary process instead of linearly having to test back one by one.

Binary process:  
in a  
**0->1->2->3->4->5->6->7->CURRENT**  
chain of commits where 0 is a known non-bugged version, running bisect will checkout the middle point of the commit history (in this case, commit4). Running tests, we can then tell bisect whether commit4 is _GOOD_ (doesn't feature the bug/searchedfor feature) or _BAD_ (contains it), meaning respectively the OG introduction commit is later or sooner in the chain.  
When _GOOD_, it'll then move to the middle point of the forward section, between **4-----CURRENT**. When BAD, it'll move to the midpoint between **0--------4**, respectively c6 and c2.  The process will repeat, until identifying which commit introduced the bug/searchedfor feature.  

##### in practice:
```
git bisect start KNOWN-BAD-COMMIT KNOWN-GOOD-COMMIT
```
starts up the process, defining the entry and closing point on the commit history.

```
git bisect bad/good
```
tells bisect whether a checkout-ed commit it provided is GOOD or BAD.

```
git bisect log
```
provides log of the commits checked so far, indicating if they were 'run' (checked out), and/or marked as good/bad, and thus the earliest found BAD commit

```
git bisect reset HEAD
```
when checking out the earliest found BAD commit, will end bisect checked out on it instead of reverting to the latest commit on MAIN

#### Git reset
Hard "turn back" on a small scale.  
    - Discards commits  
    - Throws away uncommited edits  
    - Unstages a file in staging area  

- --soft -> doesnt touch the staging and working areas
- --mixed -> no reset of the working dir, but staged files are aligned to the commit being reset to
- --hard -> everything is updated to be aligned to the commit being reset to

#### Git revert
Soft "turn back" useful for public branches.  
    - creates a new commit that indicates the "turn back"

#### Git checkout
Inspection tool for commits + discards edits on file level

RESET + CHECKOUT on whole commit by default, need parametres to specify smaller scales.
REVERT only applies to commits, not files, thus needs no specifying parametre.

## Git Log

Displays commit history

### Detailing the reports
#### --stat 
will also display the amt of edits per commit, in numbers of deletions and insertions (++++++---), + amt of files changed

#### -p
will display the actual changes within the files.

### Filtering
 
#### --after= --before=  
sets date (YYYY/MM/DD)  
also works with relative refs ( _yesterday_, _3 days ago_)  
can be used in conjunction to establish start and end of tracking  

#### --author=
filter by user  
can be multiple users with \|  
works with user-email as well  
needn't be perfect match  

#### --grep=  
search by commit msg  

#### --merges and --no-merges 
as per cmd argument suggests  

#### range
using **..** defines a range between two arguments to act as start and endpoint of tracking.  
Useful for branch history, ex:  
```
git log main..feature
```
will display commit history of edits specific to the feature branch since creation off the main branch.  
feature..main instead will display commit hist of main branch since feature branch creation

### History of a file

providing file path after -- will list commits containing the file at set path.  

**-S""** and **-G""**  
can track a string or expression respectively, ie searching for where "hello world" was included in all files of the tree, through the history, 
```
git log -S"hello world"
```
will display commit history of any inclusion/deletion of the string.

## Git cherry-pick
Picks specific commits, from a branch or else,  
needs clean HEAD  
good for -> applying hot fixes to MAIN without applying other feature edits ; recuperating specific edits from a branch without the Mess  

#### --edit
allows to edit the commit message

#### --no-commit
on default, cherry pick creates a new commit when porting the branch's commits. no-commit allow to just import the edits without committing them


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

## GitCLI

### SETUP
#### git auth login
setup link with ghub accnt  

#### gh config set editor
+editors name  
sets up the editor for CLI  

#### gh alias set
sets frequent use aliases  

### REPO MANAGEMENT

#### gh repo create [name] 
creates repo of [name]  
- **-p**, **--template [repolnk]**, uses a repo as template
- **-t**, **--team [name]**, grants access to org of [name]
- **-c**, **--clone**, clones the repo locally

#### gh repo fork [repolnk]
forks repo  

#### gh repo clone [repolnk][dir]
clones a repo  

#### gh repo view [repolnk] 
views dist repo
- **-b** **--branch [string]** view specific branch
- **-w**, **--web**, opens repo in browser  

### ISSUES

#### gh issue create
creates an issue
- **-t**, **--title [string]**, specifies title
- **-l**, **--label [name]**, adds a label
- **-a**, **--assignee [login]** assigns people to the issue. 
    - @me self assigns the task

#### gh issue list
lists issues  
- **-a**, filters by assignee
- **-A**, filters by author
- **-s [open|closed|all]**, filters by state
    - on default, is "open"
- **-l** filters by label

#### gh issues status
shows status of issues  

#### gh issues view (number | url)
view specified issue
- **-c** displays comments

#### gh issue close (number | url)  
closes issue
- **-c** adds a closing comment
- **-r** specifies reason for closing

### PR

#### gh pr create
creates pull request
- **-a**, which branch to merge into
- **-f**, uses last commit info as PR title and body
- **-l**, adds label  

#### gh pr list
lists pull request
- **-a**, filters by assignee
- **-A**, filters by author
- **-s [open|closed|all]**, filters by state
    - on default, is "open"
- **-l** filters by label  

#### gh pr status
shows status of PRs  

#### gh pr view (number | url | branch)  
view specific pr
- **-c** displays comments  

#### gh pr checkout (number | url | branch)  
checkout pull request  

#### gh pr merge (number | url | branch) 
merges pull request  

#### gh pr diff (number | url | branch) 
display changes in pr  

#### gh pr close (number | url | branch)  
closes pr  
- **c** leaves closing comment
- **d** deletes branch upon closing

#### gh pr reopen (number | url | branch)
reopens closed pr
- **-c** leaves closing comment  
