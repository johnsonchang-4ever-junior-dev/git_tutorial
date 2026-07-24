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

## 1. Start Working Locally

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

You use git status to inspect your current workspace before and after staging files.

```bash
git status
```

you will see something like this before staging:

```
On branch main
Your branch is up to date with 'origin/main'.
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   git_tutorial.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   git_tutorial.md
```

Now you can see what commits have already been saved in this repo with

```bash
git log
```

or for a more compact view:

```bash
git log --oneline
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
  > “Hey Git, whenever I say _origin_, I actually mean this GitHub URL.”

You can have multiple remotes — each with a different name or URL.

Examples:

```bash
git remote add backup https://gitlab.com/username/project.git
git push backup main
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


Here's the full recap, start to finish.

## 1. Download the Git auto-complete script

```bash
curl -o ~/.git-completion.bash https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash
```

- `curl` = fetches something from the internet
- `-o ~/.git-completion.bash` = save it in your home folder, named with a dot (hidden file)

## 2. Open your profile file with nano

```bash
nano ~/.bash_profile
```

This opens your Terminal's "startup checklist" file for editing.

## 3. If you got "Permission denied"

Means the file was owned by `root`, not you. Fix:

```bash
sudo chown johnsonchang ~/.bash_profile
```

- `sudo` = do this as admin (asks for your Mac password)
- `chown johnsonchang` = change the file's owner to you

Then confirm:

```bash
ls -la ~/.bash_profile
```

Should show `johnsonchang` as owner now.

## 4. Add the loading snippet

Reopen with `nano ~/.bash_profile`, go to the **bottom**, below the conda block, paste:

```bash
# If the completion script exists, load it into memory
if [ -f ~/.git-completion.bash ]; then
  . ~/.git-completion.bash
fi
```

Save: `Ctrl+X` → `Y` → `Enter`.

## 5. Restart Terminal and test

Close the window, open a new one. Then test:

```bash
git co[Tab]
```

Should hesitate between `commit`/`config` — type one more letter and Tab again to confirm.

## 6. Set your Git identity (separate, one-time setup)

```bash
git config --global user.name "Johnson Chang"
git config --global user.email "you@example.com"
git config --global core.editor "code --wait"
git config --global color.ui true
```

Check it saved correctly:

```bash
cat ~/.gitconfig
```

---

That's the full chain: **download script → edit profile file → fix permission if blocked → load script → restart → test → set identity.**


Four topics here. Let's go one at a time.

## 1. Starting a Git project (`git init`)

Think of `git init` like putting a security camera in a room — it starts watching a folder for changes, but you need the folder to exist first.

**Step 1 — Make a project folder**

```bash
cd ~/Documents          # go into Documents
mkdir first_git_project # make a new folder
cd first_git_project    # go inside it
```

**Step 2 — Turn on Git tracking**

```bash
git init
```

You'll see: `Initialized empty Git repository in .../first_git_project/.git/`

Run `ls -la` (the `-a` shows hidden dot-files too) and you'll spot a new `.git` folder — that's the camera. It's invisible by default because it starts with a dot.

## 2. What's inside `.git`

```bash
ls -la .git
```

This folder is Git's **entire brain** for this project — every commit, every branch, every setting. Nothing else, nowhere else.

- `config` → project-only settings (like your global ones, but just for this folder)
- `branches`, `hooks`, `objects`, `refs` → internal machinery, leave these alone

**Important:** delete `.git` and you delete *all* Git history for that project — like smashing the security camera's hard drive. The files you were working on stay, but every past version is gone.

(Side note comparing to SVN, an older tool: SVN scatters tiny tracking files into every folder, so removing it means hunting them all down. Git keeps it all in one tidy `.git` box — easier to remove cleanly.)

## 3. Your first commit — the 3-step loop

This is the core rhythm of Git, repeated forever: **change → add → commit**.

**Step 1 — Make a change**

