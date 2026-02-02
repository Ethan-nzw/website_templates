# Deploy This Project to GitHub (SofeagcGrasp)

Use these steps to upload this website to your repository:  
**https://github.com/Ethan-nzw/SofeagcGrasp.git**

---

## Option A: Push to SofeagcGrasp (keep both repos)

If you want to keep your current `origin` (website_templates) and also push this project to SofeagcGrasp:

```bash
cd /home/niu/website_templates

# 1. Add SofeagcGrasp as a second remote named "sofeagc"
git remote add sofeagc https://github.com/Ethan-nzw/SofeagcGrasp.git

# 2. Stage all files (including new ones)
git add .

# 3. Commit
git commit -m "Add SofeagcGrasp paper website and improved index"

# 4. Push to SofeagcGrasp (first time: set upstream)
git push -u sofeagc master
```

If the SofeagcGrasp repo already has a README or other commits and Git refuses the push:

```bash
# Pull and merge unrelated histories, then push
git pull sofeagc master --allow-unrelated-histories
# Resolve any conflicts if asked, then:
git push -u sofeagc master
```

---

## Option B: Make SofeagcGrasp the main remote

If you want this folder to point only at SofeagcGrasp (replace `origin`):

```bash
cd /home/niu/website_templates

# 1. Change origin to SofeagcGrasp
git remote set-url origin https://github.com/Ethan-nzw/SofeagcGrasp.git

# 2. Stage and commit
git add .
git commit -m "Add SofeagcGrasp paper website"

# 3. Push (SofeagcGrasp may have existing commits – see note below)
git push -u origin master
```

If you get "rejected (non-fast-forward)" because SofeagcGrasp already has content:

```bash
git pull origin master --allow-unrelated-histories
# Fix any merge conflicts, then:
git push -u origin master
```

---

## Option C: Overwrite SofeagcGrasp completely

If SofeagcGrasp only has a README and you want this project to be the only content:

```bash
cd /home/niu/website_templates

git remote add sofeagc https://github.com/Ethan-nzw/SofeagcGrasp.git
git add .
git commit -m "Add SofeagcGrasp paper website"
git push -u sofeagc master --force
```

**Warning:** `--force` overwrites the history on SofeagcGrasp. Only use this if you don’t need anything that’s already in that repo.

---

## After pushing: enable GitHub Pages

1. Open **https://github.com/Ethan-nzw/SofeagcGrasp**
2. Go to **Settings → Pages**
3. Under **Source**, choose **Deploy from a branch**
4. Branch: **master** (or **main**), folder: **/ (root)**
5. Save. Your site will be at:  
   **https://ethan-nzw.github.io/SofeagcGrasp/**

Use **index_improved.html** as the main page by either:
- Renaming it to **index.html** and committing, or  
- Visiting **https://ethan-nzw.github.io/SofeagcGrasp/index_improved.html** directly.
