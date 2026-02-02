# Fix: Videos Not Playing on GitHub Pages

**"No video with supported format and MIME type found"** means the URL is returning something that isn’t a valid video—usually an **LFS pointer** (small text file) or a **404 HTML page**. GitHub Pages does **not** resolve Git LFS; it serves the pointer file, so the browser gets text and reports that error.

**What we did:**  
1. Stopped using LFS for `.mp4` so videos are stored as regular files (all under 100 MB).  
2. Added a `<base href="https://ethan-nzw.github.io/SofeagcGrasp/">` tag so relative video paths resolve correctly on Pages.  
3. Fixed the first carousel video (was pointing to the excluded 150 MB file) to use `droping_obejct.mp4`.

---

## Steps to apply (run in your project folder)

```bash
cd /home/niu/website_templates

# 1. Remove LFS pointers from the index (keeps files on disk)
git rm --cached static/videos/*.mp4

# 2. Add videos as regular files (from your working directory)
git add .gitattributes
git add static/videos/
git add index.html

# 3. Commit and push
git commit -m "Store videos as regular files so GitHub Pages can serve them"
git push sofeagc master
```

**Note:** Your `static/videos/` folder must contain the **actual video files** on disk (not LFS pointers). If you cloned the repo and never ran `git lfs pull`, run `git lfs pull` first so the real files are in `static/videos/`, then run the commands above.

After the push, wait 1–2 minutes for GitHub Pages to rebuild. Videos on https://ethan-nzw.github.io/SofeagcGrasp/ should then play.

---

## Verify

Open this URL directly in your browser:  
**https://ethan-nzw.github.io/SofeagcGrasp/static/videos/website_start_0.mp4**

- If the **video plays or downloads** → the repo is serving real video; the site should work.  
- If you see **text** (e.g. `version https://git-lfs.github.com/...`) or a **404 page** → the repo still has LFS pointers or the files weren’t pushed; run the steps above again and ensure `static/videos/` on disk has the real `.mp4` files before `git add`.