Create a file (use a code editor like VS Code, not Word — Word adds hidden formatting Git doesn't want).

`first_file.txt` containing: `This is my first file.`

**Step 2 — Stage the change (`git add`)**

```bash
git add .
```

- `.` means "current folder" → "hey Git, notice every change in here"
- Staging = putting items in a box, ready to seal — not sealed yet

**Step 3 — Commit (`git commit`)**

```bash
git commit -m "Initial commit"
```

- `-m` = short for **message**
- This seals the box permanently into your project's history

That's it — **change, add, commit**. You'll do this loop constantly.

## 4. Viewing history (`git log`)

```bash
git log
```

Shows every commit, newest first. Each entry has:

| Field | What it is |
|---|---|
| commit ID | A unique fingerprint for that commit |
| Author | Pulled from your `git config` name/email |
| Date | When it was committed |
| Message | Your `-m` text |

**Useful filters:**

```bash
git log -n 5                        # only show the last 5 commits
git log --since=2020-01-01          # commits made after this date
git log --until=2020-01-01          # commits made before this date
git log --author=Johnson            # only commits by matching name
git log --grep="bug fix"            # search commit messages for this text
```

`--grep` searches commit **messages** — this is why writing clear, descriptive messages matters. It lets future-you search your whole history by topic later.

---

Four big ideas here. Let's go slow, one at a time.

## 1. The Three Trees

"Tree" just means a file structure — folders inside folders, like branches. Git uses **three** of these, working together.

**Most other tools use two:**
- **Repository** — the permanent saved history
- **Working copy** — the files on your hard drive you're actually editing

Problem with just two: if you edit a file, your working copy and the repository now disagree, and there's no in-between step to organise things.

**Git adds a third tree in the middle: the Staging Index.**

Think of it like packing a suitcase before a trip:
- **Working directory** = your clothes scattered on your bed (edited, but not organised)
- **Staging index** = clothes you've picked up and put in the suitcase (chosen, ready)
- **Repository** = the suitcase zipped shut and put away (permanent, saved)

Why bother with the middle step? Say you changed 10 files, but only 5 of them are ready to save together as one logical change. Staging lets you pick just those 5, leaving the other 5 on the "bed" for later.

## 2. The Git Workflow (a, b, c example)

This is the three trees in motion, repeated over and over:

```bash
# Version 1 of file.txt exists in working directory (call it change "a")
git add file.txt      # move it: working directory → staging index
git commit -m "a"      # move it: staging index → repository
```

Now repository has "a" saved. Edit the file again (call it "b"):

```bash
git add file.txt
git commit -m "b"
```

Now the repository holds **both** "a" and "b" — like a stack of saved snapshots, oldest at the bottom.

Do it again for "c" — same steps. This add → commit loop is the heartbeat of using Git.

Note: `git add file.txt` (a specific file) vs `git add .` (everything) — same command, just choosing how much to grab.

## 3. Hash Values (SHA-1)

Git doesn't call your commits "a", "b", "c" — it gives each one a unique fingerprint called a **hash** (specifically, a **SHA-1** hash).

**What's a hash, simply?**

Imagine a machine: you feed in *any* data, and it spits out a fixed-length code — always the *same* code for the *same* input, but a *totally different* code if even one letter changes.

- Git feeds in: your file changes + author + message + parent commit
- Out comes: a 40-character code like `5c15e8bd...` (using digits 0-9 and letters a-f — that's what "hexadecimal" means)

**Why this matters — data integrity:**

Because the message and parent commit are part of what gets hashed, commits **link together like a chain**:

```
Commit A (5c15e8) → Commit B (points back to A) → Commit C (points back to B)
```

If someone secretly edited Commit A afterward, A's hash would change — which breaks the chain, because B was pointing to A's *original* hash. So tampering is easy to detect, like a wax seal that cracks if someone opens the envelope.

You don't need to know how SHA-1 math works — just that it's Git's fingerprint system, and people will call it "the SHA" in conversation.

## 4. The HEAD Pointer

**HEAD** = a marker for "where you currently are" in your project's history.

**Analogy — a cassette tape recorder:** the little playback/record head sits at a spot on the tape. Wherever it's sitting, that's where recording starts if you press record again. HEAD works the same way for commits — it marks where your *next* commit will attach.

**Walking through it:**

1. First commit `5c15e8` → HEAD points to it
2. Make a new commit → new commit's parent = `5c15e8`, HEAD **moves** to point to the new one
3. Repeat — HEAD always sits on the most recent commit of your current branch

**Where to actually see it:**

```bash
cat .git/HEAD
```

This might show:
```
ref: refs/heads/master
```

Meaning: "go look inside `refs/heads/master` for the real answer." Then:

```bash
cat .git/refs/heads/master
```

This shows the actual SHA value — and it'll match the top entry in `git log`.

You won't move HEAD by hand day-to-day — Git handles it — but this matters a lot later once you start using **branches** (separate parallel histories), since each branch has its own HEAD position.

---

Quick summary chain: **working directory → (git add) → staging index → (git commit) → repository**, each commit gets a unique SHA fingerprint, and **HEAD** marks your current spot in that chain.


Six topics here. Let's go through each carefully, with every command.

## 1. Adding new files

**Check the state of things first:**

```bash
git status
```

This tells you three possible things about each file: untracked, staged, or clean. Right now it should say "nothing to commit, working tree clean."

**Create two new files** (in your text editor): `second_file.txt`, `third_file.txt`.

**Check status again:**

```bash
git status
```

Now it lists them as **untracked** — meaning Git sees they exist, but isn't watching them yet. Any changes you make to them right now won't be recorded anywhere.

**Stage one file:**

```bash
git add second_file.txt
```

This moves it: working directory → staging index.

**Check status:**

```bash
git status
```

Now it says "changes to be committed" for `second_file.txt`, and still shows `third_file.txt` as untracked.

**Commit it:**

```bash
git commit -m "Add second file to project"
```

**Repeat for the third file:**

```bash
git add third_file.txt
git commit -m "Add third file to project"
```

**Confirm everything's clean:**

```bash
git status
```

## 2. Editing tracked files

Edit `first_file.txt` — change the text inside it, save.

```bash
git status
```

This time it says "**changes not staged for commit**" — different wording from "untracked," because Git already *knows* this file (it's in the repository), it just sees the working copy no longer matches.

Stage and commit it the exact same way as before:

```bash
git add first_file.txt
```

**Key insight:** Git doesn't care if a change is a *new file* or an *edit* — both are just "changes." `git add` treats them identically.

You can also edit **multiple files** before committing:

Edit `second_file.txt` and `third_file.txt`, save both, then:

```bash
git status
```

Notice it now shows two sections — one for staged changes, one for unstaged changes.

Stage just one:

```bash
git add second_file.txt
git commit -m "Made changes to first and second files"
```

Then handle the last one:

```bash
git add third_file.txt
git commit -m "Modified the text of the third file"
```

Point of this section: staging lets you **group changes selectively** into one commit, even if you edited many files at once.

## 3. Viewing changes — `git diff`

Edit `first_file.txt` again (add some lines), save.

```bash
git status
```

This tells you *that* something changed, but not *what*. For that:

```bash
git diff
```

This runs the Unix `diff` tool — think of it as a "spot the difference" checker between two versions of text.

Reading the output:
- `-` (red) = line removed
- `+` (green) = line added
- A `-` line followed by a `+` line = that line was **changed** (old removed, new added)

If you edit **multiple files** at once, `git diff` shows each file's changes one after another, only showing the lines that actually changed — not the whole file.

**Important default behaviour:** `git diff` (no options) compares your **working directory against the staging index** — not against the repository.

## 4. Viewing only staged changes — `git diff --staged`

Say you've edited `first_file.txt` and `third_file.txt`, then stage just one:

```bash
git add first_file.txt
```

Now run:

```bash
git diff
```

It only shows changes for `third_file.txt` — because that's still unstaged (working dir vs staging). `first_file.txt`'s changes have "moved on" and no longer show here.

To see what's actually **waiting in staging** (staging vs repository), use:

```bash
git diff --staged
```

There's an older, equivalent name for this flag:

```bash
git diff --cached
```

Same result — `--staged` is just a friendlier, newer name for the same thing. You'll see both used in the wild.

**Cheat sheet:**
| Command | Compares |
|---|---|
| `git diff` | Working directory ↔ Staging |
| `git diff --staged` | Staging ↔ Repository |

## 5. Deleting files

Create two throwaway files, add and commit them normally:

```bash
git add .
git commit -m "Adds files to delete soon"
```

**Method 1 — delete manually, then tell Git**

Drag `file_to_delete1.txt` to Trash (or delete it any normal way).

```bash
git status
```

Git notices it's missing from your working directory. To record that deletion officially:

```bash
git rm file_to_delete1.txt
```

Wait — this seems odd since the file's already gone. What `git rm` does here is just **stage the deletion** (like `git add`, but for a removal).

```bash
git commit -m "Delete first file"
```

**Method 2 — let Git do the deleting**

```bash
git rm file_to_delete2.txt
```

This does two things **in one step**:
1. Actually deletes the file from your hard drive (permanently — not sent to Trash)
2. Stages that deletion

```bash
git status    # already shows it staged, ready to commit
git commit -m "Delete second file"
```

**Which to use?** If you might still want the file sitting around outside the project (e.g. moved to Desktop), delete it manually first. If you're sure you want it gone for good, `git rm` is quicker (one command instead of two actions).

## 6. Moving / renaming files

Renaming a file **is** moving it — a "move" is just giving something a new file path, even if that path is in the same folder.

**Method 1 — rename manually, then tell Git**

Rename `first_file.txt` → `primary_file.txt` using Finder/File Explorer.

```bash
git status
```

Git sees this as **two separate events**: one file deleted, one new untracked file — it doesn't yet know they're related.

```bash
git add primary_file.txt
git rm first_file.txt
git status
```

*Now* Git checks: are these two changes (one delete, one add) similar enough content-wise (roughly 50%+ match) to guess it's a rename? If yes, status shows "**renamed**" instead of two separate changes.

**Method 2 — let Git do the rename directly**

```bash
git mv second_file.txt secondary_file.txt
```

One command does both: renames the actual file on disk **and** stages it as a rename.

```bash
git status   # already shows "renamed", ready to commit
```

**Moving into a folder works the same way:**

```bash
git mv third_file.txt first_folder/third_file.txt
```

Then commit everything:

```bash
git commit -m "Reorganized file names"
```

---

**The big theme across all six of these:** Git doesn't really care whether something is "new," "edited," "deleted," or "renamed" — it all boils down to the same loop: **make a change → `git add` (or `git rm`/`git mv`, which auto-stage) → `git commit`.**


# Part 1: Setting Up & Tracking Changes

**1. Initialise Git in a project**

Think of `git init` like putting a security camera in a room. Before you run it, Git isn't watching anything — no camera, no recordings.

```bash
cd explore-california      # walk into the project folder
ls -la                     # show ALL files, even hidden ones
git status                 # "not a git repository" — no camera yet!

git init                   # installs the camera (.git folder)
git status                 # now it sees files, but nothing recorded yet
```

- `git log` errors here because there's no recording yet — nothing's been committed.
- `git add .` → puts everything in the "about to be saved" box (staging).
- `git commit -m "Initial commit"` → takes the first snapshot.

**Key idea:** each project's `.git` folder is its own separate camera system. Projects don't share history.

---

**2. Making edits & viewing them**

You edit files normally (like changing a phone number in the footer). Then:

```bash
git status              # "hey, these files changed"
git diff                # shows exactly what changed, old vs new
git diff --color-words  # same thing, but only highlights the CHANGED WORDS
                         # (great for long paragraphs — no scrolling through unchanged text)
```

Type `q` to quit the diff viewer (it opens a scrollable page-by-page view called a **pager**).

---

**3. Stage + commit shortcut**

Normally it's two steps: `git add` (stage) then `git commit` (save snapshot).

```bash
git commit -a -m "Edits support phone number"
# same as: git commit --all -m "..."
```

⚠️ Two catches:
- It grabs **every tracked file's changes** — even ones you forgot about. Careful!
- It **won't** include brand new files. Those still need `git add` first.

---

**4. Viewing an old commit**

```bash
git log                  # see list of commits, each with an ID (called a SHA)
git show 1c16945          # shows what changed in that specific commit
git show 1c16945 --color-words   # same, but cleaner highlighting
```

You only need the first 6–8 characters of the SHA — like a nickname, Git's smart enough to know which commit you mean.

---

**5. Comparing two commits**

```bash
git diff <older-SHA>..<newer-SHA>
```

This is like holding up two photos and asking "what's different between these two?" — not just one commit's changes, but everything between two points in time.

Bonus: `HEAD` always means "my most recent commit" — so `git diff <old-SHA>..HEAD` works too.

---

# Part 2: Good Habits — Messages & Atomic Commits

**6. Multi-line commit messages**

So far we used `-m "short message"`. But sometimes one line isn't enough to explain a change.

```bash
git commit -a
# don't add -m this time!
```

This opens your text editor and waits. Type like this:

```
Minor text edits

Client emailed changes to the Explorers page.
```

- First line = short summary (like a headline)
- Blank line = convention (Git expects this gap)
- Rest = extra detail

```bash
git log             # shows full message
git log --oneline   # shows ONLY the first line of each commit — nice and tidy
```

Think of the first line as a book's title, and the rest as the blurb on the back.

---

**7. Atomic commits — the big lesson**

"Atomic" = smallest possible, related-to-one-thing-only. Like an atom: a basic building block, not a mixed bag.

**Why bother?**
- Easier to understand later
- Easier to find bugs
- If a teammate wants just ONE of your changes, they can grab just that commit — not everything mixed together

**Example — two unrelated changes at once:**
- Renaming a file (`tour_detail_backpack.html` → `tour_detail_backpack_cal.html`) + fixing links to it
- Removing contractions on the Contact page

These are *different topics*, so they should be **two separate commits**, not one.

```bash
# Stage ONLY the tours-related files
git add tours/tour_detail_backpack_cal.html
git add tours/

git status   # tours = staged (green), contact.html = not staged yet

git commit -m "Changes filename of backpack tour and related links"

# NOW handle the second, unrelated change
git commit -a -m "Remove contractions from Contact page"
```

**Rule of thumb:** if you can describe your commit message with "and" in it ("fixed the bug **and** changed the colour"), it's probably two commits, not one.

---

**8. Renaming files with Git**

```bash
git mv tours/tour_detail_backpack.html tours/tour_detail_backpack_cal.html
```

This renames it AND tells Git about it in one step — cleaner than renaming in Finder/Explorer and having Git figure it out itself.

---

**9. The challenge — how it was solved (worked example)**

Client wanted 3 things:
1. Big Sur price: $620 → $750
2. California Calm price: $250 → $270
3. Explorers page title: "Come Make A Few Friends" → "Make New Friends"

**The trap:** all 3 changes ended up touching the *same file* (`explorers.html`), but they're **not really related** (2 are price changes, 1 is a title change).

**The trick used to split them:**

```bash
git diff explorers.html
# see ALL three changes mixed together
```

So the instructor:
1. Temporarily **undid** the title change in the file (saved it back to old text)
2. Now `git diff` only shows the 2 price changes
3. Staged just those: `git add explorers.html` (+ other price files)
4. **Redid** the title change in the editor (typed "Make New Friends" again)
5. `git status` → title change sits in working directory, price changes sit safely in staging
6. Committed the staged price changes only:
```bash
git commit -m "Edits prices on two packages

* Big Sur Retreat from 620 to 750 and California Calm from 250 to 270"
```
7. Then committed the rest:
```bash
git commit -a -m "Changes title of Explorers page"
```

**The clever bit:** staging is like a tray you fill up separately from your working table. You can load the tray (stage), keep working on the table (edit more), and the tray doesn't change until you touch it again.

---

## Quick command cheat-sheet

| Command | What it does |
|---|---|
| `git init` | Start tracking a folder |
| `git status` | What's changed right now |
| `git diff` | Show the actual changes |
| `git add <file>` | Put a file in staging (ready to save) |
| `git commit -m "msg"` | Save a snapshot |
| `git commit -a -m "msg"` | Skip staging, save everything tracked |
| `git log` / `git log --oneline` | See commit history |
| `git show <SHA>` | See what one commit changed |
| `git mv old new` | Rename + track in one go |

# Undoing Changes in Git

**10. Undo changes in the working directory**

Imagine you deleted something from a file by accident and already closed it — no "undo" button left. Git remembers though, because it has the last saved snapshot.

```bash
git status
# tells you: "use git checkout -- <file> to discard changes"

git checkout -- index.html
```

Breaking down `git checkout -- index.html`:
- `git checkout` = "go get me a version of something"
- `--` = a wall that says "I mean a **file**, not a branch" (checkout is used for both, so this avoids confusion)
- `index.html` = the file to restore

This is like returning a rented book and getting a brand new copy — whatever you scribbled in your working copy gets thrown away, replaced with what's in the repository.

⚠️ It's destructive — your edit is gone, no way back (unless it was committed).

---

**11. Unstage files**

You staged something (`git add`) but changed your mind — you don't want it in the next commit yet.

```bash
git add tours/*        # stages a bunch of files
git status              # tells you: "use git reset HEAD <file> to unstage"

git reset HEAD tours.html
```

Think of staging like a shopping basket at checkout. `git reset HEAD <file>` = "actually, put that back on the shelf." The item still exists (it's still changed in your working directory) — it's just not in the basket anymore.

To undo everything (unstage AND discard the actual edits):
```bash
git checkout -- .   # the "." means "all files"
```

---

**12. Amend a commit**

Say you just made a commit, but forgot something small. Instead of a whole new commit, you can **edit the last one** — but only the *last* one.

**Why only the last one?** Each commit's ID (SHA) is like a fingerprint built from its content + its parent's fingerprint. Change an old commit → its fingerprint changes → every commit after it points to a fingerprint that no longer exists → the whole chain breaks. Only the very last commit is safe to touch, since nothing depends on it yet.

```bash
# made a commit already...
git commit -am "changed items to bring"

# oops, forgot something. Edit the file, then:
git add resources.html
git commit --amend -m "reorder recommended items for trip"
```

What `--amend` really does: takes your old commit, pulls it back down, mixes in whatever's newly staged, and creates a **brand new commit with a new SHA** in its place. The old one disappears from `git log`.

You can even amend just to fix a typo in the message:
```bash
git commit --amend -m "reorder recommended items for outdoor trip"
```

---

**13. Retrieve an old version of a file**

You want to see (or bring back) how a file looked *before* a certain commit — without breaking Git's rule of "never edit old history."

```bash
git log                          # find the commit BEFORE the change you want to undo
git checkout <that-SHA> -- explorers.html
```

This pulls that old version into both your **working directory** and **staging** (unlike the earlier `checkout --` which only touches the working directory).

```bash
git diff --staged   # see exactly what's about to be "undone"
```

Then you either:
- Commit it as-is (a clean "revert" done by hand), or
- Tweak it further, then commit

**Golden rule:** Don't try to rewrite old history. If you want to undo something, make a **new commit** that reflects the undo — like admitting "yeah I changed my mind" rather than pretending it never happened.

---

**14. Revert a commit (the easy way)**

Doing the above by hand works, but there's a shortcut for "just undo this whole commit":

```bash
git log                  # find the SHA of the commit to undo
git revert <SHA>
```

This opens your editor with a message like "Revert changes title of Explorers page" — pre-filled, referencing the original commit. Save and close.

Git automatically creates a **new commit that's the exact opposite** of the one you're reverting.

```bash
git show <old-SHA>    # see the original change
git show HEAD          # see the revert — it's the mirror image
```

**Why atomic commits matter here:** if that commit only did ONE thing, reverting it is clean and safe. If it had 50 unrelated changes bundled in, reverting it would undo all 50 — even ones you wanted to keep.

---

**15. Remove untracked files (`git clean`)**

For junk files Git isn't tracking at all (like stray temp files) that you want gone completely.

```bash
git status         # shows them as "untracked"

git clean -n        # DRY RUN — shows what WOULD be deleted, doesn't touch anything
git clean -f         # FORCE — actually deletes them
```

- `-n` = "just tell me" (safe, no changes made)
- `-f` = "do it for real" (permanent — no trash bin, no undo)

⚠️ Important nuance: if a file is already **staged** (even just added, not committed), `git clean` will **not** touch it — it only removes files Git has zero record of. Staged files need `git reset HEAD <file>` first if you want `clean` to catch them too.

---

## Cheat-sheet — Undo commands

| Situation | Command |
|---|---|
| Discard uncommitted edits to a file | `git checkout -- <file>` |
| Unstage a file (keep the edit) | `git reset HEAD <file>` |
| Fix the very last commit | `git commit --amend` |
| Pull an old file version into staging | `git checkout <SHA> -- <file>` |
| Undo a whole commit safely (new commit) | `git revert <SHA>` |
| Delete untracked junk files | `git clean -n` then `git clean -f` |



