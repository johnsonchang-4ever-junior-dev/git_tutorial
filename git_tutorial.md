# Git Tutorial

## Create a Repo Folder

Create a new repo for this project on GitHub.com and call it `demo_repo`, choosing the **public** option instead of the default private.  
Create another repo for this project on GitHub.com and call it `demoTeam_repo`, also choosing the **public** option.

Clone that repository onto your local machine, inside the `repos` folder using:
```bash
git clone <repo-link>
```

Now `cd` into the `demo_repo` project directory (because Git commands must be run from inside your project’s folder).

---

## 🪴 1. Start Working Locally

You’re writing code, creating files, fixing bugs — all on your own computer.  
Nothing is uploaded online yet.

---

## 2. Save “Checkpoints” (Commits)

While you’re coding, you’ll reach small milestones:

- “I finished the login form.”  
- “I fixed the validation bug.”  
- “I added comments to the code.”

Each of these moments is a good time to **save a group of changes** in Git.  
You can add a short message describing what you did for future reference.

The **Working Directory** is where you edit files.  
The **Staging Area** is where you collect changes to be committed next.

---

### `git add .`

> “Tell Git to **track all changes** (new, modified, or deleted files) in the **current folder** and all its subfolders.”

The `.` means “this directory.”

`git add` takes a snapshot from the **working directory** to the **staging area**.

---

### Can I Replace `.` with a File or Folder Name?

Yes, you can.

Examples:
```bash
git add index.html         # Add one file
git add index.html style.css   # Add multiple files
git add src/               # Add an entire folder
```

---

Back to commits.  

Set up your `README.md` file and write a brief introduction describing what the project is and what skills you’ll demonstrate.

Create `index.html` and `lasagna.html`.

Move everything to the staging area either with `.` or by adding files individually.  
Then add an explanation for your work using `git commit`.

```bash
git add .
git commit -m "Create README.md, index.html, and lasagna.html"
```

That’s the end of the commit part — now we’ve staged and recorded our changes.

---

## 3. Push Changes to GitHub

```bash
git push origin main
```

Here:
- `origin` is the **nickname** Git gives to the **remote repository** you cloned or connected.  
  You can set it manually:
  ```bash
  git remote add origin https://github.com/username/project.git
  ```
- This means:  
  > “Hey Git, whenever I say *origin*, I actually mean this GitHub URL.”

You can have multiple remotes — each with a different name or URL.

Examples:
```bash
git remote add backup https://gitlab.com/username/project.git
git push backup main
git push team main
```

---

## 4. What “Origin” Really Is

When you **clone** a repository:
```bash
git clone https://github.com/username/project.git
```

Git automatically:
- Creates a **remote connection** to that URL.
- Names it **`origin`** by default.

So `origin` = “the place I originally cloned this repo from.”

To rename:
```bash
git remote rename origin newOriginName
```
To add another remote:
```bash
git remote add team https://gitlab.com/username/project.git
```

Check your remotes:
```bash
git remote -v
```
(`-v` stands for **verbose** — “show more details.”)
You’ll see:
```
origin  https://github.com/username/project.git (fetch)
origin  https://github.com/username/project.git (push)
```

---

## 5. Explanation of Fetch and Push

### Fetch:
```bash
git fetch origin main
```
> “Go to the remote named `origin` and **download** the newest commits from the `main` branch — but don’t touch my local files yet.”

After fetching:
```
Your local main       → old commits  
origin/main (fetched) → new commits from GitHub
```

### Merge:
```bash
git merge origin/main
```
> “Take the commits from `origin/main` (the local copy of the remote main branch) and merge them into my current branch.”

### Shortcut (Fetch + Merge):
```bash
git pull origin main
```

---

### Push:
```bash
git push origin main
```
> “Push my local branch named `main` up to GitHub (`origin`) and update (or create if not existing) a branch called `main` there.”

⚠️ The `main` branch is sacred — it’s what’s deployed to users or servers.  
Junior and senior developers **do not push directly** to `main`.  
They work on **feature branches**.

---

## 6. Feature Branches

If you’re working on another branch locally, e.g. `feature-login`, you can push it too:

```bash
git push origin feature-login
```
> “Push my local branch named `feature-login` up to GitHub (`origin`) and create (or update) a branch called `feature-login` there.”

Or push to another remote:
```bash
git push backup feature-login
```
> “Take my local branch `feature-login` and upload it to the remote repository named `backup`.”

---

## 7. Create and Switch Branches

Create a new branch (but you’ll still be on your old one):
```bash
git branch feature-login
```

Switch between branches:
```bash
git switch feature-login
git switch main
```
or (older syntax):
```bash
git checkout main
```

Create **and immediately switch**:
```bash
git switch -c feature-login
```
or:
```bash
git checkout -b feature-login
```

See all branches:
```bash
git branch
```

Output example:
```
* feature-login
  main
```
The `*` indicates the branch you’re currently on.
