# 配置说明

详细的配置选项说明和示例。

## 完整配置示例

```javascript
window.$docsify = {
  // 基础配置
  el: '#app',
  name: '知识库',
  repo: 'https://github.com/username/repo',
  homepage: 'README.md',
  
  // 侧边栏和导航
  loadSidebar: true,
  loadNavbar: true,
  coverpage: true,
  
  // 层级配置
  maxLevel: 4,
  subMaxLevel: 3,
  
  // 路由配置
  routerMode: 'history',
  basePath: '/',
  relativePath: false,
  auto2top: true,
  
  // 别名配置
  alias: {
    '/.*/_sidebar.md': '/_sidebar.md',
    '/.*/_navbar.md': '/_navbar.md'
  },
  
  // Markdown配置
  markdown: {
    smartypants: true,
    renderer: {
      code: function(code, lang) {
        // 自定义代码渲染
        return `<pre><code class="language-${lang}">${code}</code></pre>`;
      }
    }
  },
  
  // 搜索配置
  search: {
    maxAge: 86400000,
    paths: 'auto',
    placeholder: '搜索',
    noData: '没有结果',
    depth: 6,
    hideOtherSidebarContent: false
  },
  
  // 字数统计
  count: {
    countable: true,
    fontsize: '0.9em',
    color: 'rgb(90,90,90)',
    language: 'chinese'
  },
  
  // 分页导航
  pagination: {
    previousText: '上一章节',
    nextText: '下一章节',
    crossChapter: true,
    crossChapterText: true
  },
  
  // 代码复制
  copyCode: {
    buttonText: '复制',
    errorText: '错误',
    successText: '已复制'
  },
  
  // 外部链接
  externalLinkTarget: '_blank',
  externalLinkRel: 'noopener',
  
  // 更新时间
  formatUpdated: '{YYYY}/{MM}/{DD} {HH}:{mm}',
  
  // 合并导航栏
  mergeNavbar: true,
  
  // 主题颜色
  themeColor: '#42b983',
  
  // 执行脚本（谨慎使用）
  executeScript: false,
  
  // 404页面
  notFoundPage: true,
  
  // PWA
  pwa: {
    enabled: false,
    path: '/sw.js'
  },
  
  // 插件
  plugins: [
    // 自定义插件
  ]
}
```

## 分类配置详解

### 内容配置

#### 侧边栏

**自动生成侧边栏**

```javascript
window.$docsify = {
  loadSidebar: true,
  maxLevel: 4,  // 显示到h4
  subMaxLevel: 3  // 当前页目录显示到h3
}
```

**自定义侧边栏文件**

```javascript
window.$docsify = {
  loadSidebar: 'summary.md'
}
```

**多个侧边栏**

```javascript
window.$docsify = {
  loadSidebar: true,
  alias: {
    '/guide/_sidebar.md': '/guide/_sidebar.md',
    '/tutorial/_sidebar.md': '/tutorial/_sidebar.md',
    '/.*/_sidebar.md': '/_sidebar.md'
  }
}
```

#### 导航栏

```javascript
window.$docsify = {
  loadNavbar: true,
  // 小屏合并到侧边栏
  mergeNavbar: true
}
```

#### 封面页

**单个封面**

```javascript
window.$docsify = {
  coverpage: true
}
```

**多个封面**

```javascript
window.$docsify = {
  coverpage: ['/', '/zh-cn/'],
  // 只在首页显示
  onlyCover: false
}
```

创建`_coverpage.md`：

```markdown
![logo](_media/icon.svg)

# 知识库

> 基于Docsify的现代化文档系统

- 简单易用
- 功能强大
- 美观现代

[GitHub](https://github.com)
[开始使用](#快速开始)

<!-- 背景颜色 -->
![color](#42b983)
```

### 样式配置

#### 主题选择

```html
<!-- Vue主题 -->
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/vue.css">

<!-- Buble主题 -->
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/buble.css">

<!-- Dark主题 -->
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/dark.css">

<!-- Pure主题 -->
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/pure.css">
```

#### 自定义颜色

