# Fix: Videos Not Playing on GitHub Pages

## Root cause

**"No video with supported format and MIME type found"** happens because:

1. **GitHub Pages serves `.mp4` with the wrong MIME type** (e.g. `application/octet-stream` or `application/mp4` instead of `video/mp4`). Browsers then refuse to play the file.
2. **GitHub Pages does not resolve Git LFS** – if the repo has LFS pointers instead of real video files, the browser gets a small text file and shows the same error.
3. **MIME types cannot be configured** on GitHub Pages, so serving videos from Pages directly often fails.

## Solution applied

**All video sources in `index.html` now use the jsDelivr CDN**, which serves files from your GitHub repo with the **correct MIME type** (`video/mp4`):

- Example: `https://cdn.jsdelivr.net/gh/Ethan-nzw/SofeagcGrasp@master/static/videos/website_start_0.mp4`
- jsDelivr fetches from GitHub and sets the right `Content-Type`, so the `<video>` element can play the file.

**Requirements:**

- The **actual video files** (not LFS pointers) must be in the repo. If you previously used LFS, run:

  ```bash
  git rm --cached static/videos/*.mp4
  git add static/videos/
  git commit -m "Store videos as regular files"
  git push sofeagc master
  ```

- If your **default branch is `main`** (not `master`), replace `@master` with `@main` in every video URL in `index.html` (search for `@master` and change to `@main`).

After pushing the updated `index.html`, videos on https://ethan-nzw.github.io/SofeagcGrasp/ should play.

---

## Verify

Open one video URL directly (e.g. jsDelivr):

**https://cdn.jsdelivr.net/gh/Ethan-nzw/SofeagcGrasp@master/static/videos/website_start_0.mp4**

- If the **video plays** → the repo has real video files and the site should work.
- If you see **text** (LFS pointer) or **404** → push the real `.mp4` files as regular files (no LFS) and try again.
