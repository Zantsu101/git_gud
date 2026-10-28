# hey fys! 👋 let's get branching

you know how to create a repository, track your files, and stage changes. now it's time to learn how developers actually work on projects without messing up each other's code.

imagine you're building a website. you want to add a login page, your friend wants to redesign the homepage, and someone else wants to fix a bug.

would you make all these changes directly to `main` and hope nothing breaks? probably not. 😭

that's where **git workflow and branches** come in!

by the end of this guide, you'll know how to create branches, make commits, push your work to github, and merge changes when they're ready.

**no prior branching experience needed. just follow along and experiment!**

---

## 1. understanding the git workflow

before learning branches, let's understand how changes move through git.

when you modify a file, git doesn't automatically save that change in your project history. you decide which changes to include and when to record them.

a simplified git workflow looks like this:

```text
        working directory
         (edit your files)
                |
                | git add
                v
          staging area
       (select your changes)
                |
                | git commit
                v
        local repository
        (save a snapshot)
                |
                | git push
                v
       remote repository
           (github)
```

let's understand each stage.

* **working directory:** where you create and modify your project files.
* **staging area:** where you select the changes you want to include in your next commit.
* **local repository:** where git stores your commits and project history on your computer.
* **remote repository:** the version of your repository hosted online, usually on github.

### the commands that connect everything

| command                   | what it does                                                                             |
| ------------------------- | ---------------------------------------------------------------------------------------- |
| `git add <file>`          | stages changes to a file                                                                 |
| `git commit -m "message"` | records staged changes as a commit                                                       |
| `git push`                | uploads local commits to a remote repository                                             |
| `git fetch`               | downloads information about remote changes without merging them into your current branch |
| `git pull`                | fetches remote changes and integrates them into your current branch                      |

**remember:** `git add` does not upload anything, and `git commit` does not push anything to github. each command has a different purpose!

