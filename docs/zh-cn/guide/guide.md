# 环境
- node 12
- npm  6.14.16

# 安装

```shell
npm install -g docsify-cli
```

# 初始化

```shell
mkdir light-docsify && cd light-docsify
docsify init ./docs
```

# 运行

```shell
docsify serve ./docs
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

# 部署站点
- [deploy](https://docsify.js.org/#/deploy)
  - [Github Pages](https://docsify.js.org/#/deploy?id=github-pages)
  - [Gitlab Pages](https://docsify.js.org/#/deploy?id=gitlab-pages)
  - [Firebase-Hosting](https://docsify.js.org/#/deploy?id=firebase-hosting)
  - [VPS](https://docsify.js.org/#/deploy?id=vps)
  - [Netlify](https://docsify.js.org/#/deploy?id=netlify)
  - [Vercel](https://docsify.js.org/#/deploy?id=vercel)
  - [AWS-Amplify](https://docsify.js.org/#/deploy?id=aws-amplify)
  - [Docker](https://docsify.js.org/#/deploy?id=docker)

点击进入项目的Settings页面`https://github.com/lorchr/light-docsify/settings/pages`

`Settings` -> `Pages` -> `Build and deployment`

- Source : Deploy from a branch
- Branch : Main docs
- Save and visit `https://lorchr.github.io/light-docsify`
