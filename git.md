# Git and GitHub

## What (and why) is Git?

Git is a version control software (VCS) that has become the standard for managing development projects. It serves two main purposes:

1. Version Control: manage the evolution of a project as it grows in complexity, easily rollback or revert breaking changes, inspect history, and maintain separate versions for development, integration, release, etc.
2. Collaboration: allow many users to collaborate on a single codebase remotely in an effective and managed manner; provides tools for integrating changes from multiple developers, resolving conflicts, and tracking the owner of certain features/changes.

You should use git for every software project you work on, regardless of whether you share that project with others.
You do not need to use GitHub with git.
You should be comfortable with using git from the command line (without a GUI).
You do not need to memorize all the git commands, but we'll cover an important set of them.
You do not need to be a pro on resolving merge conflicts, but should be comfortable if one pops up.

> Note: git keeps track of all this neat stuff in a folder that you can view (put should probably never mess with) in the projects `.git/` folder

## Fundamentals (git)

We'll cover the core concepts and terms that are fundamental to understanding git

**Repository**: A "repo" is a collection of managed code. It may represent a complete project, a part of a larger project, or really logical unit of code.
**Remote**: Repositories can be set up to keep in sync with a "remote" repository that is kept in a central place like GitHub, GitLab, BitBucket, etc. allowing for effective collaboration.
**Branch**: A branch is a tool to keep some collection of changes separated from the rest of the project. Commonly used to work on developing new features while the "main" branch is kept stable.
**Commit**: A commit marks a set of changes submitted to the code's history. It's up to the developer to decide what should go in a commit, but best practice is to keep commits small and "atomic", meaning that they can stepped through one-by-one without breaking the project. These are identified by a "SHA" (unique hash value).
**HEAD**: This is a special marker in git (similar to a "SHA") that points to the latest commit on the active branch (indicating where new commits will be applied).
**Working Tree**: This represents the state of the files on your local computer. This may include new changes, ignored files, etc. and thus not fully match the state of the repository.
**Stage**: The stage is the collection of changes that are about to be committed. This allows you to specify which changes make it into a commit when you have a lot of unrelated changes in your working tree.

## Configuration

config
gitignore
global gitignore

## Working with Remotes

Local repositories can be kept in sync with a single "remote" (git calls this `origin` by default), or with many named remotes. Each remote will have an identifying name and a url associating it with the remote repository.

### Remotes

A "remote" is just a central location for a repository to be kept, allowing for local repositories to keep in sync with each other. You may wish to use a remote for collaboration, or just as a backup place for your personal projects to live. GitHub, GitLab, and BitBucket are all popular choices. Users interact with remotes via push and pull to publish local changes and retrieve changes contributed by others.

### Forks

A "fork" is just a way for you to contribute or make changes to another remote repository without direct collaboration. Many open source projects have strict guidelines or restrictions around who can contribute code and how. If you find you need to make changes to a repository you don't own, remotes give the option to create a fork which retains a link to the source but grants ownership to you. Forks operate like branches but at a higher level.

### Conflicts

When you interact with a remote repository with many collaborators, you are bound to encounter conflicts when attempting to reconcile (merge) changes made by multiple people.

For example, you may change a script to load a file from you computer's local filesystem; one of your collaborators do the same. When you both push to the same central remote, the remote will see two different changes to the same line of code and panic; you must tell git how to "resolve" that conflict. There are lots of ways to avoid or reduce merge conflicts (and lots of ways to resolve them), but that's a bit beyond scope of this tutorial. In general, try to communicate with and separate your work from your collaborators, use branches, pull requests, and other provided tools, and keep system-specific configuration in environment variables or an "ignored" configuration file (kept out of version control).

### Pull Requests (or Merge Requests)

Pull requests are a feature provided by remotes (like GitHub, etc.) which offer a nice way to integrate changes which have been kept in separate branches. Most common is a request to merge development changes back into the "main" branch once deemed complete. Typical pull request systems allow you to specify the source and destination branches (e.g. `development -> main`), provide comments on your request, solicit reviews from collaborators, review code changes and submit comments or approval/request to change, and finally merge the changes from source to destination branch. Pull requests are an excellent feature as they help keep the main branch clean and give collaborators a place to review and discuss each other's work.

