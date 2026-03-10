# Git & NGINX Assessment

**Author:** Abhinay Pandey  | **Date:** March 10, 2026

![Git](https://img.shields.io/badge/Git-2.43.0-F05032?style=flat&logo=git&logoColor=white)
![NGINX](https://img.shields.io/badge/NGINX-009639?style=flat&logo=nginx&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu_24-E95420?style=flat&logo=ubuntu&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white)

---

## 📋 Table of Contents

1. [Git Installation & Configuration](#1-git-installation--configuration)
2. [Repository Init & First Commit](#2-repository-init--first-commit)
3. [Feature Branch & Calculator Module](#3-feature-branch--calculator-module)
4. [GitHub Remote, Push & Pull Request](#4-github-remote-push--pull-request)
5. [Bugfix Branch, Stash, Revert & Reset](#5-bugfix-branch-stash-revert--reset)
6. [Merge Conflict Demo & Resolution](#6-merge-conflict-demo--resolution)
7. [NGINX Installation & Virtual Hosts](#7-nginx-installation--virtual-hosts)
8. [Docker + NGINX Container](#8-docker--nginx-container)
9. [Quick Reference](#9-quick-reference)

---

## 1. Git Installation & Configuration

### Install Git via apt

```bash
sudo apt update
sudo apt install git -y
git version   # git version 2.43.0
```

![Git Install](screenshots/Screenshot_from_20260310_124243.png)

### Set Global User Config

```bash
git config --global user.name "Abhinay-Pandey"
git config --global user.email "pandeyabhinay1269@gmail.com"
git config -l
```

![Git Config](screenshots/Screenshot_from_20260310_124618.png)

---

## 2. Repository Init & First Commit

### Create Directory & Initialize Git Repo

```bash
mkdir git-nginx-assessment
cd git-nginx-assessment
git init
```

![Git Init](screenshots/Screenshot_from_20260310_124721.png)

### Create Initial Files

```bash
echo "#Git & NGINX Assessment Name : Abhinay" > README.md
echo "print('Hello Git')" > app.py
ls
```

![Create Files](screenshots/Screenshot_from_20260310_124933.png)

### Stage, Status Check & First Commit

```bash
git add README.md app.py
git status
git commit -m "Inital commit : Add README and app.py"
```

![First Commit](screenshots/Screenshot_from_20260310_125114.png)

### Verify with git log

```bash
git log
```

![Git Log](screenshots/Screenshot_from_20260310_125134.png)

---

## 3. Feature Branch & Calculator Module

### Create & Switch to Feature Branch

```bash
git checkout -b feature/add-calculator
git branch
```

![Feature Branch](screenshots/Screenshot_from_20260310_125423.png)

### Write calculator.py

```python
def add(a, b):
    return a+b

def subtract(a, b):
    return a-b
```

![Vim Calculator](screenshots/Screenshot_from_20260310_125825.png)

### Commit Calculator Module

```bash
git add calculator.py
git commit -m "Feat: add calculator mudule with add and subtract functions"
```

![Commit Calculator](screenshots/Screenshot_from_20260310_130654.png)

### Git Log — Two Commits

```bash
git log --oneline
```

![Git Log Feature](screenshots/Screenshot_from_20260310_131754.png)

---

## 4. GitHub Remote, Push & Pull Request

### Add Remote & Push master

```bash
git remote -v
git push origin master
```

![Push Master](screenshots/Screenshot_from_20260310_131910.png)

### Push Feature Branch

```bash
git push origin feature/add-calculator
```

![Push Feature](screenshots/Screenshot_from_20260310_132046.png)

### Compare Changes on GitHub

![GitHub Compare](screenshots/Screenshot_from_20260310_132413.png)

### Open Pull Request

![GitHub PR](screenshots/Screenshot_from_20260310_132609.png)

### Pull Merged Changes Locally

```bash
git checkout master
git pull origin master
git log --oneline
```

![Git Pull](screenshots/Screenshot_from_20260310_132742.png)

---

## 5. Bugfix Branch, Stash, Revert & Reset

### Create Bugfix Branch & Edit app.py

```bash
git checkout -b bugfix/stash-demo
vim app.py   # add "# this is a temp change"
```

![Bugfix Branch](screenshots/Screenshot_from_20260310_132817.png)

![Vim Temp Change](screenshots/Screenshot_from_20260310_132904.png)

### Git Stash — Save WIP

```bash
git stash
git status   # working tree clean
cat app.py   # temp change is gone
```

![Git Stash](screenshots/Screenshot_from_20260310_132959.png)

### Add a Bug Commit

```bash
echo "this is a bug" > bug.txt
git add bug.txt
git commit -m "bug : add bug.txt"
git log --oneline
```

![Bug Commit](screenshots/Screenshot_from_20260310_133202.png)

### Revert the Bug Commit

```bash
git revert HEAD
```

![Git Revert](screenshots/Screenshot_from_20260310_133331.png)

### Wrong Commit + git commit --amend

```bash
echo "hotfix content" > hotfix.txt
git add hotfix.txt
git commit -m "wrong commit"

# Fix the commit message:
git commit --amend -m "Fix :hotfix wiht corrected messege"
```

![Wrong Commit Amend](screenshots/Screenshot_from_20260310_133550.png)

![Amended Log](screenshots/Screenshot_from_20260310_133746.png)

### Add Commits & git reset --soft

```bash
echo "file one" > one.txt && git add one.txt && git commit -m "add one.txt"
echo "file two" > two.txt && git add two.txt && git commit -m "add two.txt"

# Undo last commit, keep changes staged:
git reset --soft HEAD~1
git status
```

![Reset Soft](screenshots/Screenshot_from_20260310_134412.png)

### Git Stash Pop — Restore WIP

```bash
git stash pop
cat app.py
# print('Hello Git')
# # this is a temp change
```

![Stash Pop](screenshots/Screenshot_from_20260310_134837.png)

![Cat app.py After Pop](screenshots/Screenshot_from_20260310_134908.png)

### Final Status — Clean

```bash
git status   # nothing to commit, working tree clean
```

![Git Status Clean](screenshots/Screenshot_from_20260310_134951.png)

---

## 6. Merge Conflict Demo & Resolution

### Update README on master Branch

```bash
git checkout master
nano README.md   # edit heading
git add README.md
git commit -m "docs: update heading on main branch"
```

![Master README Update](screenshots/Screenshot_from_20260310_135950.png)

### Create conflict-demo Branch & Edit Same Line

```bash
git checkout -b conflict-demo
nano README.md   # edit same heading differently
git add README.md
git commit -m "docs: update heading on conflict-demo branch"
```

![Conflict Demo Branch](screenshots/Screenshot_from_20260310_140102.png)

### Trigger the Merge Conflict

```bash
git checkout master
git merge conflict-demo
# CONFLICT (content): Merge conflict in README.md
# Automatic merge failed; fix conflicts and then commit the result.
```

![Merge Conflict](screenshots/Screenshot_from_20260310_140520.png)

### View Conflict Markers

```
<<<<<<< HEAD
# Git and NGINX Assessment - Main Version
=======
# Git and NGINX Assessment - Conflict Version
>>>>>>> conflict-demo
```

![Conflict Markers](screenshots/Screenshot_from_20260310_141014.png)

### Resolve Conflict & Commit

```bash
nano README.md   # remove markers, keep correct version
git add README.md
git commit -m "fix: resolve merge conflict in README heading"
```

![Resolve Conflict](screenshots/Screenshot_from_20260310_142321.png)

### Final Git Log After Resolution

```bash
git log --oneline
```

![Final Log](screenshots/Screenshot_from_20260310_142551.png)

---

## 7. NGINX Installation & Virtual Hosts

### Install & Start NGINX

```bash
sudo systemctl status nginx   # active (running)
sudo systemctl enable nginx
```

![NGINX Status](screenshots/Screenshot_from_20260310_144658.png)

![NGINX Enable](screenshots/Screenshot_from_20260310_144818.png)

### Create Web Roots & HTML Files

```bash
sudo mkdir -p /var/www/app1.local/html
echo '<h1>welcome to app 1</h1>' | sudo tee /var/www/app1.local/html/index.html

sudo mkdir -p /var/www/app2.local/html
echo '<h1>welcome to app 2</h1>' | sudo tee /var/www/app2.local/html/index.html

sudo chown -R www-data:www-data /var/www/app1.local /var/www/app2.local
sudo chmod -R 755 /var/www/app1.local /var/www/app2.local
```

![Create Web Roots](screenshots/Screenshot_from_20260310_145059.png)

### app1.local — NGINX Config

```nginx
server {
    listen 80;
    server_name app1.local;

    root /var/www/app1.local/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

![App1 Config](screenshots/Screenshot_from_20260310_145306.png)

### app2.local — NGINX Config

```nginx
server {
    listen 80;
    server_name app2.local;

    root /var/www/app2.local/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

![App2 Config](screenshots/Screenshot_from_20260310_145823.png)

### Enable Sites, Test & Reload

```bash
sudo ln -s /etc/nginx/sites-available/app1.local /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/app2.local /etc/nginx/sites-enabled/
sudo nginx -t
# nginx: configuration file /etc/nginx/nginx.conf syntax is ok
# nginx: configuration file /etc/nginx/nginx.conf test is successful
sudo systemctl reload nginx
```

![NGINX Test](screenshots/Screenshot_from_20260310_145901.png)

![Reload NGINX](screenshots/Screenshot_from_20260310_150053.png)

### Verified via curl & Browser

```bash
curl -k https://16.171.37.11
# <h1>welcome to app 1</h1>
```

![Curl Verify](screenshots/Screenshot_from_20260310_150148.png)

> ✅ **app1.local** → `https://16.171.37.11` → *welcome to app 1*  
> ✅ **app2.local** → `https://16.171.37.11:8082` → *welcome to app 2*

---

## 8. Docker + NGINX Container

### Fix Docker Permissions & Run Container

```bash
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
docker ps

docker run -d -p 8080:80 --name backend-app nginx:alpine
curl http://localhost:8080   # Welcome to nginx!
```

![Docker Run](screenshots/Screenshot_from_20260310_134143.png)

> ✅ `http://16.171.37.11:8080` → NGINX default welcome page served from Docker container (`nginx:alpine`)

---

## 9. Quick Reference

| Command | Purpose |
|---|---|
| `git init` | Initialize a new local repository |
| `git add / commit` | Stage changes and create a snapshot |
| `git checkout -b <name>` | Create and switch to a new branch |
| `git stash` | Save uncommitted work temporarily |
| `git stash pop` | Restore stashed changes |
| `git revert HEAD` | Safely undo last commit (adds new commit) |
| `git commit --amend` | Fix the last commit message |
| `git reset --soft HEAD~1` | Undo commit, keep changes staged |
| `git merge <branch>` | Merge another branch into current |
| `git push / pull` | Sync local changes with GitHub remote |
| `git log --oneline` | Compact commit history view |
| `sudo nginx -t` | Test NGINX config syntax |
| `sudo systemctl reload nginx` | Apply NGINX config changes |
| `docker run -d -p 8080:80 nginx:alpine` | Run NGINX in a Docker container |

---

*Git & NGINX Assessment — Abhinay Pandey — March 10, 2026*
