# 常见问题

收集使用Docsify过程中的常见问题和解决方案。

## 安装和部署

### Q: 如何在本地运行Docsify？

**A:** 有三种方式：

1. **使用docsify-cli（推荐）**

```bash
npm i docsify-cli -g
docsify serve .
```

2. **使用Python HTTP服务器**

```bash
# Python 3
python -m http.server 3000

# Python 2
python -m SimpleHTTPServer 3000
```

3. **直接打开HTML文件**

双击`index.html`文件（某些功能可能受限）

### Q: 如何部署到GitHub Pages？

**A:** 步骤如下：

1. 将项目推送到GitHub仓库
2. 进入仓库Settings → Pages
3. 选择部署分支（main或gh-pages）
4. 选择根目录或docs目录
5. 保存后等待部署完成

访问地址：`https://username.github.io/repo-name`

### Q: GitHub Pages显示404怎么办？

**A:** 确保：

1. 存在`.nojekyll`文件
2. 选择了正确的分支和目录
3. `index.html`在根目录或docs目录
4. 仓库设置中启用了GitHub Pages

### Q: 如何使用自定义域名？

**A:**

1. 在仓库根目录创建`CNAME`文件
2. 写入你的域名（不带http://）
3. 在域名服务商处添加CNAME记录指向`username.github.io`
4. 等待DNS生效（可能需要几小时）

## 配置问题

### Q: 侧边栏不显示怎么办？

**A:** 检查：

1. 配置中是否启用了侧边栏

```javascript
window.$docsify = {
  loadSidebar: true
}
```

2. `_sidebar.md`文件是否存在
3. 文件路径和格式是否正确
4. 浏览器控制台是否有错误

### Q: 如何自定义侧边栏标题？

**A:** 在`index.html`中配置：

```javascript
window.$docsify = {
  name: '知识库标题',
  logo: '/_media/icon.svg'  // 可选logo
}
```

### Q: 搜索功能不工作？

**A:** 确保：

1. 引入了搜索插件

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>
```

2. 配置了搜索选项

```javascript
window.$docsify = {
  search: {
    paths: 'auto',
    placeholder: '搜索',
    depth: 6
  }
}
```

3. 清除浏览器缓存后重试

### Q: 如何修改主题颜色？

**A:** 两种方式：

1. **使用配置**

```javascript
window.$docsify = {
  themeColor: '#3F51B5'
}
```

2. **使用CSS变量**

```css
:root {
  --theme-color: #3F51B5;
}
```

## 内容问题

### Q: 图片不显示怎么办？

**A:** 检查：

1. **路径是否正确**

```markdown
<!-- 相对路径 -->
![](../assets/images/pic.png)