```css
:root {
  /* 主题色 */
  --theme-color: #42b983;
  --theme-color-dark: #369b73;
  
  /* 文字颜色 */
  --text-color-base: #333;
  --text-color-secondary: #7f8c8d;
  --text-color-tertiary: #848484;
  
  /* 标题颜色 */
  --heading-color: #2c3e50;
  
  /* 链接颜色 */
  --link-color: var(--theme-color);
  --link-color-hover: var(--theme-color-dark);
  
  /* 侧边栏 */
  --sidebar-width: 300px;
  --sidebar-background: white;
  
  /* 内容区域 */
  --content-max-width: 900px;
  
  /* 代码块 */
  --code-font-family: 'Monaco', 'Courier New', monospace;
  --code-background: #f8f8f8;
  
  /* 表格 */
  --table-border-color: #dfe2e5;
  --table-row-odd-background: #f6f8fa;
}
```

### 插件配置

#### 全文搜索

```javascript
window.$docsify = {
  search: {
    maxAge: 86400000,              // 缓存过期时间（1天）
    paths: 'auto',                 // 自动搜索所有路径
    placeholder: '搜索',           // 输入框占位符
    noData: '没有结果',            // 无结果提示
    depth: 6,                      // 搜索标题深度
    hideOtherSidebarContent: false, // 是否隐藏其他侧边栏内容
    namespace: 'website-1',        // 命名空间（多站点共存）
    
    // 自定义路径
    paths: [
      '/guide/',
      '/tutorial/',
      '/reference/'
    ],
    
    // 路径过滤
    pathNamespaces: ['/zh-cn', '/en'],
    
    // 搜索结果高亮
    highlightMatch: true
  }
}
```

引入搜索插件：

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>
```

#### 代码复制

```javascript
window.$docsify = {
  copyCode: {
    buttonText: '复制',
    errorText: '错误',
    successText: '已复制'
  }
}
```

```html
<script src="//cdn.jsdelivr.net/npm/docsify-copy-code@2"></script>
```

#### 图片缩放

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/zoom-image.min.js"></script>
```

配置忽略特定图片：

```markdown
![](image.png ':no-zoom')
```

#### 分页导航

```javascript
window.$docsify = {
  pagination: {
    previousText: '上一章节',
    nextText: '下一章节',
    crossChapter: true,
    crossChapterText: true
  }
}
```

```html
<script src="//cdn.jsdelivr.net/npm/docsify-pagination/dist/docsify-pagination.min.js"></script>
```

#### 字数统计

```javascript
window.$docsify = {
  count: {
    countable: true,
    position: 'top',
    margin: '10px',
    float: 'right',
    fontsize: '0.9em',
    color: 'rgb(90,90,90)',
    language: 'chinese',
    localization: {
      words: '字',
      minute: '分钟'
    },
    isExpected: true
  }
}
```

```html
<script src="//unpkg.com/docsify-count/dist/countable.js"></script>
```

#### Emoji支持

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/emoji.min.js"></script>
```

#### 外部脚本

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/external-script.min.js"></script>
```

```javascript
window.$docsify = {
  executeScript: true
}
```

### 代码高亮配置

引入Prism语言组件：

```html
<!-- JavaScript -->
<script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-javascript.min.js"></script>

<!-- Python -->
<script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-python.min.js"></script>

<!-- Java -->
<script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-java.min.js"></script>

<!-- Go -->
<script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-go.min.js"></script>

<!-- Bash -->
<script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-bash.min.js"></script>

<!-- SQL -->
<script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-sql.min.js"></script>

<!-- JSON -->
<script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-json.min.js"></script>

<!-- YAML -->
<script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-yaml.min.js"></script>
```

### 国际化配置

```javascript
window.$docsify = {
  name: {
    '/zh-cn/': '中文文档',
    '/en/': 'English Docs',
    '/': 'Documentation'
  },
  nameLink: {
    '/zh-cn/': '/zh-cn/',
    '/en/': '/en/',
    '/': '/'
  },
  loadSidebar: true,
  alias: {
    '/zh-cn/_sidebar.md': '/zh-cn/_sidebar.md',
    '/en/_sidebar.md': '/en/_sidebar.md',
    '/.*/_sidebar.md': '/_sidebar.md'
  },
  fallbackLanguages: ['zh-cn', 'en']
}
```

## 环境变量

可以在配置中使用环境变量：

```javascript
window.$docsify = {
  repo: process.env.REPO_URL || 'https://github.com/default',
  name: process.env.SITE_NAME || '默认名称'
}
```

## 下一步

- [常见问题](reference/faq.md)
- [API参考](reference/README.md)

