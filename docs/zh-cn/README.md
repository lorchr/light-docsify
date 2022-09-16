# 安装

```shell
npm install -g docsify-cli
```

# 初始化

```shell
mkdir light-docsify
docsify init
```

# 运行

```shell
docsify serve ./
```

# 推送仓库

```shell
echo "# light-docsify" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:lorchr/light-docsify.git
git push -u origin main
```
