# Create / verify `.gitignore` in your vault root (keeps Archive & junk out)
- everything is currently `commented` out due to wanting everything on my notes currently
```bash
# Ignore ONLY what we don't want
# Archive - Discontinued - September 18 2025/
# *.vmdk
# *.iso
# *.zip
# *.7z
# *.tar
# *.gz
# *.mp4
# *.mov

# Obsidian noise
# .obsidian/workspace
# .obsidian/cache
# .obsidian/plugins/obsidian-git/data.json

# OS junk
# Thumbs.db
# .DS_Store
```
# Initialize Repo and push first time
```bash
# from your vault folder, e.g. D:\Asylum
git init                                 # make it a repo
git add .                                 # stage files (respects .gitignore)
git commit -m "Initial commit: notes only"
git branch -M main
git remote add origin git@github.com:<you>/<repo>.git   # use your SSH URL
git push -u origin main                   # first push + set upstream
```
If GitHub rejects because you accidentally tracked a big file, fix `.gitignore`, then:
```bash
git rm -r --cached .                      # clear index so .gitignore applies
git add .
git commit -m "Apply .gitignore (remove big files from index)"
git push
```
# ONE-TIME SETUP (Second device / laptop)
```bash
# Pick a folder where you want the vault
cd D:\

# Clone your repo
git clone git@github.com:<you>/<repo>.git Asylum   # or any folder name
cd Asylum

# Optional: verify remote
git remote -v
```
That’s it—this device now has the same notes.
# Daily Use
- A) Work computer → **Push changes**
```bash
cd D:\Asylum

git status                                      # (optional) see changes
git add .                                       # stage all changes
git commit -m "Update notes: <short message>"   # snapshot
git push                                        # upload only the diffs
```
- B) Other device → **Pull updates**
```bash
cd D:\Asylum

git status                                      # make sure no uncommitted edits
git pull                                        # download & merge new commits
```
# WORKING ON BOTH DEVICES? (Avoid clobbering)
- **Before you start editing** on any device: `git pull`
- **When you finish** on that device: `git add . && git commit -m "msg" && git push`
- ***This keeps both machines in sync and prevents conflicts.***
# TLDR
- **Work (push):** `git add . && git commit -m "msg" && git push`
- **Other device (pull):** `git pull`
- Every commit is a checkpoint; pushes/pulls only sync **changes**, not overwrite untouched files.
- Only redo the `git rm -r --cached .` step if you change `.gitignore` and need Git to forget newly ignored stuff.