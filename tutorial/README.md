# 入门教程

欢迎来到Docsify知识库入门教程！本教程将带你快速掌握Docsify的使用方法。

## 学习路径

### 第一步：了解基础

在开始之前，你需要了解：

1. **Markdown语法** - Docsify使用Markdown编写文档
2. **HTML基础** - 了解基本的HTML知识有助于自定义配置
3. **JavaScript基础** - 用于配置Docsify选项（可选）

### 第二步：搭建环境

按照以下步骤搭建你的Docsify环境：

1. 安装Node.js和npm
2. 安装docsify-cli工具
3. 初始化项目
4. 启动本地服务器

详细步骤请参考：[安装配置](../guide/installation.md)

### 第三步：创建内容

开始创建你的第一份文档：

1. 编辑`README.md`作为首页
2. 创建新的Markdown文件
3. 在侧边栏中添加链接
4. 预览效果

详细使用方法：[基本使用](../guide/basic-usage.md)

## 实战案例

### 案例1：创建个人博客

使用Docsify创建个人技术博客：

**步骤：**
1. 创建文章分类目录（前端、后端、数据库等）
2. 为每篇文章创建Markdown文件
3. 配置侧边栏显示文章列表
4. 添加搜索和分页功能
5. 部署到GitHub Pages

### 案例2：项目文档

为开源项目编写文档：

**步骤：**
1. 创建入门指南
2. 编写API参考文档
3. 添加使用示例
4. 配置多语言支持
5. 集成到项目仓库

### 案例3：团队知识库

搭建团队内部知识库：

**步骤：**
1. 规划知识体系结构
2. 创建各个领域的文档
3. 添加权限控制（如需要）
4. 部署到内网服务器
5. 定期维护更新

## 常用技巧

### 1. 快速导航

使用侧边栏和搜索功能快速找到内容：

```javascript
search: {
  maxAge: 86400000,
  paths: 'auto',
  placeholder: '搜索',
  depth: 6
}
```

### 2. 代码高亮

引入对应语言的Prism插件：

```html
<script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-python.min.js"></script>
```

### 3. 图片优化

使用图片缩放插件：

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/zoom-image.min.js"></script>
```

### 4. 离线缓存

配置Service Worker实现离线访问：

```javascript
serviceWorker: {
  enabled: true,
  path: '/sw.js'
}
```

## 学习资源

### 官方资源

- [Docsify官方文档](https://docsify.js.org)
- [GitHub仓库](https://github.com/docsifyjs/docsify)
- [插件列表](https://docsify.js.org/#/awesome)

### 社区资源

- [中文社区](https://github.com/docsifyjs/docsify/discussions)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/docsify)
- [示例网站集合](https://github.com/docsifyjs/awesome-docsify)

### 相关工具

- [Typora](https://typora.io/) - Markdown编辑器
- [VS Code](https://code.visualstudio.com/) - 代码编辑器
- [GitHub Desktop](https://desktop.github.com/) - Git客户端

## 练习项目

### 初级练习

1. 创建一个包含5个页面的简单文档网站
2. 配置侧边栏和导航栏
3. 添加搜索功能
4. 部署到GitHub Pages

### 中级练习

1. 创建一个多级目录结构的知识库
2. 添加封面页和自定义主题
3. 集成多个插件（代码复制、分页等）
4. 实现多语言支持

### 高级练习

1. 开发自定义Docsify插件
2. 实现自动化文档生成
3. 集成CI/CD部署流程
4. 优化SEO和性能

## 下一步

继续学习更多高级功能：

- [进阶教程](tutorial/advanced.md)
- [最佳实践](tutorial/best-practices.md)
- [API参考](../reference/README.md)

---

💡 **提示**：遇到问题时，先查看[常见问题](../reference/faq.md)，或在社区提问。