📖 [Git documentation: Getting started](https://git-scm.com/docs/gittutorial)

---

## 2. commits: saving snapshots of your work

a **commit** is a snapshot of the changes you've staged. it gives you a point in your project's history that you can inspect later.

think of commits as checkpoints in a game. if something goes wrong later, these checkpoints help you understand how your project reached its current state.

### creating a commit

after making changes to a file, check what git detects:

```bash
git status
```

stage the file:

```bash
git add README.md
```

record the changes:

```bash
git commit -m "Update project documentation"
```

and that's it! you've created a commit.

### writing good commit messages

a commit message should briefly describe what changed.

| good commit message                | not-so-good commit message |
| ---------------------------------- | -------------------------- |
| `Add login form`                   | `changes`                  |
| `Fix navbar alignment`             | `stuff`                    |
| `Update installation instructions` | `final update v2`          |
| `Add input validation`             | `done`                     |

good commit messages make your project history easier to understand, especially when working with other people.

**pro tip:** try to keep each commit focused on one logical change instead of combining unrelated changes into a single giant commit.

---

## 3. what are branches?

a **branch** is a separate line of development in your repository.

imagine your project is a tree. `main` is the main branch, and you create another branch to work on a new feature.

you can experiment on that branch without immediately adding your changes to `main`.

```text
                    feature-login
                   /             \
                  /               \
main ------------●-----------------●
                 initial            merge
                 commit
```

this is a simplified illustration. the important idea is that you can work separately and combine your changes later.

### why do we need branches?

branches are useful because they let you:

* develop new features without directly changing `main`.
* experiment with ideas safely.
* fix bugs separately from ongoing development.
* work on different tasks without mixing unrelated changes.
* organise contributions in team projects.

### what is `main`?

`main` is commonly used as the default branch of a repository.

it usually contains the project's primary line of development. teams often protect it and require changes to be reviewed before they are merged.

**important:** `main` is just a branch name. it isn't a special kind of branch that git requires you to use.

---

## 4. creating and switching branches

let's learn the commands you'll use most often.

### viewing existing branches

```bash
git branch
```

this lists your local branches.

the branch marked with `*` is the branch you're currently on.

### creating a branch

suppose you want to add a login page.

```bash
git branch feature-login
```

this creates a new branch called `feature-login`.

**but there's a catch:** creating a branch doesn't automatically switch you to it.

### switching branches

to switch to an existing branch, run:

```bash
git switch feature-login
```

now you're working on `feature-login`.

### creating and switching in one command

instead of running two separate commands, you can use:

```bash
git switch -c feature-login
```

this creates the branch and switches to it immediately.

`-c` stands for create.

### older syntax

you might also see this command in older tutorials:

```bash
git checkout -b feature-login
```

it creates a branch and switches to it, too. for this workshop, we'll mainly use `git switch` because it makes the intention clearer.

### try it out

1. open a terminal inside your git repository.
2. check your current branch using `git branch`.
3. create a branch named `practice-branch` and switch to it.

```bash
git switch -c practice-branch
```

4. check your branches again.

```bash
git branch
```

you should now see `practice-branch` marked with `*`.

congratulations! you've created your first branch. 🎉

---

## 5. working on a branch

creating a branch is only the beginning. now let's actually make changes on it.

for this example, we'll create a small file representing a feature in our project.

### step 1: make sure you're on your branch

```bash
git switch practice-branch
```

### step 2: create a file

create a file named `feature.txt` in your repository and add the following content:

```text
this is my first feature.
i am learning git branches!
```

save the file.

### step 3: check your changes

```bash
git status
```

git should show `feature.txt` as an untracked file.

### step 4: stage and commit

```bash
git add feature.txt
git commit -m "Add first feature"
```

your changes are now recorded in the history of `practice-branch`.

### step 5: switch back to main

```bash
git switch main
```

now check whether `feature.txt` exists in your current working directory.

because the file was created and committed only on `practice-branch`, it won't appear on `main` unless it already existed there or the change has been integrated.

### step 6: switch back

```bash
git switch practice-branch
```

your committed file should be visible again.

**what just happened?**

you created a change on one branch without immediately adding it to another branch.

that's the fundamental idea behind branching!

**remember:** switching branches is easiest when your working directory is clean. if you have uncommitted changes, git may prevent the switch to avoid overwriting them.

---

## 6. pushing a branch to github

so far, we've been working locally on our computer.

what if you want to upload your branch to github so that other people can see your work?

that's where `git push` comes in.

### step 1: check your current branch

```bash
git branch
```

make sure you're on the branch you want to upload.

for example:

```text
* practice-branch
  main
```

### step 2: push the branch

```bash
git push -u origin practice-branch
```

let's break down the command:

* `git push`: uploads your local commits.
* `origin`: the conventional name for the remote repository.
* `practice-branch`: the branch you want to upload.
* `-u`: sets the upstream relationship between your local branch and its remote counterpart.

after setting the upstream, you can usually use these shorter commands on future updates:

```bash
git push
```

to upload new commits, and:

```bash
git pull
```

to fetch and integrate changes from the configured upstream branch.

### what if `origin` doesn't exist?

check your configured remotes:

```bash
git remote -v
```

if your repository has no remote, you need to connect it to a github repository before pushing. if `origin` already exists, don't add it again.

**important:** you need permission to push to the remote repository. cloning a public repository doesn't automatically grant write access.

---

## 7. keeping your branch updated

when working with other people, the `main` branch may change while you're developing your feature.

you might need to bring those changes into your own branch.

### fetching remote changes

```bash
git fetch origin
```

this downloads information about the remote repository's branches and commits without automatically integrating those changes into your current branch.

### pulling changes

if you want to update your local `main` branch from the remote, switch to `main` first:

```bash
git switch main
git pull origin main
```

this fetches and integrates changes from `origin/main` into your local `main` branch.

### bringing the latest main into your feature branch

first, update your local `main`:

```bash
git switch main
git pull origin main
```

then switch to your feature branch:

```bash
git switch practice-branch
```

you can merge the updated `main` into your feature branch:

```bash
git merge main
```

this helps you incorporate the latest changes before integrating your work into `main`.

**note:** pulling and merging can sometimes produce conflicts. don't panic if that happens! module 4 covers merge conflicts in more detail.

📖 [Git documentation: git fetch](https://git-scm.com/docs/git-fetch)

---

## 8. merging branches

you've made a change on your feature branch, and now you want to bring it into `main`.

that's where **merging** comes in.

merging combines changes from different branches.

let's merge our `practice-branch` into `main`.

### step 1: switch to the branch that should receive the changes

```bash
git switch main
```

we're switching to `main` because that's where we want the changes to be integrated.

### step 2: merge the feature branch

```bash
git merge practice-branch
```

git attempts to integrate the changes from `practice-branch` into the current branch.

if git can merge the changes automatically, it completes the merge.

if the branches have conflicting changes, git will ask you to resolve them before the merge can finish.

### step 3: verify the result

```bash
git status
```

you can also inspect the recent commit history:

```bash
git log --oneline --graph --all
```

if the merge succeeded, the changes from `practice-branch` are now part of `main`.

### step 4: push the updated main branch

if you have permission to push directly to the remote `main` branch:

```bash
git push origin main
```

if your team requires pull requests, push your feature branch and open a pull request on github instead.

### step 5: clean up the branch

after the branch has been merged and you no longer need it, you can delete the local branch:

```bash
git branch -d practice-branch
```

if you also pushed that branch to github and want to delete the remote branch:

```bash
git push origin --delete practice-branch
```

only delete branches when you're sure they're no longer needed.

**important:** in shared repositories, follow your team's rules before deleting branches or pushing directly to `main`.

📖 [Pro Git: Basic Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)

---

## 9. exploring your git history

ever wondered what changes you've made or which commit introduced a particular feature?

git provides commands that help you inspect your project's history.

### viewing commit history

```bash
git log
```

this displays detailed information about previous commits.

for a shorter view:

```bash
git log --oneline
```

each commit is displayed on a single line.

### viewing the branch history

```bash
git log --oneline --graph --all
```

this displays a compact history of commits across branches, using a graph to show how the branches developed and where they were merged.

### checking unstaged changes

```bash
git diff
```

this shows differences between your working directory and the staging area.

### checking staged changes

```bash
git diff --staged
```

this shows changes you've staged but haven't committed yet.

### why are these commands useful?

* `git log` helps you understand the project's history.
* `git diff` helps you review modifications before staging them.
* `git diff --staged` helps you check what you're about to commit.
* `git log --oneline --graph --all` helps you visualise branching and merging.

**pro tip:** before committing, review your changes. it's much easier to catch a mistake before it becomes part of your project history!

---

## 10. a few common mistakes to avoid

learning git involves making mistakes. here are some things to keep in mind.

| mistake                                   | what to remember                                               |
| ----------------------------------------- | -------------------------------------------------------------- |
| forgetting which branch you're on         | run `git branch` or `git status`                               |
| creating a branch but not switching to it | use `git switch -c <branch_name>`                              |
| forgetting to commit                      | run `git status` to check for uncommitted changes              |
| forgetting to push                        | your local commits aren't automatically uploaded               |
| trying to push without permission         | use your own fork or request access                            |
| merging into the wrong branch             | check `git branch` before running `git merge`                  |
| deleting a branch too early               | make sure its work has been integrated and is no longer needed |

### what if you want to abandon a merge?

if a merge is in progress and you decide you don't want to continue it, you can usually cancel it with:

```bash
git merge --abort
```

this attempts to return the working tree to its state before the merge began.

**be careful:** commands that discard changes can cause data loss. don't run unfamiliar commands blindly, especially when you have work you haven't committed.

module 4 covers more advanced collaboration topics, including merge conflicts and undoing changes.

---

## 11. hands-on challenge: build your first feature branch! 🚀

time to put everything together.

imagine you're contributing to a student project, and your task is to add a short introduction to its README.

follow these steps in your own practice repository.

### task 1: check your repository

```bash
git status
git branch
```

make sure you're in the correct repository and know which branch you're currently using.

### task 2: create a feature branch

```bash
git switch -c add-introduction
```

### task 3: make a change

open `README.md` and add a small section:

```markdown
## About Me

Hi! I'm a first-year student learning Git and GitHub.
I'm excited to start contributing to projects!
```

save the file.

### task 4: review and commit your changes

```bash
git status
git diff
git add README.md
git diff --staged
git commit -m "Add introduction to README"
```

notice how we review the changes both before and after staging.

### task 5: push your branch

```bash
git push -u origin add-introduction
```

open your repository on github and check that your branch is visible.

if you don't have permission to push to the repository, use your own practice repository or fork instead.

### task 6: merge your changes

if you're practising in a repository where you can merge directly into `main`, run:

```bash
git switch main
git merge add-introduction
```

if the remote repository has changed and you want to update your local `main` first, fetch and integrate the latest changes before merging.

if you're working in a shared workshop repository, follow the organisers' instructions instead. they may ask you to open a pull request and wait for approval.

### task 7: verify your work

```bash
git log --oneline --graph --all
git status
```

check that your commit is present and that your working directory is in the expected state.

### bonus challenges

once you've completed the main task, try these:

1. create another branch called `change-introduction`.
2. modify the introduction and create another commit.
3. use `git log --oneline` to inspect your commit history.
4. use `git diff` to inspect a change before committing it.
5. create two branches and observe how their histories differ.

if something goes wrong, don't panic. start by running `git status`, read the message git gives you, and ask for help if you're unsure what to do.

---

## quick cheat sheet

| what you want to do                          | command                            |
| -------------------------------------------- | ---------------------------------- |
| check the current branch                     | `git branch`                       |
| create a branch                              | `git branch <branch_name>`         |
| switch branches                              | `git switch <branch_name>`         |
| create and switch branches                   | `git switch -c <branch_name>`      |
| check repository status                      | `git status`                       |
| stage a file                                 | `git add <file>`                   |
| commit changes                               | `git commit -m "message"`          |
| push a branch for the first time             | `git push -u origin <branch_name>` |
| push subsequent commits                      | `git push`                         |
| fetch remote updates                         | `git fetch origin`                 |
| pull updates                                 | `git pull`                         |
| merge another branch into the current branch | `git merge <branch_name>`          |
| view commit history                          | `git log --oneline`                |
| visualise branch history                     | `git log --oneline --graph --all`  |
| view unstaged changes                        | `git diff`                         |
| view staged changes                          | `git diff --staged`                |
| delete a merged local branch                 | `git branch -d <branch_name>`      |

---

## useful resources 📚

* [Git documentation](https://git-scm.com/doc) — official Git documentation.
* [Pro Git: Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging) — learn how branching and merging work.
* [Learn Git Branching](https://learngitbranching.js.org/) — an interactive way to visualise Git branches.
* [GitHub Skills](https://skills.github.com/) — hands-on courses for learning GitHub.

---

you've now learned how to create branches, record changes, push your work to github, and merge branches together!

these are some of the most useful skills you'll use in college projects, hackathons, internships, and open-source contributions.

don't worry about memorising every command. keep practising, check `git status` when you're confused, and remember that everyone starts somewhere.

**happy coding, fys! 💜**
 