# Standard Operating Procedure: Renaming `master` to `main`

This guide outlines the proper workflow for changing a Git repository's default branch from `master` to `main` when working with Android Studio, VS Code, or any terminal environment.

---

## Prerequisites
* Save and commit any uncommitted local changes before starting.
* Ensure you are connected to the internet and authenticated with GitHub.

---

## Step 1: Execute Local Branch Changes (Terminal / IDE)

Open your terminal or embedded IDE terminal (Android Studio / IntelliJ / VS Code) inside your project root and run the following commands sequentially:

```bash
# 1. Rename your local 'master' branch to 'main'
git branch -m master main

# 2. Push the new 'main' branch to GitHub and set up tracking
git push -u origin main
```

> **Note:** At this point, GitHub now has both `master` and `main` branches. `master` remains the designated *default* branch on GitHub until changed manually via the web interface.

---

## Step 2: Switch the Default Branch on GitHub (Web Interface)

Because GitHub protects the default branch from being deleted, you must change the default branch designation before deleting `master`.

1. Go to your repository home page on **GitHub.com**.
2. Click **Settings** (located in the top menu bar).
3. Select **Branches** from the left-hand navigation sidebar.
4. Next to the **Default branch** header, click the **Switch default branch** button (represented by two arrows `⇆`).
5. Choose **`main`** from the dropdown menu and click **Update**.
6. Confirm the prompt when GitHub asks to confirm the change.

---

## Step 3: Remove Old Remote Branch & Verify Sync (Terminal)

Now that `main` is the primary default branch on GitHub, return to your terminal to delete the remote `master` branch and verify the local setup:

```bash
# 1. Delete the remote 'master' branch from GitHub
git push origin --delete master

# 2. Update local remote reference HEAD pointing to origin/main
git remote set-head origin -a

# 3. Fetch latest references and verify local state
git fetch --prune
git status
```

---

## Step 4: Sync Secondary Machines / Other Clones (If applicable)

If you have already cloned this repository on another machine (e.g., Ubuntu workspace, laptop), perform these commands on that secondary machine to align local references:

```bash
# 1. Fetch all updated branches and remote references
git fetch origin

# 2. Switch local 'master' to track updated 'main'
git checkout master
git branch -m master main
git branch -u origin/main main

# 3. Update the HEAD pointer reference
git remote set-head origin -a
```

---

## Quick Reference Summary Sheet

| Action | Command |
| :--- | :--- |
| **Rename branch locally** | `git branch -m master main` |
| **Push & track `main`** | `git push -u origin main` |
| **Delete remote `master`** | `git push origin --delete master` |
| **Prune stale references** | `git fetch --prune` |
| **Update remote HEAD reference** | `git remote set-head origin -a` |
