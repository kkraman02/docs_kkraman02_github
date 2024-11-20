---
title: GitHub
date: 2024-07-10 22:02:56
categories: GitHub
tags: GitHub Commands
---



# What is GitHub?

GitHub is a platform where developers store and share their code. Think of it like a social network for programmers, but instead of sharing photos or updates, they share software projects. It helps developers collaborate on projects, track changes, and manage different versions of their code. It's widely used for open-source projects and by teams working on software development together.

## 1. Installing and Getting Started with Git in Linux

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install git
git --version
```

### 1.2. Configuring Git

After installing Git, you should configure it with your name and email. This information is used to identify your commits.

1. **Set Your Name:** Replace `Your Name` with your actual name:

   ```bash
   git config --global user.name "Your Name"
   ```
   
2. **Set Your Email:** Replace `your.email@example.com` with your email address:

   ```bash
   git config --global user.email "your.email@example.com"
   ```

### 1.3. Cloning an Existing Repository:

1. **Navigate to the Directory:** Open Terminal and navigate to the directory where you want to clone the repository. For example:

   ```bash
   cd /path/to/your/desired/directory
   ```

2. **Clone the Repository:** Use the `git clone` command followed by the URL of the GitHub repository you want to clone. For example, to clone a repository named `example_repo` from GitHub:

   ```bash
   git clone https://github.com/username/example_repo.git
   ```

   Replace `username` with the GitHub username and `example_repo` with the name of the repository you want to clone.

3. **Navigate into the Cloned Repository:** After cloning, navigate into the cloned repository:

   ```bash
   cd example_repo
   ```



## 2. Branching in the repositories
### 2.1. Creating a new branch

   ```bash
   git branch --all
   git checkout -b new-branch-name
   git checkout new-branch-name
   ```

### 2.2. Deleting a branch

Once you've merged your changes from a branch and no longer need it, you can delete it:

   1. **Delete Locally:**

      ```bash
      git branch -d branch-name
      ```

      This deletes the branch named `branch-name` locally, but only if its changes have been merged into another branch.

   2. **Delete Remotely:** If you've pushed the branch to GitHub and want to delete it there too:

      ```bash
      git push origin --delete branch-name
      ```

      This deletes the branch named `branch-name` on the remote repository (`origin` on GitHub).

### 2.3 Add Files

Start tracking files by adding them to the staging area:

   ```bash
   git add <file>  # Replace <file> with the actual filename or use '.' to add all files
   ```

### 2.4 Commit Changes

Commit the staged changes to the repository:

   ```bash
   git commit -m "Initial commit"  # Use a meaningful commit message
   
   template:
   <type>[optional scope]: <description>
   
   [optional body]
   
   [optional footer(s)]
   ```

## 3. Merging the branches

**Navigate to main:** First, ensure you are on the branch into which you want to merge changes. Typically, this is the `main` branch:

```bash
git checkout main
git fetch origin
```

**Fetch Latest Changes:** It's a good practice to fetch the latest changes from the remote repository before merging:

```bash
git fetch origin
```

**Merge Branch:** Merge the changes from the branch you want to merge (let's say `devpt`) into `main`:

```bash
git merge devpt
```



## 4. Creating patches

**List all commits on a specific branch:** Replace `<branch-name>` with the name of the branch you're interested in, such as `devpt` in your case.

```bash
git log devpt (or)
git log -n 10  # Shows the last 10 commits
```

Generate patches for the commits:

```bash
git format-patch <commit_hash> (or) # for a particular
git format-patch <commit_hash_from>..<commit_hash_to> # for 2 or more commits
```

### 4.1 Applying the patch files

If you have `.patch` files generated using `git format-patch` or another method, you can apply them using `git apply` or `git am`.

#### 4.1.2 Using git apply

1. **Navigate to your Git repository:**

   ```bash
   cd /path/to/your/repository
   ```

2. **Apply the patch using `git apply`:**

   ```bash
   git apply path/to/your/patchfile.patch
   ```

   Replace `path/to/your/patchfile.patch` with the actual path to your patch file.



## 5. Reset the repo to the specific commit

Use `git reset` to move the `HEAD` pointer and working directory to the specific commit you want to start from. This effectively "rewinds" your repository's state to that commit.

```bash
git log devpt
git reset --hard <commit-hash>
```

Replace `<commit-hash>` with the hash of the commit you want to start from. This hash uniquely identifies each commit and can be found using `git log`.
