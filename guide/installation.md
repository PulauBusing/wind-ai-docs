# 安装配置

## 安装docsify-cli

推荐全局安装`docsify-cli`工具，可以方便地在本地预览文档。

### 使用npm安装

```bash
npm i docsify-cli -g
```

### 使用yarn安装

```bash
yarn global add docsify-cli
```

## 初始化项目

如果你想从头开始创建项目，可以使用`docsify init`命令：

```bash
# 在当前目录初始化
docsify init .

# 在指定目录初始化
docsify init ./docs
```

初始化后会创建以下文件：
- `index.html` - 入口文件
- `README.md` - 首页内容
- `.nojekyll` - 用于GitHub Pages

## 本地预览

使用`docsify serve`命令启动本地服务器：

```bash
docsify serve .
```

默认访问地址：`http://localhost:3000`

### 自定义端口

```bash
docsify serve . -p 8080
```

### 指定目录

```bash
docsify serve ./docs
```

## 目录结构

推荐的项目结构：

```
docs/
├── index.html          # 入口文件
├── README.md           # 首页
├── _sidebar.md         # 侧边栏配置
├── _navbar.md          # 导航栏配置
├── _coverpage.md       # 封面页
├── .nojekyll          # GitHub Pages配置
├── guide/             # 指南目录
│   ├── README.md
│   └── ...
├── tutorial/          # 教程目录
│   ├── README.md
│   └── ...
└── assets/            # 资源目录
    ├── images/
    └── css/
```

## 配置选项

在`index.html`中可以配置Docsify的各种选项：

```javascript
window.$docsify = {
  name: '知识库名称',
  repo: 'https://github.com/your-repo',
  loadSidebar: true,
  loadNavbar: true,
  maxLevel: 4,
  subMaxLevel: 3,
  auto2top: true,
  homepage: 'README.md',
  search: {
    placeholder: '搜索',
    noData: '没有结果',
    depth: 6
  }
}
```

## 部署

### GitHub Pages

1. 将项目推送到GitHub仓库
2. 在仓库设置中启用GitHub Pages
3. 选择部署分支（通常是main或gh-pages）
4. 访问`https://username.github.io/repo-name`

### 其他平台

Docsify生成的是纯静态网站，可以部署到任何静态托管平台：

- Vercel
- Netlify
- GitLab Pages
- Cloudflare Pages
- 阿里云OSS
- 腾讯云COS

只需上传所有文件即可。

## 下一步

- [基本使用](guide/basic-usage.md)
- [配置说明](reference/configuration.md)

