### Basic Workflow
* Once you've created the repository and done your first commit, or forked it onto your local drive this is the basic workflow:
* `git status` - displays what files have changed or been added or deleted.
* `git add -A` - adds all changes ("stages" the files). The `A` flag adds all changes.
* `git commit -m "your message"` - commits all changes and adds a message describing this change.
* `git push` - pushes your changes to the remote repository.
* Here's a very useful [cheat sheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) with multiple basic git commands.

### Synchronizing Changes
* You may do this in a couple of ways. You can use `git fetch` in combination with `git merge` or just `git pull`. The recommended method is just to do `git pull`. Here's a description of what they do:
* `git fetch` - gets all the changes from the repository but doesn't change your local files.
* `git merge` - combines the changes that you just fetched to update your files.
* `git pull` - downloads all the changes and updates your local files.

### Other
* `rm -rf .git/` - to remove that directory from “version control”.

### Errors
* To 'unstage' commits do: `git reset --soft HEAD~` (if you need to 'unstage' multiple commits, repeat this command as many times as needed). Afterwards, when you've fixed the files you can `git add -A` and `git commit` again.
* To remove from files you have 'added' do:`git reset HEAD <file>`. Your files will still be in the folder but they will not be 'added' to github anymore.
* If you only need to change the commit message then `git commit --amend` will open the message editor.

More info [here](https://github.com/denten/dhnotes/wiki/github-workflow) by Dennis Tenen.