<!-- 绝对路径 -->
![](/assets/images/pic.png)
```

2. **文件是否存在**
3. **文件名大小写是否匹配**
4. **是否在浏览器控制台看到404错误**

### Q: 链接跳转不正确？

**A:**

1. **相对路径链接**

```markdown
[链接](./page.md)
[上级目录](../README.md)
```

2. **绝对路径链接**

```markdown
[首页](/)
[指南](/guide/README.md)
```

3. **锚点链接**

```markdown
[跳转](#标题)
```

### Q: 代码块没有高亮？

**A:** 确保：

1. 指定了语言

````markdown
```javascript
console.log('Hello');
```
````

2. 引入了对应语言的Prism组件

```html
<script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-javascript.min.js"></script>
```

### Q: 如何显示代码行号？

**A:** 使用Prism的行号插件：

```html
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/prismjs/plugins/line-numbers/prism-line-numbers.css">
<script src="//cdn.jsdelivr.net/npm/prismjs/plugins/line-numbers/prism-line-numbers.min.js"></script>
```

在代码块中添加行号类：

````markdown
```javascript line-numbers
function hello() {
  console.log('Hello');
}
```
````

### Q: 表格显示不正常？

**A:** 确保表格格式正确：

```markdown
| 列1 | 列2 | 列3 |
| --- | --- | --- |
| 内容1 | 内容2 | 内容3 |
```

注意：
- 表头和内容之间要有分隔行
- 每行的列数要一致
- 表格前后要有空行

## 功能问题

### Q: 如何添加页脚？

**A:** 使用页脚插件：

```html
<script src="//unpkg.com/docsify-footer-enh/dist/docsify-footer-enh.min.js"></script>
```

```javascript
window.$docsify = {
  footer: {
    copy: '<span>Copyright &copy; 2025</span>',
    auth: 'by Your Name',
    pre: '<hr/>',
    style: 'text-align: center;'
  }
}
```

### Q: 如何添加评论系统？

**A:** 可以使用Gitalk或Disqus：

**Gitalk示例：**

```html
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/gitalk/dist/gitalk.css">
<script src="//cdn.jsdelivr.net/npm/gitalk/dist/gitalk.min.js"></script>

<script>
const gitalk = new Gitalk({
  clientID: 'GitHub Application Client ID',
  clientSecret: 'GitHub Application Client Secret',
  repo: 'GitHub repo',
  owner: 'GitHub repo owner',
  admin: ['GitHub repo admin']
});
gitalk.render('gitalk-container');
</script>
```

### Q: 如何实现多语言切换？

**A:** 创建多语言目录结构：

```
docs/
├── README.md       # 默认语言
├── zh-cn/
│   └── README.md
└── en/
    └── README.md
```

配置：

```javascript
window.$docsify = {
  nameLink: {
    '/zh-cn/': '/zh-cn/',
    '/en/': '/en/',
    '/': '/'
  },
  alias: {
    '/zh-cn/_sidebar.md': '/zh-cn/_sidebar.md',
    '/en/_sidebar.md': '/en/_sidebar.md'
  }
}
```

导航栏（`_navbar.md`）：

```markdown
* 语言
  * [:cn: 中文](/)
  * [:us: English](/en/)
```

### Q: 如何添加全局变量？

**A:** 使用插件：

```javascript
window.$docsify = {
  plugins: [
    function(hook, vm) {
      hook.beforeEach(function(content) {
        // 替换变量
        content = content.replace(/\{\{version\}\}/g, '1.0.0');
        content = content.replace(/\{\{author\}\}/g, 'Your Name');
        return content;
      });
    }
  ]
}
```

在Markdown中使用：

```markdown
当前版本：{{version}}
作者：{{author}}
```

## 性能问题

### Q: 页面加载速度慢怎么办？

**A:** 优化建议：

1. **使用CDN加速**

```html
<script src="//cdn.jsdelivr.net/npm/docsify@4"></script>
```

2. **减少插件数量**

只加载必要的插件

3. **压缩图片**

使用工具压缩图片大小

4. **启用浏览器缓存**

配置缓存策略

5. **使用PWA**

```javascript
window.$docsify = {
  pwa: {
    enabled: true,
    path: '/sw.js'
  }
}
```

### Q: 文档很大时如何优化？

**A:**

1. **分页加载**

使用分页插件

2. **延迟加载图片**

```markdown
![](image.png ':lazy')
```

3. **拆分文档**

将大文档拆分为多个小文档

4. **使用搜索缓存**

```javascript
window.$docsify = {
  search: {
    maxAge: 86400000  // 缓存1天
  }
}
```

## 样式问题

### Q: 如何修改字体？

**A:**

```css
body {
  font-family: 'Arial', 'Microsoft YaHei', sans-serif;
}

code {
  font-family: 'Monaco', 'Courier New', monospace;
}
```

### Q: 如何调整内容宽度？

**A:**

```css
.markdown-section {
  max-width: 1200px;  /* 默认900px */
}
```

### Q: 如何自定义侧边栏宽度？

**A:**

```css
.sidebar {
  width: 350px;  /* 默认300px */
}

.content {
  left: 350px;
}
```

### Q: 移动端显示不正常？

**A:** 确保：

1. 添加了viewport meta标签

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

2. 启用了导航栏合并

```javascript
window.$docsify = {
  mergeNavbar: true
}
```

3. 使用响应式CSS

```css
@media screen and (max-width: 768px) {
  .sidebar {
    width: 250px;
  }
}
```

## 其他问题

### Q: 如何嵌入视频？

**A:**

```markdown
<!-- YouTube -->
<iframe width="560" height="315" src="https://www.youtube.com/embed/VIDEO_ID" frameborder="0" allowfullscreen></iframe>

<!-- Bilibili -->
<iframe src="//player.bilibili.com/player.html?bvid=BV_ID" scrolling="no" border="0" frameborder="no" allowfullscreen="true"></iframe>
```

### Q: 如何导出PDF？

**A:** 使用浏览器打印功能：

1. 打开要导出的页面
2. 按Ctrl+P（或Cmd+P）
3. 选择"另存为PDF"
4. 调整设置后保存

或使用专业工具：
- Puppeteer
- wkhtmltopdf
- 浏览器插件

### Q: 如何实现暗黑模式？

**A:**

1. **使用暗黑主题**

```html
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/dark.css">
```

2. **自定义主题切换**

```javascript
// 创建切换按钮
const toggleButton = document.createElement('button');
toggleButton.textContent = '切换主题';
toggleButton.onclick = function() {
  document.body.classList.toggle('dark-mode');
};
document.body.appendChild(toggleButton);
```

```css
.dark-mode {
  --theme-color: #64b5f6;
  --text-color-base: #e0e0e0;
  background: #1e1e1e;
  color: #e0e0e0;
}
```

## 获取帮助

如果以上问题没有解决你的疑问，可以：

1. 查看[Docsify官方文档](https://docsify.js.org)
2. 在[GitHub Issues](https://github.com/docsifyjs/docsify/issues)搜索或提问
3. 加入社区讨论
4. 查看[示例网站](https://github.com/docsifyjs/awesome-docsify)

---

💡 **提示**：遇到问题时，先检查浏览器控制台的错误信息，通常能快速定位问题。