![Basic Git Workflow (how changes progress)](https://www.cloudturbine.com/wordpress/wp-content/uploads/2016/08/git_workflow.png)

## Quick Note on Best Practices

Git is pretty flexible and leaves a lot of room for style and choice. However, because git is meant to simplify collaboration, it is worth following some common best practices if you can.

### General

- Test first, commit second: commits become a part of the project's permanent history, try not to commit things that are broken.
- Use your stash for unfinished work: if you need to pull, or checkout something but have in-progress, local changes, you can "stash" them instead of creating a temporary commit.
- Commit early and often: repo timelines are far more helpful if you can step through small, incremental changes.
- Write good messages: more info [below](#commit-messages).
- Don't panic: if you think you've messed up, don't worry - [so has everyone](https://www.edureka.co/blog/common-git-mistakes/) - and there are lots of guides online! Just a simple google of "Oops... I committed all those changes to the master branch" will usually get you an answer! Also see [How to undo (almost) anything with Git](https://github.blog/2015-06-08-how-to-undo-almost-anything-with-git/).

### Commit Messages

Motivation: As noted, commits are meant to be stable checkpoints in history containing some small, meaningful change and able to run stably on its own. Because of this, a commit needs to help you identify what that change was and why it's there! The contents of a commit can be easily inspected to show what changed; however, the "why" is answered only by the commit message. Make a point to answer this question in your commit message.

Format:

Title should answer the prompt: _"If applied, this commit will..."_
> Allow users to log in with one time passcode

Body should provide more detail around the motivation.
> Project managers have requested TFA for increased security.
> Users have indicated a hesitance to install additional apps for this
> so we decided on OTP for convenience.


Example:
```
Capitalized, short (50 chars or less) summary

More detailed explanatory text, if necessary.  Wrap it to about 72
characters or so.  In some contexts, the first line is treated as the
subject of an email and the rest of the text as the body.  The blank
line separating the summary from the body is critical (unless you omit
the body entirely); tools like rebase can get confused if you run the
two together.

Write your commit message in the imperative: "Fix bug" and not "Fixed bug"
or "Fixes bug."  This convention matches up with commit messages generated
by commands like git merge and git revert.

Further paragraphs come after blank lines.

- Bullet points are okay, too

- Typically a hyphen or asterisk is used for the bullet, followed by a
  single space, with blank lines in between, but conventions vary here

- Use a hanging indent

If you use an issue tracker, add a reference(s) to them at the bottom,
like so:

Resolves: #123
```

**The seven rules of a great Git commit message** (from [Chris Beams blog](https://chris.beams.io/posts/git-commit/))
1. Separate subject from body with a blank line
2. Limit the subject line to 50 characters
3. Capitalize the subject line
4. Do not end the subject line with a period
5. Use the imperative mood in the subject line
6. Wrap the body at 72 characters
7. Use the body to explain what and why vs. how

### Working with Collaborators

A few basic rules to keep in mind:

- Try to avoid working on the same file in the same branch as another developer as this will inevitably lead to merge conflicts.
- If you are working on the same branch as a collaborator, communicate well and pull/push often so that they know what you've changed and are not stuck waiting on un-pushed changes while you're away.
- You should (almost) **never** rewrite history in the remote. If you need to "undo" some commits locally, that's fine. But don't undo commits that have been pushed as this will corrupt repo history for people who have pulled recently. Instead, use `git revert <SHA>` which will create a new commit undoing the specified changes.


There are many different workflows for collaboration - pick your favorite for your own projects, or check with your team/project owners for there preferred strategy.

One popular one is "Gitflow":
![GitFlow Workflow (one strategy for remote collaboration)](https://wac-cdn.atlassian.com/dam/jcr:b5259cce-6245-49f2-b89b-9871f9ee3fa4/03%20(2).svg?cdnVersion=1548)

> Note: most open source projects include a `COLLABORATING.md` document outlining their desired collaboration pattern. Please respect this if you plan to contribute!

## Common Commands

### Local

`status`: Shows the current status including current branch, comparison to remote, list of new changes, and the stage contents ready for commit
`log`: Shows a log of commits made on the current branch
`show`: Shows the changes contained by a particular commit (or other git object)
`diff`: Shows the changes between particular commits or between a commit and the working tree
`stash`: Moves your current set of changes into a "stash" for later, returning your working tree to the last commit (can then `list`, `apply`, or `pop` them back out)
`add`: Adds changes from working tree to the "stage"
`reset`: Removes changes from the "stage" (changes kept in working tree)
`commit`: Commits the changes in "stage" to version control history
`revert`: Create a new commit (or commits) that undo the specified changes
`branch`: List (`-l`, `-r`, `-a`, or with no arguments), create (specify branch name as argument), or delete branches (`-d` or `-D`)
`checkout`: Switch branches or restore some file in working tree from its state in history (`git checkout -- some_file`)
`tag`: Create a new tag pointing to `HEAD` or list existing tags, or delete a specified tag

### Remotes

`clone`: Download some repository from a remote to your local machine (must have access if private)
`fetch`: Download objects and refs (branches/tags) from remote
`remote`: Manage remote repositories tracked by local repository (no arguments to list remotes, `-v` to include associated urls)
    `add` to add new remote (specify name and url)
    `rename` to change name for existing remote
    `remote` to remove
    `set-url` to change url for existing remote
`pull`: Incorporate remote changes to local branch (`fetch` and `merge` by default); this will make changes to your working tree (local filesystem)
`merge`: Creates a new commit which includes all the changes from two branches since their divergence
`rebase`: Reapply commits on top of another base (stashes your un-pushed local commits, pulls down the new remote commits, then pops those stashed local commits)

> Note: merge and rebase can be quite confusing... I think [this guide](https://www.atlassian.com/git/tutorials/merging-vs-rebasing) explains the difference quite well; or, more info on [merge](https://www.atlassian.com/git/tutorials/using-branches/git-merge) and [rebase](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase)

> Note: anything that changes your working tree (pull, merge, rebase, etc.) should only be run with a **clean** working tree; e.g. stash or commit any new changes first.

![Merge Branch Diagram](https://wac-cdn.atlassian.com/dam/jcr:83323200-3c57-4c29-9b7e-e67e98745427/Branch-1.png?cdnVersion=1549)

## Managing Releases

### Tags

Tags are useful references that point to a particular reference (commit/branch). This allows you to identify commit `2f8b5e9ccef3d9ac0d03db8f5187124e33d400dd` as tag `v1.0 - much nicer! Tags end up being used to identify significant development points, most often: versions.

### Releases

Remotes typically allow you to create a "release" with documentation, packaged software, and the source code associated with a particular point in the repository's history. These are particular useful when managing software used by others.


### Wikis

Wikis provide a place for you to add extra documentation (typically much more extensive than a README file) for your users. This may be geared towards using the actual software provided by your project, explaining the history of the project, or anything else you deem important.

## GitHub Features

### Issues



### Repo Settings



### SSH Keys



#### Using You New SSH Key with Github

You can try this with any repository you have access to, for now, let's try it with this one (since it's public).

On the repository home page, you should see a big green button that says **Code**. Just click this button to clone it - but wait! If you're new to ssh, your pop-up probably says **HTTPS** at the top - we want to change that to **SSH**. The new link to copy should look like: `git@github.com:michaelfedell/linux_essentials.git`

### GPG Keys



### Actions



### Pages



## What if I?

> Have made a ton of changes since my last commit...

add/commit changes incrementally

> Can't push because someone else has made changes...

stash/commit, pull (merge/rebase), push

> Can't pull because I've made changes...

stash

> Can't find the changes I was working on...

check your stash, check your current branch, etc.

> Need to "go back in time"...

git checkout <some commit>

> Mess up some file and need to reset it

git checkout -- <some file>

> Forgot to add a file to my last commit

git commit --amend --no-edit (`oops`)

> Accidentally committed something secret (api key, passwords, etc...)

It's in history forever...  
Expire the secret, purge from history (bfg)

> Committed something that shouldn't be in git (not sensitive)

git reset <some file> or git remove --cached

> Have made a ton of commits on my branch that I don't want to show up in main branch

git rebase --interactive

## More Resources

GitHub provides a nice "cheat sheet" for common git commands:  
https://education.github.com/git-cheat-sheet-education.pdf

Atlassian (providers of BitBucket) has an excellent tutorial/handbook for all things git:  
https://www.atlassian.com/git/tutorials/what-is-version-control

git-scm is the official git software website, their manual pages are often quite helpful when googling something specific, or you can see there handbook here:  
https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control

