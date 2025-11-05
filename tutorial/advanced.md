# 进阶教程

深入了解Docsify的高级功能和最佳实践。

## 自定义主题

### 使用官方主题

Docsify提供了多个官方主题：

```html
<!-- Vue主题（默认） -->
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/vue.css">

<!-- Buble主题 -->
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/buble.css">

<!-- Dark主题 -->
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/dark.css">

<!-- Pure主题 -->
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/pure.css">
```

### 自定义CSS变量

通过CSS变量自定义主题颜色：

```css
:root {
  --theme-color: #42b983;
  --theme-color-dark: #369b73;
  --text-color-base: #333;
  --text-color-secondary: #7f8c8d;
  --heading-color: #2c3e50;
  --link-color: var(--theme-color);
  --sidebar-width: 300px;
  --content-max-width: 900px;
}
```

### 创建自定义主题

创建`custom.css`文件：

```css
/* 自定义侧边栏样式 */
.sidebar {
  background: linear-gradient(180deg, #667eea 0%, #764ba2 100%);
  color: white;
}

.sidebar-nav li a {
  color: rgba(255, 255, 255, 0.8);
}

.sidebar-nav li a:hover {
  color: white;
  font-weight: bold;
}

/* 自定义内容区域 */
.markdown-section {
  padding: 30px 40px;
}

.markdown-section h1 {
  border-bottom: 3px solid var(--theme-color);
  padding-bottom: 10px;
}

/* 自定义代码块 */
.markdown-section pre {
  border-radius: 8px;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
}
```

在`index.html`中引入：

```html
<link rel="stylesheet" href="custom.css">
```

## 插件开发

### 创建简单插件

创建一个显示阅读时间的插件：

```javascript
// plugins/reading-time.js
(function() {
  var plugin = function(hook, vm) {
    hook.beforeEach(function(content) {
      // 计算字数
      var words = content.match(/[\u4e00-\u9fa5]|[a-zA-Z0-9]+/g)?.length || 0;
      // 假设每分钟阅读500字
      var minutes = Math.ceil(words / 500);
      
      // 在内容开头添加阅读时间
      var readingTime = `\n\n> ⏱️ 预计阅读时间：${minutes} 分钟\n\n`;
      
      return readingTime + content;
    });
  };
  
  window.$docsify = window.$docsify || {};
  window.$docsify.plugins = [].concat(plugin, window.$docsify.plugins || []);
})();
```

在`index.html`中引入：

```html
<script src="plugins/reading-time.js"></script>
```

### 高级插件示例

创建一个目录插件：

```javascript
(function() {
  var plugin = function(hook, vm) {
    var generateTOC = function(content) {
      var headings = content.match(/#{2,4}\s.+/g) || [];
      if (headings.length === 0) return '';
      
      var toc = '<div class="toc-container">\n<h2>目录</h2>\n<ul>\n';
      
      headings.forEach(function(heading) {
        var level = heading.match(/#{2,4}/)[0].length;
        var text = heading.replace(/#{2,4}\s/, '');
        var id = text.toLowerCase().replace(/\s/g, '-');
        var indent = '  '.repeat(level - 2);
        
        toc += `${indent}<li><a href="#${id}">${text}</a></li>\n`;
      });
      
      toc += '</ul>\n</div>\n\n';
      return toc;
    };
    
    hook.beforeEach(function(content) {
      var toc = generateTOC(content);
      return toc + content;
    });
  };
  
  window.$docsify.plugins = [].concat(plugin, window.$docsify.plugins || []);
})();
```

## 多语言支持

### 配置多语言

创建语言目录结构：

```
docs/
├── README.md          # 中文首页
├── zh-cn/
│   ├── README.md
│   └── guide.md
└── en/
    ├── README.md
    └── guide.md
```

配置语言切换：

```javascript
window.$docsify = {
  name: '知识库',
  nameLink: {
    '/zh-cn/': '/zh-cn/',
    '/en/': '/en/',
    '/': '/'
  },
  
  // 导航栏语言切换
  loadNavbar: true,
  
  // 侧边栏
  loadSidebar: true,
  alias: {
    '/zh-cn/_sidebar.md': '/zh-cn/_sidebar.md',
    '/en/_sidebar.md': '/en/_sidebar.md'
  }
}
```

导航栏配置（`_navbar.md`）：

```markdown
* 语言
  * [:cn: 中文](/)
  * [:us: English](/en/)
  * [:jp: 日本語](/ja/)
```

## 高级配置

### SEO优化

```html
<!-- 添加meta标签 -->
<meta name="description" content="知识库描述">
<meta name="keywords" content="关键词1, 关键词2">
<meta name="author" content="作者名称">

<!-- Open Graph -->
<meta property="og:title" content="知识库标题">
<meta property="og:description" content="知识库描述">
<meta property="og:image" content="封面图片URL">
<meta property="og:url" content="网站URL">
```

### 性能优化

```javascript
window.$docsify = {
  // 路由模式
  routerMode: 'history',
  
  // 延迟加载
  executeScript: true,
  
  // 缓存
  requestHeaders: {
    'cache-control': 'max-age=600'
  },
  
  // 代码高亮异步加载
  noCompileLinks: ['/foo', '/bar/.*']
}
```

### PWA支持

创建`sw.js`文件：

```javascript
/* sw.js */
self.addEventListener('install', function(event) {
  event.waitUntil(
    caches.open('docsify-cache').then(function(cache) {
      return cache.addAll([
        '/',
        '/index.html',
        '/README.md',
        'https://cdn.jsdelivr.net/npm/docsify@4/lib/docsify.min.js'
      ]);
    })
  );
});

self.addEventListener('fetch', function(event) {
  event.respondWith(
    caches.match(event.request).then(function(response) {
      return response || fetch(event.request);
    })
  );
});
```

配置PWA：

```javascript
window.$docsify = {
  pwa: {
    enabled: true,
    path: '/sw.js'
  }
}
```

## 集成第三方服务

### Google Analytics

```html
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_MEASUREMENT_ID');
</script>
```

### Gitalk评论系统

```html
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/gitalk/dist/gitalk.css">
<script src="//cdn.jsdelivr.net/npm/gitalk/dist/gitalk.min.js"></script>

<script>
  var gitalk = new Gitalk({
    clientID: 'GitHub Application Client ID',
    clientSecret: 'GitHub Application Client Secret',
    repo: 'GitHub repo',
    owner: 'GitHub repo owner',
    admin: ['GitHub repo admin'],
    distractionFreeMode: false
  });
</script>
```

### 百度统计

```html
<script>
var _hmt = _hmt || [];
(function() {
  var hm = document.createElement("script");
  hm.src = "https://hm.baidu.com/hm.js?YOUR_SITE_ID";
  var s = document.getElementsByTagName("script")[0]; 
  s.parentNode.insertBefore(hm, s);
})();
</script>
```

## 自动化部署

### GitHub Actions

创建`.github/workflows/deploy.yml`：

```yaml
name: Deploy Docsify

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./
```

### Vercel部署

创建`vercel.json`：

```json
{
  "version": 2,
  "builds": [
    {
      "src": "index.html",
      "use": "@vercel/static"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "/index.html"
    }
  ]
}
```

## 下一步

- [最佳实践](tutorial/best-practices.md)
- [常见问题](../reference/faq.md)

