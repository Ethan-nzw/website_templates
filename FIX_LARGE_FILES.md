# Fix GitHub Push: Large Video Files

GitHub **rejects** files over **100 MB**. Your push failed because:

- **Blocking:** `static/videos/in_use_video_plastic_cup.mp4` is **150.78 MB** (over 100 MB limit).
- Even with Git LFS, the file was **already in your git history** (in an earlier commit), so GitHub still sees the large blob and rejects the push.

**What we did:** The 150 MB file is now **excluded** from the repo (added to `.gitignore`). The first carousel video in `index_improved.html` temporarily uses `droping_obejct.mp4` so the page still works. When you host the plastic-cup video elsewhere (Google Drive, your server, etc.), replace that `<source src="...">` with your hosted URL.

To make the push succeed, **rewrite history** so no commit contains the 150 MB file. Use a **fresh history** (one new commit without the big file):

---

## Step 1: Remove the big file from the index (if still tracked)

From your project root:

```bash
cd /home/niu/website_templates

# Stop tracking the 150 MB file (keeps the file on disk, removes from git)
git rm --cached static/videos/in_use_video_plastic_cup.mp4 2>/dev/null || true
```

---

## Step 2: Create a new history without the large file

These commands create a **single new commit** that has no parent history, so the 150 MB file never appears in any commit.

```bash
cd /home/niu/website_templates

# 1. Create a new branch with no history (orphan)
git checkout --orphan new-main

# 2. Unstage everything
git rm -rf --cached .

# 3. Add .gitignore first (so the 150 MB file is ignored)
git add .gitignore

# 4. Add everything else (in_use_video_plastic_cup.mp4 is ignored)
git add .

# 5. Commit
git commit -m "Add SofeagcGrasp paper website"

# 6. Replace master with this new history
git branch -D master
git branch -m master

# 7. Force push to your remotes (required because history changed)
git push -f sofeagc master
git push -f origin master
```

Use only the remote you care about if you prefer (e.g. only `git push -f sofeagc master` for SofeagcGrasp).

---

## Step 3: Optional – host the 150 MB video and fix the first carousel

1. Upload `static/videos/in_use_video_plastic_cup.mp4` to Google Drive, your server, or another host and get a direct video URL.
2. In `index_improved.html` (and `index_1.html` if you use it), find the first carousel video (id `exp1-video1`) and replace:
   ```html
   <source src="static/videos/droping_obejct.mp4" type="video/mp4">
   ```
   with:
   ```html
   <source src="YOUR_HOSTED_VIDEO_URL" type="video/mp4">
   ```
3. Commit and push.

---

## Why LFS didn’t fix it

Git LFS only affects **new** commits. The 150 MB file was already committed as a normal blob in a previous commit. When you push, GitHub checks **all** objects in the pushed history, so it still saw the 150 MB file and rejected the push. Creating a new orphan branch and committing again means that file never appears in any commit, so the push succeeds.
