# 最佳实践

总结使用Docsify构建知识库的最佳实践和注意事项。

## 文档组织

### 目录结构规范

推荐的目录结构：

```
docs/
├── index.html              # 入口文件
├── README.md               # 首页
├── _sidebar.md             # 侧边栏
├── _navbar.md              # 导航栏
├── _coverpage.md           # 封面
├── .nojekyll              # GitHub Pages配置
├── assets/                # 静态资源
│   ├── images/           # 图片
│   ├── css/              # 自定义样式
│   └── js/               # 自定义脚本
├── guide/                # 指南文档
│   ├── README.md
│   ├── getting-started.md
│   └── installation.md
├── tutorial/             # 教程文档
│   ├── README.md
│   ├── basic.md
│   └── advanced.md
├── reference/            # 参考文档
│   ├── README.md
│   ├── api.md
│   └── config.md
└── changelog.md          # 更新日志
```

### 文件命名规范

1. **使用小写字母**：`getting-started.md`
2. **使用连字符**：`best-practices.md`（不使用下划线或空格）
3. **语义化命名**：文件名要清晰表达内容
4. **避免特殊字符**：不使用中文、空格、特殊符号

### 内容组织原则

1. **从简单到复杂**：按照学习曲线组织内容
2. **模块化**：每个文档专注于一个主题
3. **相互关联**：通过链接建立文档间的联系
4. **保持更新**：定期检查和更新过时内容

## 写作规范

### Markdown规范

#### 标题层级

```markdown
# 一级标题（页面标题，每页只有一个）
## 二级标题（主要章节）
### 三级标题（子章节）
#### 四级标题（详细内容）
```

#### 段落格式

- 段落之间空一行
- 列表项前后空一行
- 代码块前后空一行

```markdown
这是第一段内容。

这是第二段内容。

- 列表项1
- 列表项2

这是代码示例：

```javascript
console.log('Hello');
```. // (去掉这个点)

继续正文内容。
```

### 代码规范

#### 代码块标注语言

总是为代码块指定语言：

````markdown
```javascript
function hello() {
  console.log('Hello');
}
```

```python
def hello():
    print("Hello")
```

```bash
npm install docsify-cli -g
```
````

#### 代码注释

为复杂代码添加注释：

```javascript
// 初始化Docsify配置
window.$docsify = {
  name: '知识库',        // 文档站点名称
  repo: '',              // GitHub仓库地址
  loadSidebar: true,     // 加载侧边栏
  maxLevel: 4,           // 侧边栏最大层级
  subMaxLevel: 3         // 内容目录最大层级
}
```

### 图片使用规范

#### 图片存储

```
assets/
└── images/
    ├── guide/          # 按目录分类
    │   └── screenshot.png
    ├── tutorial/
    │   └── demo.gif
    └── common/         # 公共图片
        └── logo.png
```

#### 图片引用

```markdown
<!-- 相对路径 -->
![描述文本](../assets/images/guide/screenshot.png)

<!-- 绝对路径 -->
![描述文本](/assets/images/logo.png)

<!-- 外部链接 -->
![描述文本](https://example.com/image.png)
```

#### 图片优化

1. **压缩图片**：使用工具压缩图片大小
2. **合适尺寸**：不要上传过大的图片
3. **使用WebP**：现代浏览器支持WebP格式
4. **添加描述**：总是添加alt文本

### 链接规范

#### 内部链接

```markdown
<!-- 相对路径 -->
[安装指南](./installation.md)
[上级目录](../README.md)

<!-- 绝对路径 -->
[首页](/)
[指南](/guide/README.md)

<!-- 锚点链接 -->
[跳转到安装](#安装)
```

#### 外部链接

```markdown
<!-- 在新标签页打开 -->
[Docsify官网](https://docsify.js.org ':target=_blank')

<!-- 禁用链接 -->
[暂未开放](# ':disabled')
```

## 性能优化

### 1. 延迟加载

对于大型文档，使用延迟加载：

