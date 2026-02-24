# Managing Two GitHub Accounts on One Machine
### A Complete Guide — shamimdewan & shamimdewan390

---

## Problem 1: Permission Denied Error

**Q:** Getting this error when pushing:
```
git push origin main
ERROR: Permission to shamimdewan390/oop.git denied to shamimdewan.
fatal: Could not read from remote repository.
```

**A:** Git is authenticating as `shamimdewan` instead of `shamimdewan390`. Fix it by:

1. **Clear stored credentials** (Windows: Credential Manager, Mac: Keychain)
2. **Update the remote URL** to use SSH:
   ```bash
   git remote set-url origin git@github.com:shamimdewan390/oop.git
   ```
3. **Use a Personal Access Token (PAT)** — GitHub no longer accepts passwords
4. **Check SSH key is linked to the right account:**
   ```bash
   ssh -T git@github.com
   # Should say: Hi shamimdewan390! You've successfully authenticated...
   ```

---

## Problem 2: Can I Control 2 GitHub Accounts at the Same Time?

**Q:** Is it possible to push to both `shamimdewan` and `shamimdewan390` from the same machine?

**A:** Yes! The best way is using **SSH Config**.

### Step 1 — Generate 2 SSH Keys
```bash
# For account 1
ssh-keygen -t ed25519 -C "shamimdewan@email.com" -f ~/.ssh/id_shamimdewan

# For account 2
ssh-keygen -t ed25519 -C "shamimdewan390@email.com" -f ~/.ssh/id_shamimdewan390
```

### Step 2 — Create SSH Config File
```bash
nano ~/.ssh/config
```
Paste:
```
# Account 1
Host github-shamimdewan
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_shamimdewan

# Account 2
Host github-shamimdewan390
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_shamimdewan390
```

### Step 3 — Add Public Keys to GitHub
Copy each public key and add to the respective GitHub account under **Settings → SSH and GPG keys → New SSH key**.

### Step 4 — Test Both Connections
```bash
ssh -T git@github-shamimdewan
ssh -T git@github-shamimdewan390
```

### Step 5 — Set Remote URL Per Project
```bash
# For shamimdewan repos
git remote set-url origin git@github-shamimdewan:shamimdewan/REPO-NAME.git

# For shamimdewan390 repos
git remote set-url origin git@github-shamimdewan390:shamimdewan390/REPO-NAME.git
```

### Step 6 — Set Git Identity Per Project
```bash
# Inside shamimdewan's project
git config user.name "shamimdewan"
git config user.email "shamimdewan@email.com"

# Inside shamimdewan390's project
git config user.name "shamimdewan390"
git config user.email "shamimdewan390@email.com"
```

---

## Problem 3: SSH Key Already Exists for shamimdewan — How to Generate a New One?

**Q:** SSH key for `shamimdewan` already exists. How to generate a new one for `shamimdewan390` without touching the old one?

**A:** Just generate a new key with a different filename:
```bash
ssh-keygen -t ed25519 -C "shamimdewan390@email.com" -f ~/.ssh/id_shamimdewan343
```
This creates:
- `~/.ssh/id_shamimdewan343` (private key)
- `~/.ssh/id_shamimdewan343.pub` (public key)

Your old key is completely safe and untouched. Verify both exist:
```bash
ls ~/.ssh/
```

---

## Problem 4: Writing the SSH Config File

**Q:** SSH key files found:
```
id_ed25519          → shamimdewan (existing)
id_shamimdewan343   → shamimdewan390 (new)
```
How to write the config file?

**A:**
```bash
nano ~/.ssh/config
```
```
# Account 1 - shamimdewan (existing key)
Host github-shamimdewan
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519

# Account 2 - shamimdewan390 (new key)
Host github-shamimdewan390
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_shamimdewan343
```
Save: **Ctrl + X → Y → Enter**

Then add the public key to shamimdewan390's GitHub:
```bash
cat ~/.ssh/id_shamimdewan343.pub
```

---

## Problem 5: Testing Authentication

**Q:** After config setup, both accounts authenticated successfully:
```
Hi shamimdewan! You've successfully authenticated...
Hi shamimdewan390! You've successfully authenticated...
```
But got error: `fatal: not a git repository`

**A:** You were inside `~/.ssh` folder, not your project folder. Navigate to your project first:
```bash
cd ~/Documents/Prectices/oop
git remote set-url origin git@github-shamimdewan390:shamimdewan390/oop.git
```

---

## Problem 6: Push Error — Branch Name Typo

**Q:** Getting this error:
```
git push origin mian
error: src refspec mian does not match any
```

**A:** Typo in branch name — `mian` instead of `main`:
```bash
git push origin main
```

---

## Problem 7: Do I Need to Run `git remote set-url` for Every Project?

**Q:** Will `git remote set-url origin git@github-shamimdewan390:shamimdewan390/oop.git` be needed for every project repo?

**A:** Yes, but only the **repo name** changes each time.

**Pattern:**
```bash
# For shamimdewan390's repos:
git remote set-url origin git@github-shamimdewan390:shamimdewan390/REPO-NAME.git

# For shamimdewan's repos:
git remote set-url origin git@github-shamimdewan:shamimdewan/REPO-NAME.git
```

**Examples:**
```bash
git remote set-url origin git@github-shamimdewan390:shamimdewan390/portfolio.git
git remote set-url origin git@github-shamimdewan390:shamimdewan390/todo-app.git
```

For every new project, run these **2 commands**:
```bash
# 1. Set correct remote URL
git remote set-url origin git@github-shamimdewan390:shamimdewan390/REPO-NAME.git

# 2. Set local git identity
git config user.name "shamimdewan390"
git config user.email "your390@email.com"
```

---

## Quick Reference Summary

| | shamimdewan | shamimdewan390 |
|---|---|---|
| SSH Key File | `id_ed25519` | `id_shamimdewan343` |
| SSH Host Alias | `github-shamimdewan` | `github-shamimdewan390` |
| Remote URL Pattern | `git@github-shamimdewan:shamimdewan/REPO.git` | `git@github-shamimdewan390:shamimdewan390/REPO.git` |
