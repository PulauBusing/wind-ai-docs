# 快速开始指南

## 🚀 5分钟快速上手

### 方法一：直接打开（最简单）

1. **双击打开** `index.html` 文件
2. 在浏览器中即可查看知识库

> ⚠️ 注意：某些功能可能需要本地服务器才能正常工作

### 方法二：使用本地服务器（推荐）

#### 使用docsify-cli

```bash
# 1. 全局安装docsify-cli
npm install -g docsify-cli

# 2. 启动服务器
docsify serve .

# 3. 打开浏览器访问
# http://localhost:3000
```

#### 使用npm脚本

```bash
# 1. 安装依赖
npm install

# 2. 启动开发服务器
npm run dev

# 3. 打开浏览器访问
# http://localhost:3000
```

#### 使用Python（无需安装Node.js）

```bash
# Python 3
python -m http.server 3000

# Python 2  
python -m SimpleHTTPServer 3000
```

## 📝 开始编写文档

### 1. 编辑首页

打开 `README.md` 文件，编写首页内容：

```markdown
# 我的知识库

欢迎来到我的知识库！

## 介绍

这里是介绍内容...
```

### 2. 创建新文档

在相应目录下创建 `.md` 文件：

```bash
# 例如在guide目录下创建新文档
guide/my-new-doc.md
```

### 3. 更新侧边栏

编辑 `_sidebar.md`，添加链接：

```markdown
* 快速开始
  * [简介](guide/README.md)
  * [我的新文档](guide/my-new-doc.md)
```

### 4. 刷新查看

刷新浏览器，查看新添加的内容。

## 🎨 自定义配置

### 修改站点名称

编辑 `index.html`，找到配置部分：

```javascript
window.$docsify = {
  name: '我的知识库',  // 修改这里
  repo: 'https://github.com/your-username/your-repo'  // 添加你的仓库地址
}
```

### 修改主题颜色

在 `index.html` 的 `<style>` 标签中：

```css
:root {
  --theme-color: #42b983;  /* 修改为你喜欢的颜色 */
}
```

### 更换主题

替换主题CSS链接：

```html
<!-- Vue主题（默认） -->
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/vue.css">

<!-- 或选择其他主题 -->
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/dark.css">
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/buble.css">
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/pure.css">
```

## 📂 目录结构说明

```
.
├── index.html              # ⭐ 主入口文件（配置在这里）
├── README.md               # ⭐ 首页内容（这里是你的主页）
├── _sidebar.md             # ⭐ 侧边栏导航（配置目录结构）
├── _navbar.md              # 顶部导航栏
├── .nojekyll              # GitHub Pages配置文件
├── package.json           # 项目依赖配置
├── guide/                 # 📁 指南文档目录
├── tutorial/              # 📁 教程文档目录
├── reference/             # 📁 参考文档目录
├── assets/                # 📁 静态资源目录
│   ├── images/           #    图片
│   ├── css/              #    自定义样式
│   └── js/               #    自定义脚本
├── changelog.md           # 更新日志
├── contributing.md        # 贡献指南
└── about.md              # 关于页面
```

## 🎯 常用操作

### 添加图片

1. 将图片放入 `assets/images/` 目录
2. 在Markdown中引用：

```markdown
![图片描述](assets/images/your-image.png)
```

### 添加链接

```markdown
<!-- 内部链接 -->
[链接到其他页面](guide/installation.md)

<!-- 外部链接 -->
[访问GitHub](https://github.com)
```

### 代码高亮

````markdown
```javascript
function hello() {
  console.log('Hello World');
}
```
````

### 添加提示框

```markdown
?> 这是一个提示框

!> 这是一个警告框
```

## 🌐 部署上线

### 部署到GitHub Pages

1. 创建GitHub仓库
2. 推送代码：

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/your-username/your-repo.git
git push -u origin main
```

3. 在仓库设置中启用GitHub Pages
4. 访问 `https://your-username.github.io/your-repo/`

### 部署到Vercel

```bash
# 安装Vercel CLI
npm i -g vercel

# 登录
vercel login

# 部署
vercel
```

### 部署到Netlify

1. 访问 [Netlify](https://www.netlify.com/)
2. 拖拽整个文件夹到网站
3. 等待部署完成

## 📚 下一步

- 📖 阅读[完整文档](guide/README.md)了解更多功能
- 🎓 查看[教程](tutorial/README.md)学习进阶用法
- ❓ 遇到问题？查看[常见问题](reference/faq.md)
- 🤝 想要贡献？阅读[贡献指南](contributing.md)

## 💡 提示

- **Markdown预览**：使用VS Code的Markdown预览功能边写边看效果
- **实时预览**：修改文件后刷新浏览器即可看到变化
- **搜索功能**：按 `/` 键快速打开搜索框
- **移动端**：知识库自动适配移动设备

## 🆘 需要帮助？

- 查看 [Docsify官方文档](https://docsify.js.org)
- 查看本项目的 [常见问题](reference/faq.md)
- 在 [GitHub Issues](https://github.com/docsifyjs/docsify/issues) 搜索或提问

---

**开始你的知识库之旅吧！** 🚀