```javascript
window.$docsify = {
  // 延迟加载侧边栏
  loadSidebar: true,
  
  // 只在需要时加载
  executeScript: true
}
```

### 2. 资源优化

```html
<!-- 使用CDN -->
<script src="//cdn.jsdelivr.net/npm/docsify@4"></script>

<!-- 最小化CSS -->
<link rel="stylesheet" href="style.min.css">

<!-- 图片懒加载 -->
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/zoom-image.min.js"></script>
```

### 3. 缓存策略

```javascript
// Service Worker缓存
window.$docsify = {
  pwa: {
    enabled: true,
    path: '/sw.js'
  }
}
```

### 4. 减少插件

只加载必要的插件，避免过多插件影响性能。

## SEO优化

### Meta标签

```html
<meta name="description" content="详细的页面描述">
<meta name="keywords" content="关键词1,关键词2,关键词3">
<meta name="author" content="作者名称">
<meta name="robots" content="index,follow">

<!-- Open Graph -->
<meta property="og:title" content="页面标题">
<meta property="og:description" content="页面描述">
<meta property="og:image" content="封面图片">
<meta property="og:type" content="website">
```

### 语义化HTML

```html
<!-- 使用语义化标签 -->
<header>
<nav>
<main>
<article>
<aside>
<footer>
```

### 站点地图

创建`sitemap.xml`：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://example.com/</loc>
    <lastmod>2025-01-01</lastmod>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://example.com/guide/</loc>
    <lastmod>2025-01-01</lastmod>
    <priority>0.8</priority>
  </url>
</urlset>
```

## 版本管理

### 使用Git

```bash
# 初始化仓库
git init

# 创建.gitignore
echo "node_modules/" > .gitignore
echo ".DS_Store" >> .gitignore

# 提交代码
git add .
git commit -m "Initial commit"

# 推送到远程
git remote add origin <repository-url>
git push -u origin main
```

### 版本标签

```bash
# 创建版本标签
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

### 更新日志

维护`changelog.md`：

```markdown
# 更新日志

## [1.1.0] - 2025-01-15

### 新增
- 添加搜索功能
- 新增评论系统

### 改进
- 优化移动端显示
- 提升加载速度

### 修复
- 修复侧边栏滚动问题
- 修复图片显示bug

## [1.0.0] - 2025-01-01

### 新增
- 初始版本发布
```

## 团队协作

### 贡献指南

创建`contributing.md`：

```markdown
# 贡献指南

## 如何贡献

1. Fork本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启Pull Request

## 写作规范

- 遵循Markdown语法规范
- 保持文档清晰简洁
- 添加适当的示例
- 检查拼写和语法

## 代码审查

所有PR需要至少一人审查通过后才能合并。
```

### 文档模板

创建文档模板（`.github/ISSUE_TEMPLATE/`）：

```markdown
---
name: 文档改进建议
about: 提出文档改进建议
---

## 问题描述
<!-- 描述当前文档存在的问题 -->

## 改进建议
<!-- 提出你的改进建议 -->

## 相关页面
<!-- 相关文档页面链接 -->
```

## 安全性

### 内容安全

1. **不要暴露敏感信息**：API密钥、密码等
2. **验证外部链接**：确保链接安全可信
3. **使用HTTPS**：部署时使用HTTPS协议

### XSS防护

Docsify默认会转义HTML，但如果使用`executeScript`，需要注意：

```javascript
window.$docsify = {
  // 谨慎使用
  executeScript: false
}
```

## 维护清单

### 定期检查

- [ ] 检查所有链接是否有效
- [ ] 更新过时的内容
- [ ] 检查图片是否正常显示
- [ ] 测试搜索功能
- [ ] 检查移动端显示
- [ ] 更新依赖版本
- [ ] 备份文档内容

### 监控指标

- 页面加载速度
- 搜索使用频率
- 用户访问路径
- 404错误页面

## 下一步

- [API参考](../reference/README.md)
- [配置说明](../reference/configuration.md)
- [常见问题](../reference/faq.md)

