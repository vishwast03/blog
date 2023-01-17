# Practical Guide to using Git for Beginners

**Mike:** I made some changes in my [source code](https://en.wikipedia.org/wiki/Source_code) and my application broke. Now, I can’t undo the changes that I made earlier.

**VT:** You should have used git.

**Mike:** Git? What is that?

**VT:** Git is a version control system, which tracks the history of changes. As you make changes to the project, any earlier version of the project can be recovered at any time.

**Mike:** This sounds great! But, how can I use it?

**VT:** OK! I will show you.

## Step 1: Install git

**VT:** First, download git from http://git-scm.com and install it on your computer.

**Mike:** OK! Done!

## Step 2: Configure git

**VT:** Configure user information for git. This helps to set your details to all your commits.

Open a terminal (or command prompt) and run the following commands:

```bash
git config --global user.name "[name]"
git config --global user.email "[email address]"
```

> Make sure to replace `[name]` and `[email address]` with your real `name` and `email address` respectively.

**Mike:** Done!

## Step 3: Create a new git repository

**Mike:** But what is a git repository?

**VT:** A Git repository is the `.git/` folder inside a project. This repository tracks all changes made to files in your project and builds a history over time.

**Mike:** But I don’t have a `.git/` folder.

**VT:** First, you have to initialize a git repository.

Open a terminal (or command prompt) in an empty folder (or in your project folder) and run this command:

```bash
git init
```

**Output:**

```bash
Initialized empty Git repository in /path/to/your/Project/.git/
```

**Mike:** Oh, now I got the `.git``/` folder. What's next?

> If you are not seeing the `.git/` folder, turn on the `Show Hidden Files` option. Usually, it is turned on with `Ctrl+H`.

**VT:** That's it. Now you have a git repository where all the changes that you make will be tracked by git.

Let's make some changes now.

## Step 4: Making changes

**VT:** Make a new file (or change the existing one, if any) in the folder where you initialized the git repository.

**VT:** Let's make an HTML file (`index.html`), or download an HTML file from [here](https://drive.google.com/uc?id=1wtBer4YwmexsMFsSzgSssADmoJe9Vw6N&export=download).

![Screenshot of the .git/ folder and index.html](https://cdn.hashnode.com/res/hashnode/image/upload/v1673932895833/SnPB8TBJV.png align="left")

**VT:** Now, you can run this command to see your changes tracked by git.

```bash
git status
```

**Output:**

```bash
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	index.html

nothing added to commit but untracked files present (use "git add" to track)
```

**Mike:** Done! But what are `branch master` and `commits` mentioned in the output?

**VT:** Hold on! We will talk about branches in a moment. Let's first talk about commits.

## Step 5: Committing changes

**VT:** Commits record file snapshots permanently in the version history.

Let's see how we can commit our changes to the git repository.

**VT:** First, we have to add our change to the "staging area".

**Mike:** What is the "staging area"?

**VT:** The staging area is like a rough draft space, it's where we can add a version of a file (or files) that we want to save in our next commit.

**VT:** Let's add our `index.html` file to the "staging area".

Run the following command:

```bash
git add index.html
```

**OR,** we can add all the changes to the staging area at once by running this command:

```bash
git add .
```

**VT:** Now, if we run the command `git status`, we will get an output something like this:

```bash
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   index.html
```

**VT:** We can commit our stagged changes by running the command:

```bash
git commit -m "[descriptive message]"
```

> We can add a message to describe our changes by replacing `[descriptive message]` in the above command.

**Output:**

```bash
[master (root-commit) db027ec] added index.html
 1 file changed, 13 insertions(+)
 create mode 100644 index.html
```

**VT:** We have successfully committed our change. We can see all our commits by running the command:

```bash
git log
```

**Output:**

```bash
Author: Vishwas Tyagi <vishwast8126@gmail.com>
Date:   Mon Aug 15 19:06:57 2022 +0530

    added index.html
```

**Mike:** That's great! But what if I made a commit by mistake? How would I undo any commit?

## Undo commits

**VT:** We can undo any commit at any time by running the `git reset` command.

**VT:** Let's see it in action.

Make a change to the `index.html` file to make another commit.

Add the following line to the `index.html` file:

```xml
<p><strong>Making a change.</strong></p>
```

Save the file.

Now, on running the `git status` command we will get the following output:

```bash
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
```

**VT:** Now, let's commit our change.

Run the following commands:

```bash
git add index.html
git commit -m "updated index.html"
```

**VT:** Now as we have committed all our changes.

Suppose we made the last commit by mistake and we want to undo that commit.

First, we have to find the **hash id of the commit to which we want to go back.**

**VT:** Run the `git log` command to list all the commits.

```bash
commit 3d52d9625962f3147feb760ff7caccbaa2828b36 (HEAD -> master)
Author: Vishwas Tyagi <vishwast8126@gmail.com>
Date:   Mon Aug 15 21:24:29 2022 +0530

    updated index.html

commit db027ecc1d3bd09298db3b0305375047b1e31894
Author: Vishwas Tyagi <vishwast8126@gmail.com>
Date:   Mon Aug 15 19:06:57 2022 +0530

    added index.html
```

**VT:** As we want to undo the last commit, we want the hash id of the commit before the last commit.

![Screenshot showing the commit hash id](https://cdn.hashnode.com/res/hashnode/image/upload/v1673932897275/dAcxoMG-p.png align="left")

Run the following command to undo the last commit:

```bash
git reset [commit_hash_id]
```

> Replace `[commit_hash_id]` with the hash id of the commit to which you want to go back.

**Output:**

```bash
Unstaged changes after reset:
M	index.html
```

**VT:** We have undone the commit and all the changes are sent back to the unstaged area.

**Mike:** Oh, I got it.

**VT:** If you want to discard those changes, you can run the following command:

```bash
git restore index.html
```

**Mike:** Great! I got my `index.html` file restored to the initial state.

**Mike:** But what are the "branches" that you mentioned earlier?

**VT:** I think, it's the right time to talk about "branches."

## Git Branches

![visual representation of git branches](https://cdn.hashnode.com/res/hashnode/image/upload/v1673932899180/1Y-6ENjjJ.png align="left")

**VT:** In Git, a branch is a new/separate version of the main repository.

Let's say we have a large project, and we need to work on a new feature.

We can create a new branch (let's say `feature`) and then we can work on that feature without affecting the main branch.

```bash
git branch [branch_name]
```

If we are satisfied with our work, we can merge our branch with the main branch.

If not, then we can return to the main branch and discard the changes we made on the `feature` branch.

**Mike:** I am getting it, but I want to see it in action.

**VT:** Ok, let's get into it.

Suppose we want to add an image to our `index.html`.

Create a new branch with the name `image` by running the following command:

```bash
git branch image
```

We can list all the branches by running the following command:

```bash
git branch
```

**Output:**

```bash
  image
* master
```

It lists all the branches in the current git repository.

Here, the `master` is the default main branch.

The asterisk `*` shows which branch we are currently working on.

To switch branches, run the following command:

```bash
git checkout image
```

**Output:**

```bash
Switched to branch 'image'
```

**VT:** Now, we can make changes and they will affect only the current branch (`image`). They will not affect the main branch (`master`).

Add the following line to `index.html`:

```xml
<img src="https://images.unsplash.com/photo-1471897488648-5eae4ac6686b" height="300" width="200">
```

Commit the changes:

```bash
git add .
git commit -m "added image in index.html"
```

**VT:** Our change is committed but it is only in the `image` branch. It will not affect the `master` branch.

We can see this by switching the branch to `master`.

```bash
git checkout master
```

**VT:** If we inspect the `index.html` file after switching to the `master` branch, we can see that the image we added in the `index.html` file is not there.

This is because the image was added in the `image` branch.

**Mike:** How would I merge both branches?

## Merging branches

![visual representation of git branch merge](https://cdn.hashnode.com/res/hashnode/image/upload/v1673932900485/_s3o3sTGd.png align="left")

**VT:** If we are satisfied with the changes we made in the separate branch, we can merge that branch with the `master` branch by running `git merge [branch_name]`.

First, switch to the branch `master`:

```bash
git checkout master
```

Then run the following command to merge the branch `image` to the branch `master`:

```bash
git merge image
```

**Output:**

```bash
Updating fa6e17e..c5a4da8
Fast-forward
 index.html | 1 +
 1 file changed, 1 insertion(+)
```

## Deleting a branch

**VT:** If we no longer want a branch and we want to delete it, we can simply run the `git branch -d [branch-name]` command.

To delete the branch `image` in our project:

```bash
git branch -d image
```

**Output:**

```bash
Deleted branch image (was c5a4da8).
```

**VT:** That's all.

**Mike:** Oh, that's a lot for me, but by practicing it a few times, I can make it through.

## Further reading...

* [Git Handbook - GitHub Guides](https://docs.github.com/en/get-started/using-git/about-git)
    
* [Git Cheat Sheet - GitHub](https://training.github.com/downloads/github-git-cheat-sheet.pdf)
    

## Summary

Git is a free and open-source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

In this article, you learned about git repositories, git commits, git branches, and how the whole process of version control works.

I hope you enjoyed the article and learned something new. If you want, you can also follow me on [LinkedIn](https://www.linkedin.com/in/vishwas-tyagi/) or [Twitter](https://twitter.com/vishwast03).

Cheers and see you in the next one! ✌️