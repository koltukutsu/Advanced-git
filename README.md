# advanced-git commands which I have gathered while surfing in web
Advanced git commands that I don't know before
## degisiklik
1. ### Combine ADD and COMMIT
To save a snapshot of our code, we use "add" followed by a commit message.
```bash
git add .
git commit -m "New line added"
```
But, there's an actually a better way to get the job done.
You can go straight to commit by using the -am flag.
```bash
git commit -am "An easy way!"
```
This will automatically add all the files in the currenty working directory.

2. ### Aliases
There's actually a more concise way to get the job done.

The command git config provides a way to create aliases which are commonly used to shorten an existing command or create your own new custom commands.

Let's look at an example:
```bash
git config --global alias.ac "commit -am"
git ac "noice!!xD"
```
We made an alias called ac that runs the "add" and "commit" command with just two letters.

This allows us to run things faster, but sometimes going fast leads to mistakes.
3. ### Amend
What if we made a typo in the last commit??

Instead of resetting and committing a new commit, the --amend flag followed by a new message will simply update the latest commit.
```bash
git commit --amend -m "nice"
```
That's better!!

Or maybe you forgot to include or stage a couple of files with your last commit. You can also update your last commit with new files by using the --amend flag.

And if you want to keep the same commit message, add the --no-edit flag as well.

4. ### Force Push
Keep in mind, the above command only works when you haven't already pushed your code to a remote repository.

Unless you like to live dangerously, in which case, you can do a "git push" with the --force flag.
```bash
git push origin master --force
```
5. ### Revert
But what happens if you push some code to a remote repository and then realize it's a complete garbage and never should've been there in the first place.

Git revert command allows you to take one commit and go back to the state that was there previously.
```bash
git revert better-days
git log --oneline
```
We will use the "revert" command with the hash id of the latest commit.
```bash
git revert b4f4098
```

6. ### Stash
Have you ever spent time working on some changes that almost work, but they can't really be committed yet?

**git stash will** remove the changes from your current working directory and save them for later use without committing them to the repo.
```bash
git stash
git stash pop
```
when you're ready to add those changes back into your code.

But if you use the command a lot, you can use git stash save followed by a name to reference it later.
```bash
git stash save coolstuff
```
Then when you are ready to work on it again, use git stash list to find it and then git stash apply with the corresponding index to use it.
```bash
git stash list
git stash apply 0
```

7. ### Pretty Logs / Decorate Commits
```bash
git log --graph --oneline --decorate
```
![git-image](https://cdn.hashnode.com/res/hashnode/image/upload/v1650885288067/YWLBB2NH_.png?auto=compress,format&format=webp)

8. ### Searching Logs
This command returns the commit where the file is added in the Text directory.
```bash
git log -S "README file added? WUT?"
```

9. ### Bisect
Git bisect allows you to start from a commit that is known to have a bug, likely the most recent commit.
```bash
git bisect start
```
```bash
git bisect bad
git bisect good 5b010ef
git bisect bad
```
![git-image](https://cdn.hashnode.com/res/hashnode/image/upload/v1650885738714/DyOfiV0hB.png?auto=compress,format&format=webp)

10. ### Autosquash
Another advanced git technique that every developer should know is how to squash their commits.
![git-image](https://cdn.hashnode.com/res/hashnode/image/upload/v1650887016796/ptUEQMUb7.png?auto=compress,format&format=webp)
But all these commit messages are kind of pointless, and it would be better if it was just one single commit.
![git-image](https://cdn.hashnode.com/res/hashnode/image/upload/v1650887563534/e_ryRP3Tm.png?auto=compress,format&format=webp)
We can do that from our feature branch by running "git rebase" with the --interactive option for the main branch.
```bash
git rebase master --interactive
```
This will pull up a file with a list of commits on this branch.
If we want to use a commit, we just use the pick command.

We can also change a message using reword command.

Or we can combine or squash everything into the original commit using squash command.

Go ahead, save the file and close it.

Git will pull up another file prompting you to update the commit message, which by default will be a combination of all the messages that you just squashed.

And if you don't like all the messages combined, you can use "fixup" instead of "squash" when doing the rebase.

To be even more productive, you can also use --fixup and --squash flags when making commits on your branch.
```bash
git branch --fixup fb2f677
git command --squash fc2f55
```
On doing this, it tells git in advance that you want to squash them.

So when you go to do a rebase with the --autosquash command, it can handle all the squashing automatically.
```bash
git rebase -i --autosquash
```
11. ### Hooks
Could be very useful while maintaining a repo. Whenever you perform an operation with git like a commit for example, it creates an event. 
Could be very useful while maintaining a repo. Whenever you perform an operation with git like a commit for example, it creates an event. 
```bash
git commit -m "It is fixed"
```
If you look in the hidden git directory, you will see a directory called "hooks". And inside it, you will find a bunch of different scripts that can be configured to run when different events in git happen.
```
If you happen to be a JavaScript developer, there's a package called "husky" that makes it much easier to configure git hooks.
```
12. ### Destroy Things 💥💥
To wrap things up, let's talk about deleting things.

Let's imagine you have a remote repository on GitHub than a local version on your machine that you have been making changes to. But, things haven't been going too well.
![git-image](https://cdn.hashnode.com/res/hashnode/image/upload/v1650955498816/-Xs5E1mRG.png?auto=compress,format&format=webp)
And you just want to go back to the original state in the remote repo.
```bash
git fetch origin
git reset --hard origin/master
```
First, we do git fetch to grab the latest code in the remote repo.

Then, use reset with the --hard flag to override your local code with the remote code.

Be careful, your local changes will be lost forever.
But you might still be left with some random untracked files or build artifacts here and there.

Use the git clean -df command to remove those files as well.

If you want to get rid of it altogether, maybe you want to try out Apache subversion to change things up a bit.

All you have to do is, delete that hidden git folder, and you are on your own again.
![image](https://cdn.hashnode.com/res/hashnode/image/upload/v1650955921284/FhfyfCpE9.png?auto=compress,format&format=webp)
13. ### Checkout to Last
Oh! There's one other tip that comes in really handy.
If you recently switched out of a branch and forgot its name, you can use:
```bash
git checkout -
```
It takes you directly back to the previous branch that you were  working on.


# Thanks to the authors for sharing their information
 - [kubesimplify.com](https://cdn.hashnode.com/res/hashnode/image/upload/v1650887016796/ptUEQMUb7.png?auto=compress,format&format=webp)
