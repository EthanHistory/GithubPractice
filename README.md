# GithubPractice
A repository for practicing hand-on git commends and github functionalities.
This repository is based on a [blog post about hand-on git commends](https://levelup.gitconnected.com/top-30-git-commands-you-should-know-to-master-git-cli-f04e041779bc)

# What am I going to learn about Git / Github through this repository?
1. Setting Up and Configuring Git
2. Basic Repository Management
3. Branching and Merging
4. Collaborating With Others
5. Advanced Repository Management

# Setting Up and Configuring Git

## 1. Set up your username and email
Setting up your username and email is the first thing you need to do before starting anything on your repository. If you type "--local" instead of "--global" or use default option then it will be applied to your current directory and override global configuration when you make some commits on the repositories.

```bash
git config --global user.name "Tara Routray"
git config --global user.email "dev@tararoutray.com"
```


## 2. Manage credentials for authentication in remote repository 
If you want to work with a remote repository (Github), you need credential so that you can securly transfer data and push your commits. 
Basically, there are 2 types of credentials for authentication purpose: Personal Access Token (PAT) and SSH keys. Username with password also used but it deprecated since March 2013. By using these credentials, you can securely interact with remote repositories. However, it would be burdensome if you keep typing your credentials on every push that you make. Fortunately, Git allow us not to do that with credential storage. There are five modes of credential storage, normally based on your operating system: default, cache, store, osxkeychain, manager. 
There is a great explanation on these storages in git official documentation.

```
- The default is not to cache at all. Every connection will prompt you for your username and password.

- The “cache” mode keeps credentials in memory for a certain period of time. None of the passwords are ever stored on disk, and they are purged from the cache after 15 minutes.

- The “store” mode saves the credentials to a plain-text file on disk, and they never expire. This means that until you change your password for the Git host, you won’t ever have to type in your credentials again. The downside of this approach is that your passwords are stored in cleartext in a plain file in your home directory.

- If you’re using macOS, Git comes with an “osxkeychain” mode, which caches credentials in the secure keychain that’s attached to your system account. This method stores the credentials on disk, and they never expire, but they’re encrypted with the same system that stores HTTPS certificates and Safari auto-fills.

- If you’re using Windows, you can enable the Git Credential Manager feature when installing Git for Windows or separately install the latest GCM as a standalone service. This is similar to the “osxkeychain” helper described above, but uses the Windows Credential Store to control sensitive information. It can also serve credentials to WSL1 or WSL2. See GCM Install Instructions for more information.
```

You can manage credentials for authentication by using the same commend, "git config", in the previous section. 
For example, the below commend show you what type of credential storage you are using.
```bash
git config credential.helper
```


## 3. Bring remote (Github) repository to your local workspace
Basically, I assume you already have a remote repository and try to work on the repository in your local git. The first thing you need to do is initialize git repository in the current directory with this commend,

```bash
git init
```

Secondly, let your git know the location of your remote repository. This is done by below commend,
```bash
git remote add origin <remote repository URL>
```

Thirdly, download the contents of the remote repository to your local git repository. This commend will do that.
```bash
git fetch
```

Finally, you would go to the branch where you want to work on by this commend
```bash
git checkout <branch>
```

Actually, you can do these steps all it once by one commend: "git clone".

```
git clone <remote repository URL>
```

# Basic Repository Management
After you set up your local repository from your remote repository, now you would do some coding and add files as you need. Whatever you do, the change you made should be dealt with. You would stage them to staging area or commit the staged changes or just discard some changes you don't need. These days, there are lots of convenient plugins where you can easily do these work but remember that what I am going to introduce you is how you manage your changes underneath those plugins.

## 1. Add files to staging area
The first step that you should do after you made some changes would be adding them to staged area and it is called "staging". You can add all files in the current directory by "." or you can add just one file.

```bash
git add some_file.js 
git add .
```

Putting them in staging are doesn't mean that you save those changes to your repository; You need one more step called "commit"

## 2. Commit changes
The second step is to commit your staged changes. One of simply ways is using "commit" commend with the option "-m" where you can put a message about the commit.

```bash
git commit -m "Your short summary about the commit"
```

## 3. Discard / Unstage changes
Sometimes you want to discard or unstage your changes before you commit them. In that case, you can use "reset", "rm", or "checkout" commends. Depending on parts you want to discard or unstage, make sure you use commends correctly. Basically, you would use "reset --mixed" or "rm --cached" when you want to unstage changes but not delete those changes. On the other hand, if you want to discard changes as well, consider to use "reset --hard" or "checkout --". Note that the former one is more destructive so that you restore staged changes as well.

```bash
git reset HEAD --mixed # Apply to all files
git reset HEAD path/to/file.txt # Apply to one file, option default is usually "--mixed"
# or
git rm --cached path/to/file.txt

# or
git checkout -- path/to/file.txt # Discard unstaged files. "--" means it's going to be a file name after the option
git reset --hard HEAd # More destructive commend; Discard all files in staged and unstaged status
```

## 4. Rename files
You can rename a file by a git operation "mv" as well. Note that this is compeletly different from deleting the file and recreating it with a new name.

```bash
git mv <source> <destination>
```

## 5. View the status of changes and commits
While or after you stage changes, you would need to check whether you add files properly. You can do it by using git commend "status"

```bash
git status
```

In case you want to know commits in a branch you are working on, you would figure it out by using git commend "log". 

```bash
git log
git log -p
```

You can also view a specific commit by git commend "show". The way git identify each commit is hash of the commit. You can use full size or left-most 6 characters of this hash to specify the commit you want to view.

```bash
git show 1af17e73721dbe0c40011b82ed4bb1a7dbe3ce29
git show 1af17e
```

In case you want to identify changes in detail, you can use "git diff" commend. You can see only staged differences by adding "--staged" option.

```bash
git diff
git diff --staged
```

## 6. Amend the most recent commit
Did you forgot to add some files or change email address in the most recent commit? "--amend" option in "git commit" commend would rescue you from those mistakes. If you want to change email or username, you would add "--reset-author" as well. In case you don't need to change the commit message, you would add "--no-edit" option on the top of "--amend" option.

```bash
git add forgetten_dir
git commit --amend --no-edit --reset-author
```

## 7. Rollback Last Commit
You can also revert a commit. "revert" commend will allow you to put another commit on your previous commits that restore all changes from target commit.

```bash
git revert <commit to revert>
```

---
**Revert vs Reset**

The commend "revert" in git undoes only a single commit. On the other hand, the commend "reset" undoes the commit and other commits ahead of it. This can come to benefit if you want to cherry-pick a commit to be rollbacked, not touching other commits. Another benefit on using revert over reset is that revert is safer way to rollback a commit. It doesn't modify any previous commit, but append another commit with rollbacking changes. Secondly, 

---


# Branching and Merging
Now you know how to setup git repository and do some basic operations that git provides. Next, I want to explain how to branch from your repository and merging a branch. Branch is a concept for developing independent features in a git project. It is especially important when you want to keep serving a stable version of your software, while developing some new features based on the version. You can do it separately from the main service and "merge" those features later when you think it is stable enough.

# 1. Create and switch to a new branch
Basically, the first branch exist when you create a repository is called master or main branch. You can create another branch by using "branch" commend.

```bash
git branch <new branch name>
```

But it doesn't mean that you switch to the branch. To change a branch from where you are working on, you need "checkout" commend with "-b" option

```bash
git checkout -b <branch name you want to go>
```

# 2. List all branches
You can also list up all the branches in your local repository. You would see asterisk(*) sign for the current branch. Additionally, you can list up branches in the remote repository as well, with "-a" option

```bash
git branch
git branch -a
```

# 3. Delete a branch
As you create a branch, you can delete the branch. You can use "-d" option. However, if you haven't merged the branch, git would give you error message because it is not safe to delete a branch where any other branch don't have reference. In case you just don't need the branch anyway, you would use just "-D" option to force deletion.

```bash
git branch -d <branch to be delete>
git branch -D <branch to be delete>
```

    Delete a Branch
    Merge Two Branches
    Show Commit Log as Graph For Current or All Branches
    Abort a Conflicting Merge
    Push a New Branch To Remote Repository
    Remove a Remote Branch
    Use Rebase