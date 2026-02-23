# shuaills.github.io

Single-page resume site for GitHub Pages.

## Local preview

```bash
cd /root/projects/shuaills.github.io
python3 -m http.server 8080
# open http://localhost:8080
```

## Publish

```bash
cd /root/projects/shuaills.github.io
git init
git branch -M master
git remote add origin git@github.com:shuaills/shuaills.github.io.git
git add .
git commit -m "feat: rebuild resume landing page"
git push -u origin master
```

GitHub Pages will update automatically after push.
