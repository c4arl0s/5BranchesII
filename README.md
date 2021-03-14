# [go back to content](https://github.com/c4arl0s/RysGitTutorial#rys-git-tutorial)

# [5 Branches II RysGitTutorial - Content](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#go-back-to-content)
 * [Continue the Crazy Experiment](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#-continue-the-crazy-experiment)
 * [Merge the CSS Updates](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#-merge-the-css-updates)
 * [Style the Rainbow Page](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#-style-the-rainbow-page)
 * [Link to the Rainbow Page](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#-link-to-the-rainbow-page)
 * [Fork an Alternative Rainbow](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#-fork-an-alternative-rainbow)
 * [Change the Rainbow](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#-change-the-rainbow)
 * [Emergency Update](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#-emergency-update)
 * [Publish the News Hotfix](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#-publish-the-news-hotfix)
 * [Complete the Crazy Experiment](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#-complete-the-crazy-experiment)
 * [Publish the Crazy Experiment](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#-publish-the-crazy-experiment)
 * [Resolve the Merge Conflicts](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#-resolve-the-merge-conflicts)
 * [Cleanup the feature Branches](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#-cleanup-the-feature-branches)
 * [Rename Branches Local and Remote](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#-rename-branches-local-and-remote)
 * [Conclusion](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#-conclusion)
 * [Quick Reference](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#-quick-reference)

# [5 Branches II ](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#5-branches-ii-rysgittutorial---content)

Now that you have covered the mechanics behind Git Branches, we can discuss the practical impact that they have on the software development process.
Instead of introducing new commands, this module covers how the typical Git user applies this workflow to real projects, as well as some of the problems that arise in a branched environment.

**To git, a branch is a branch, but it is often useful to assign special meaning to different branches**. 

> For example, we have been using master as the stable branch for our example project, and we have also used a temporary branch to add some CSS formatting.
**Temporary branches like the latter are called topic branches because they exist to develop a certain topic branches later in this module**.

**Amid our exploration of Git branches, we will also discover that some merges cannot "fast-forwarded**". When the history of two branches diverges, a dedicated commit is required to combine the branches. **This situation may also give rise to a merge conflict, which must be manually resolved before anything can be committed to the repository**.


# 	* [Continue the Crazy Experiment](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#5-branches-ii-rysgittutorial---content)

Let`s start by checking out the crazy branch.

```console
$ git branch
  crazy
* master
```

```console
$ git checkout crazy
Switched to branch 'crazy'
```

```console
$ git log --oneline
95a36a7 (HEAD -> crazy) Rename crazy.html to rainbow.html
e1bc771 add a rainbow to crazy.html
12e24f0 Add a crazzy experiment
453c8a4 (tag: v1.0) Add navigation links
1047951 t Add blue an orange html files
6a442fc Create index page for the message
```

**The crazy branch is a longer-running type of topic branch called a feature branch**.
This is fitting, as it was created with the intention of developing a specific feature. It is also a term tht makes Git's contribution to the development workflow readly apparaent: branches enable you to focus on developing one clearly defined feature at a time.

This brings us to my rule-thumb for using git branches:

1. **Create a new branch for each mayor addition to your project**.
2. **Don't create a branch if you cannot give it a specific name**.

Following these simple guidelines will have a dramatic impact on your programming efficiency.


# 	* [Merge the CSS Updates](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#5-branches-ii-rysgittutorial---content)

**Note that CSS formatting we merged into master is nowhere to be found**.
This presents a bit of a problem if we want to experiment to reflect these updates.
Conveniently, Git let us merge changes into any branch (not just the master branch).
So, we can pull the updates in with the familiar git merge command.
Remember that merging only affects the checked-out branch.

```console
$ git merge master
```

Editing

```vim
Merge branch 'master' into crazy
""
""
""
```

```console
$ git merge master
Merge made by the 'recursive' strategy.
 blue.html   |  1 +
 index.html  |  1 +
 orange.html |  1 +
 style.css   | 14 ++++++++++++++
 4 files changed, 17 insertions(+)
 create mode 100644 style.css
```

**As of Git 1.7.1.0, this will open your editor and prompt you for a message explaining why the commit was necessary**.
You can use the default Merge branch master into crazy. When you save and close the file, you will notice an extra commit in your project history. **Recall that our first merge didn't add any new commits; it is just "fast-forwarded" the tip of the master branch**. This was not the case for our new merge, which is shown below.

![Screen Shot 2020-05-24 at 11 50 02](https://user-images.githubusercontent.com/24994818/82759729-c7cd0e00-9db4-11ea-9b4b-8e97fc80512e.png)

Take a moment to examine why the current merge could not be fast-forward one. 
How Could Git have walked the crazy pointer over the tip of the master branch ?
**It is not possible without backtracking, which kind of defeats the idea of "fast-forwarding"
We are left with a new way to combine branches: the 3-way merge**.

**A 3-way merge occurs when you try to merge two branches whose history has diverged**. It creates an extra merge commit to function as a link between the two branches.
**As a result, it has two parent commits**. The above figure visualizes this with two arrows originating from the tip of crazy. **It is like saying "this commit comes from both the crazy branch and from master**". After the merge, the crazy branch has access to both its history and the master history.

![3-way-merge](https://user-images.githubusercontent.com/24994818/111052208-baa20e00-841e-11eb-8b47-a00d9c285ce1.png)

The name comes from the internal method used to create the merge commit. **Git looks at three commits (numbered in the above figure) to generate the final state of the merge**.

This kind of branch interaction is a big part of what makes Git such a powerful development tool. **We can not only create independent lines of development, but we can also share information between them by tying together their stories with a 3-way merge**.

# 	* [Style the Rainbow Page](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#5-branches-ii-rysgittutorial---content)

Now that we have access to the CSS updates from master, we can continue developing our crazy experiment.
Link the CSS stylesheet to rainbow.html by adding the following HTML on the line after title element

```html
<link rel="stylesheet" href="style.css" />
```

Stage and commit the update, then check that it is reflected in the history

```console
$ git status
On branch crazy
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   rainbow.html

no changes added to commit (use "git add" and/or "git commit -a")
```

```console
$ git commit -a -m "add CSS stylesheet to rainbow.html"
[crazy 6a43f42] add CSS stylesheet to rainbow.html
 1 file changed, 1 insertion(+)
```

```console
$ git log --oneline
6a43f42 (HEAD -> crazy) add CSS stylesheet to rainbow.html
b9f2b14 Merge branch 'master' into crazy
1a27d0e (master) link HTML pages to stylesheet
019e981 Add CSS stylesheet
95a36a7 Rename crazy.html to rainbow.html
e1bc771 add a rainbow to crazy.html
3553479 Revert "Add a crazzy experiment"
12e24f0 Add a crazzy experiment
453c8a4 (tag: v1.0) Add navigation links
1047951 t Add blue an orange html files
6a442fc Create index page for the message
```

**Notice that we skipped the staging step this time around**.
Instead of using git add, we passed the -a flag to git commit.
This convenient parameter tells Git to automatically include all tracked files in the staged snapshot.
Combined with the -m flag, we can stage and commit snapshots with a single command.
However, be careful not to include unintended files when using the -a flag.

# 	* [Link to the Rainbow Page](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#5-branches-ii-rysgittutorial---content)

We still need to add  navigation link to the home page.
Change the "Navigation section of index.html to the following.

```html
<h2>Navigation</h2>
<ul>
  <li style="color: #F90">
    <a href="orange.html">The Orange Page</a>
  </li>
  <li style="color: #00F">
    <a href="blue.html">The Blue Page</a>
  </li>
  <li>
    <a href="rainbow.html">The Rainbow Page</a>
  </li>
</ul>
```

As usual, stage and commit the snapshots.

```console
$ git commit -a -m "Link index.html to rainbow.html"
[crazy 4310454] Link index.html to rainbow.html
 1 file changed, 3 insertions(+)
```

```console
$ git log --oneline
4310454 (HEAD -> crazy) Link index.html to rainbow.html
6a43f42 add CSS stylesheet to rainbow.html
b9f2b14 Merge branch 'master' into crazy
1a27d0e (master) link HTML pages to stylesheet
019e981 Add CSS stylesheet
95a36a7 Rename crazy.html to rainbow.html
e1bc771 add a rainbow to crazy.html
3553479 Revert "Add a crazzy experiment"
12e24f0 Add a crazzy experiment
453c8a4 (tag: v1.0) Add navigation links
1047951 t Add blue an orange html files
6a442fc Create index page for the message
```

# 	* [Fork an Alternative Rainbow](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#5-branches-ii-rysgittutorial---content)

Next, we are going to brainstorm an alternative to the current rainbow.html page.
This is a perfect time to create another topic branch:

```console
$ git branch crazy-alt
```

```console
$ git checkout crazy-alt
Switched to branch 'crazy-alt'
```

Remember, we can do whatever we want here without worrying about either crazy o master.
When git branch creates a branch, it uses the current HEAD as the starting point for the new branch.
This meeans that we begin with the same files as crazy (if we called git branch from master, we would have to re-create rainbow.html).
After creating th new branch, our repository's history looks like:


![Screen Shot 2020-05-25 at 8 26 51](https://user-images.githubusercontent.com/24994818/82816850-8181b880-9e61-11ea-8f1e-0019d14a9538.png)

# 	* [Change the Rainbow](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#5-branches-ii-rysgittutorial---content)

Change the colorful list in rainbow.html from:

```html
  <li style="color: red">Red</li>
  <li style="color: orange">Orange</li>
  <li style="color: yellow">Yellow</li>
  <li style="color: green">Green</li>
  <li style="color: blue">Blue</li>
  <li style="color: indigo">Indigo</li>
  <li style="color: violet">Violet</li>”
```

to the following:

```html
<div style="background-color: red"></div>
<div style="background-color: orange"></div>
<div style="background-color: yellow"></div>
<div style="background-color: green"></div>
<div style="background-color: blue"></div>
<div style="background-color: indigo"></div>
<div style="background-color: violet"></div>
```

Then, add some CSS formatting to head on the line after the meta element

```html
	<style>
  div {
    width: 300px;
    height: 50px;
		 }
	 </style>
```

If you open rainbow.html in a browser, you should now see colorful blocks in place of the colorful text. Don't forget to commit the changes:

```console
$ git commit -a -m "Make a REAL rainbow"
[crazy-alt d247771] Make a REAL rainbow
 1 file changed, 13 insertions(+), 7 deletions(-)
```

The resulting project history is show below, with the first four commits ommitted for the sake of presentation.

![Screen Shot 2020-05-25 at 8 49 40](https://user-images.githubusercontent.com/24994818/82818699-b5aaa880-9e64-11ea-9eff-305ed0bca27d.png)


# 	* [Emergency Update](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#5-branches-ii-rysgittutorial---content)

Our boss called in with some breaking news ! He needs us to update the site immediately, but what do we do with our rainbow.html developments? Well, the beauty of Git branches is that we can just leave them where they are and add the breaking news to master.

We will use what is called a hotfix branch to create and test the news updates. In contrast to our relatively long-running feature branch (crazy), hotfix branches are used to quickly patch a production release.

For example: you would use a hotfix branch to fix a time-sensitive bug in a public software project. This distinction is useful for demonstrating when it is appropiate to create a new branch, but it is purely conceptual - a branch is a branch according to Git

```console
$ git checkout master
Switched to branch 'master'
```

```console
$ git branch news-hotfix
```

```console
$ git checkout news-hotfix
Switched to branch 'news-hotfix'
```

Change the "News" list in index.html to match the following.

```html
	<ul>
	  <li><a href="news-1.html">Blue Is The New Hue</a></li>
  </ul>
```

And, create a new HTML page called news-1.html with the following content.

```console
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Blue Is The New Hue</title>
  <link rel="stylesheet" href="style.css" />
  <meta charset="utf-8" />
</head>
<body>
  <h1 style="color: #079">Blue Is The New Hue</h1>
  <p>European designers have just announced that
  <span style="color: #079">Blue</span> will be this year's
  hot color.</p>
    
  <p><a href="index.html">Return to home page</a></p>
</body>
</html>
```

We can't use git commit -a to automatically stage news-1.html because it is an untracked file (as shown in git status).
So, let's use an explicit git add:

```console
$ git add index.html news-1.html 
```

```console
$ git status
On branch news-hotfix
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   index.html
	new file:   news-1.html

```

```console
$ git commit -m "Add 1st news item"
[news-hotfix 049c9d9] Add 1st news item
 2 files changed, 17 insertions(+), 1 deletion(-)
 create mode 100644 news-1.html
```

Text these additions in a browser to make sure that the links work, it is typo free, etc. If everything looks good, we can "publish" the changes by merging them into the stable master branch. Isolating this in a separate branch is not really necessary for our trivial example, but in the real world, this would give you the opportunity to run build tests without touching your stable project.

# 	* [Publish the News Hotfix](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#5-branches-ii-rysgittutorial---content)

Remember that to merge into the master branch, we first need to check it out.

```console
$ git checkout master
Switched to branch 'master'
```

```console
$ git merge news-hotfix
Updating 1a27d0e..049c9d9
Fast-forward
 index.html  |  2 +-
 news-1.html | 16 ++++++++++++++++
 2 files changed, 17 insertions(+), 1 deletion(-)
 create mode 100644 news-1.html
```

Since master now contains the news update, we can delete the hotfix branch:

```console
$ git branch -d news-hotfix
Deleted branch news-hotfix (was 049c9d9).
```

```console
$ git branch
  crazy
  crazy-alt
* master
```

The following diagram reflects our repository's history before and after the merge. Can you figure out why was this a fast-forward merge instead of a 3-way merge?

![Screen Shot 2020-05-25 at 9 40 01](https://user-images.githubusercontent.com/24994818/82822643-bb57bc80-9e6b-11ea-9d72-eb5c7f1d250c.png)

**Also notice that we have another fork in our history (the commit before master branches in two directions), which means we should expect to see another merge commit in the near future**.

# 	* [Complete the Crazy Experiment](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#5-branches-ii-rysgittutorial---content)

Ok, lets finish up our crazy experiment with one more commit.

```console
$ git checkout crazy
Switched to branch 'crazy'
```

Note that the news article is nowhere to be found, as should be expected (this branch is completely isolated development environment).

We will finish up our crazy experiment by adding a news item for it on the home page. **Change the news list in index.html to the following**:

```html
<h2 style="color: #C00">News</h2>
<ul>
  <li><a href="rainbow.html">Our New Rainbow</a></li>
</ul>
```

**Astute readers have probably observed that this directly conflicts with what we changed in the news-hotfix branch**.

**We should not manually add in the other news item because it has no relationship with the current branch**. In addition, there would be no way to make sure the links works because news-1.html does not exist in this branch. This may seem trivial, but imagine the errors that could be introduced had news-hotfix made dozens of different changes.

We will simply stage and commit the snapshot as if there were no conflicts:

```console
$ git commit -a -m "Add news item for rainbow"
[crazy ebb4171] Add news item for rainbow
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Look at those experimental commits (marked with asterisks below)!

```console
$ git log --oneline
* ebb4171 (HEAD -> crazy) Add news item for rainbow
* 4310454 Link index.html to rainbow.html
6a43f42 add CSS stylesheet to rainbow.html
b9f2b14 Merge branch 'master' into crazy
1a27d0e link HTML pages to stylesheet
019e981 Add CSS stylesheet
* 95a36a7 Rename crazy.html to rainbow.html
* e1bc771 add a rainbow to crazy.html
3553479 Revert "Add a crazzy experiment"
* 12e24f0 Add a crazzy experiment
453c8a4 (tag: v1.0) Add navigation links
1047951 t Add blue an orange html files
6a442fc Create index page for the message
```

# 	* [Publish the Crazy Experiment](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#5-branches-ii-rysgittutorial---content)

We are finally ready to merge our crazy branch into master:

```console
$ git checkout master
Switched to branch 'master'
```

```console
$ git merge crazy
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

**This is our first merge conflict**. **Conflicts occur when we try to merge branches that have edited the same content**. Git does not know how to combine the two changes, so it stops to ask us what to do. We can see exactly what went wrong with the familiar git status command.

```console
$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Changes to be committed:
	new file:   rainbow.html

Unmerged paths:
  (use "git add <file>..." to mark resolution)
	both modified:   index.html
```

We are looking at the staged snapshot of a merge commit. We never saw this with the first 3-way merge because we didn't have any conflicts to resolve. **But now, Git stopped to let us modify files and resolve the conflict before committing the snapshot**. The "Unmerged paths" section contains files that have conflict..

Open up index.html and find the section that looks like:

```console
<<<<<<< HEAD
	  <li><a href="news-1.html">Blue Is The New Hue</a></li>
=======
		<li><a href="rainbow.html">Our New Rainbow</a></li>
>>>>>>> crazy
```

**Git went ahead and modified the conflicted file to show us exactly which lines are afflicted**. The format of the above text show us the difference between the two versions of the file. 

The section labeled `<<<<<<< HEAD` show us the version in the current branch, while the part after the `=======` shows the version in the crazy branch.

# 	* [Resolve the Merge Conflicts](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#5-branches-ii-rysgittutorial---content)

We can change the affected lines to whatever we want in order to resolve the conflict. **Edit the news section of index.html to keep changes from both versions**:

```console
<h2 style="color: #C00">News</h2>
<ul>
  <li><a href="news-1.html">Blue Is The New Hue</a></li>
  <li><a href="rainbow.html">Our New Rainbow</a></li>
</ul>
```

**The `<<<<<<<`, `=======`, and `>>>>>>>` markers are only used to show us the conflict and should be deleted**. Next, we need to tell Git that we are done resolving the conflict:

**That's right, all you have to do is add index.html to the staged snapshot to mark it as resolved**. 

```console
$ git add index.html
```

```console
$ git status
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:
	modified:   index.html
	new file:   rainbow.html
```

**Finally, complete the 3-way merge**:

```console
$ git commit 
[master f79223d] Merge branch 'crazy**'
```

**We didn't use the -m flag to specify a message because Git already gives us a default message for merge commits**. It also gives us a "Conflict" list, which can be particularly handy when trying to figure out where something went wrong in a project. Save and close the file to create the merge commit.

The final state of our project looks like the following.

![Screen Shot 2021-03-13 at 17 38 18](https://user-images.githubusercontent.com/24994818/111052704-ec1cd880-8422-11eb-8f1e-ab9e40bc8f64.png)

# [Important conclusions about merging branches when you modify the same file](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#5-branches-ii-rysgittutorial---content)

I tried to practice modifying this README.md file that you are reading, first I created a boldedSentencesModContinuation branch and I modified a section of the file (it was not the same line), I staged and commited, then I went back to master, I modified README.md file again, I worked on a different section of the file, staged and commited. When I tried to merge boldedSentencesModContinuation branch, it was successful, Why? Ok, this is why: I modified the same file, but this modification was not in the same line, so when you merge does not have any problem. Wooooow!

You have to repeat the example modifying the README.md file in the same line.

# 	* [Cleanup the feature Branches](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#5-branches-ii-rysgittutorial---content)

Since our crazy experiment has been successfully merged, we can get rid of our feature branches.

```console
$ git branch -d crazy
Deleted branch crazy (was ebb4171).
```

```console
$ git branch -d crazy-alt
error: The branch 'crazy-alt' is not fully merged.
If you are sure you want to delete it, run 'git branch -D crazy-alt'.
```

As noted in the last module, the git branch -d command will not let you delete a branch that contains unmerged changes. But, we really do want to scrap the alternative experiment, so we will follow the error message's instructions for overriding this behavior:

```console
$ git branch -D crazy-alt
Deleted branch crazy-alt (was d247771).
```

**Because we never merged crazy-alt into master, it is lost forever**. However, the crazy branch is still accessible through its commits, which are now reachable via the master branch. That is to say, it is still part of the structure of the repository's history, even though we deleted our reference to it.

![Screen Shot 2020-05-25 at 19 38 28](https://user-images.githubusercontent.com/24994818/82849830-58901080-9ebf-11ea-9338-d8384871beac.png)

**Fast-forward merges are not reflected in the project history**. This is the tangible distinction between fast-forward merges and 3-way merges. The next module will discuss the appropiate usage of both and the potential complications of a non-linear history.


#   * [Rename Branches Local and Remote](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#5-branches-ii-rysgittutorial---content)

**This is a new note about how to rename branches**. I remember use it when I couldn't rebase a branch over master, so I have to rename my branch as master and master as old-master

Checkout to the desired branch, this apply for local:

```console
Fri Jun 12 ~/iOS/ToDoListApp 
$ git checkout withoutStackViews
Switched to branch 'withoutStackViews'``console

Fri Jun 12 ~/iOS/ToDoListApp 
$ git branch -m old-master
```

Then check the list of branches
```console
$ git branch
* old-master
  withoutStackViews
```

Now change to the branch that you are going set as master

```console
$ git checkout withoutStackViews
Switched to branch 'withoutStackViews'

Fri Jun 12 ~/iOS/ToDoListApp 
$ git branch -m master
```

Check the new list of branches:

```console
$ git branch
* master
  old-master
```

To push this change remotely:

```console
Fri Jun 12 ~/iOS/ToDoListApp 
$ git push origin :master old-master
Total 0 (delta 0), reused 0 (delta 0)
To https://github.com/c4arl0s/ToDoListApp.git
 - [deleted]         master
 * [new branch]      old-master -> old-master
```

**As you can see in Git hub, the old-master keeps appearing, the withoutStackViews branch also, Git didn't allow me to delete it from command line**.

![Screen Shot 2020-06-12 at 12 55 19](https://user-images.githubusercontent.com/24994818/84532552-09622200-acac-11ea-93d6-18cbb079870a.png)

git push origin :old-name new-name

# 	* [Conclusion](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#5-branches-ii-rysgittutorial---content)

This module demonstrate the three most common uses of Git Branches:

1. To develop long-running features (crazy)
2. To apply quick updates (news-hotfix)
3. To record the evolution of a project (master)


# 	* [Quick Reference](https://github.com/c4arl0s/5BranchesIIRysGitTutorial#5-branches-ii-rysgittutorial---content)

```console
$ git commit -a -m "messageToCommit"
```

Stage all tracked files and commit the snapshot using the specified message.

```console
$ git branch -D branchName
```

Force the removal of an unmerged branch (be careful: it will be lost forever).

