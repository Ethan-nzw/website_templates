# Fix GitHub Push: Authentication (401)

`Authentication failed` / `401` / `No anonymous write access` means GitHub is rejecting your credentials. **GitHub no longer accepts your account password** for Git over HTTPS. Use one of the options below.

---

## Option A: Personal Access Token (HTTPS)

Use a **Personal Access Token** instead of your password.

### 1. Create a token on GitHub

1. Open **https://github.com/settings/tokens**
2. Click **Generate new token** → **Generate new token (classic)**
3. Name it (e.g. `SofeagcGrasp push`), choose an expiry, and check **repo**.
4. Click **Generate token** and **copy the token** (you won’t see it again).

### 2. Push using the token

From the terminal:

```bash
cd /home/niu/website_templates

# Push to SofeagcGrasp (replace YOUR_TOKEN with your token)
git push https://YOUR_TOKEN@github.com/Ethan-nzw/SofeagcGrasp.git master

# Or set the remote URL once so future pushes use the token:
git remote set-url sofeagc https://YOUR_TOKEN@github.com/Ethan-nzw/SofeagcGrasp.git
git push -u sofeagc master
```

When Git asks for a password, **paste the token** (not your GitHub password).

**Security:** Don’t commit the token. To avoid storing it in the URL, use the credential helper so Git asks once:

```bash
git config --global credential.helper store
# Next push: use your GitHub username and the token as password; they’ll be saved.
```

---

## Option B: SSH (recommended long-term)

Use SSH so you don’t put a token in URLs.

### 1. Check for an SSH key

```bash
ls -la ~/.ssh/id_*.pub
```

If you see `id_ed25519.pub` or `id_rsa.pub`, you already have a key. Skip to step 3.

### 2. Create an SSH key (if needed)

```bash
ssh-keygen -t ed25519 -C "your_email@example.com" -f ~/.ssh/id_ed25519 -N ""
```

### 3. Add the public key to GitHub

- Copy the key: `cat ~/.ssh/id_ed25519.pub` (or `id_rsa.pub`)
- Go to **https://github.com/settings/keys**
- **New SSH key** → paste the key → save

### 4. Use SSH for the remote and push

```bash
cd /home/niu/website_templates

# Switch sofeagc to SSH
git remote set-url sofeagc git@github.com:Ethan-nzw/SofeagcGrasp.git

# Push (may ask to confirm GitHub’s host key the first time)
git push -u sofeagc master
```

Do the same for `origin` if you use it:

```bash
git remote set-url origin git@github.com:Ethan-nzw/website_templates.git
git push -u origin master
```

---

## Quick check

- **HTTPS:** `git remote -v` shows `https://github.com/...`
- **SSH:** `git remote set-url ... git@github.com:...` then `git push` (no password prompt if SSH key is added to GitHub).

If you still get 401, the token is wrong/expired or the SSH key isn’t added to your GitHub account.
