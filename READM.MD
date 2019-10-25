## Git tricks

### Show git history
 - git log --oneline

### Show git history tree ( O Cabueta )
 - git log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white) %s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all
 - git log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold cyan)%aD%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n''          %C(white)%s%C(reset) %C(dim white)- %an%C(reset)' --all

### Edit the last commit
 - ```git add .```
 - ```git commit -m "Some cool message"```
    - Ops, I forgot something and I dont want to generate another commit
 - ```git add new-file-changed.js```
 - ```git commit --amend ```
    - The preview commit will bee merged 
    - Dont do it if the commit was alread pushed to remote
 - ```git commit --amend --author "username <email@email.com>"``` // Edit the preview commit changing the author

### Unstage added files 
 - ```git add . ```// Stage all files 
 - ```git reset HEAD ```

### Restore working directory or got to some point of git history
 -``` git checkout src/main/``` // Restore src/main to the last state 
 - ```git checkout commit_id``` // Got to commit_id
 - ```git checkout some-branch ```// Switch to some-branch

### merge remote branch before merge request 
Sync remote development branch with local before sending merge request
 - ```git add .```
 - ```git commit -m "Some cool message of what I had done"```
 - ```git fetch``` // Sync branchs from remote 
 - ```git merge origin/development```  // merge development branch with current local branch
    - cry and pray for no conflicts
    - resolve any conflicts 
 - ```git push origin my-cool-local-branch```

 Then, send a merge request to development

### save current working directory before merging remote branch
Sync remote development branch before commit 
 - ```git fetch``` // Sync branchs from remote 
 - ```git stash```// Save current work dir without commit
 - ```git merge origin/development```// merge development branch with current local branch
 - ```git stash apply``` // apply stashed work dir
    - cry and pray for no conflicts
    - resolve any conflicts 
 - ```git add .```
 - ```git commit -m "Some cool message of what I had done"```


### Multi issues / branchs flow
 - ```git add .```
 - ```git commit -m "Wip: Some cool message of what you had been doing on branch my-cool-local-branch```
 - ```git checkout another-working-branch```
    - Do something on this new branch
    - commit, push and merge it with development
 - ```git checkout my-cool-local-branch```
 - ```git fetch```
 - ```git merge origin/development```
    - Keep working 

### Copy commits from one repo to another
 - ```git remote add someotherrepo https://github.com/someuser/somerepo```
 - ```git fetch someotherrepo```
 - ```git log someotherrepo/some-other-branch``` // See history commit from the other remote
 - ```git cherry-pick commit_id``` // copy commit by id to the local branch
 - ```git push origin my-cool-local-branch```

### rebase git history ( Only if you are the only one working in this project)
 - ```git log --oneline``` // Verify the commit id where you want to change
 - ```git rebase -i HEAD~5``` // The number represents how much commits must be returned to be edited
    - on the screen find the commit you want edit and rename 'pick' to 'edit' then save 
    - make the needed changes
        - case you dont want to do any change, ```git rebase --abort```
 - ```git rebase --continue```
 - ```git push origin remote-branch -f``` ( Dont do it! )