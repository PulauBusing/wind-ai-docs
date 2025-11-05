# API参考

完整的Docsify配置选项和API文档。

## 配置选项

### 基本配置

#### el

- 类型：`String`
- 默认值：`#app`

Docsify初始化的DOM元素。

```javascript
window.$docsify = {
  el: '#app'
}
```

#### repo

- 类型：`String`
- 默认值：`null`

GitHub仓库地址，会在页面右上角显示。

```javascript
window.$docsify = {
  repo: 'https://github.com/username/repo'
}
```

#### maxLevel

- 类型：`Number`
- 默认值：`6`

侧边栏中显示的最大标题层级。

```javascript
window.$docsify = {
  maxLevel: 4
}
```

#### subMaxLevel

- 类型：`Number`
- 默认值：`0`

当前页面内容目录的最大层级。

```javascript
window.$docsify = {
  subMaxLevel: 3
}
```

#### loadSidebar

- 类型：`Boolean | String`
- 默认值：`false`

加载自定义侧边栏。

```javascript
window.$docsify = {
  loadSidebar: true,
  // 或指定文件
  loadSidebar: '_sidebar.md'
}
```

#### loadNavbar

- 类型：`Boolean | String`
- 默认值：`false`

加载自定义导航栏。

```javascript
window.$docsify = {
  loadNavbar: true,
  // 或指定文件
  loadNavbar: '_navbar.md'
}
```

#### coverpage

- 类型：`Boolean | String | Array`
- 默认值：`false`

启用封面页。

```javascript
window.$docsify = {
  coverpage: true,
  // 或指定文件
  coverpage: '_coverpage.md',
  // 多个封面页
  coverpage: ['/', '/zh-cn/']
}
```

#### name

- 类型：`String`
- 默认值：`''`

文档站点名称，显示在侧边栏顶部。

```javascript
window.$docsify = {
  name: '我的知识库'
}
```

#### nameLink

- 类型：`String | Object`
- 默认值：`window.location.pathname`

点击站点名称跳转的链接。

```javascript
window.$docsify = {
  nameLink: '/',
  // 或多语言
  nameLink: {
    '/zh-cn/': '/zh-cn/',
    '/en/': '/en/',
    '/': '/'
  }
}
```

#### homepage

- 类型：`String`
- 默认值：`README.md`

首页文件路径。

```javascript
window.$docsify = {
  homepage: 'home.md'
}
```

### 主题配置

#### themeColor

- 类型：`String`
- 默认值：`#42b983`

主题颜色。

```javascript
window.$docsify = {
  themeColor: '#3F51B5'
}
```

### 路由配置

#### routerMode

- 类型：`String`
- 默认值：`hash`

路由模式，可选 `hash` 或 `history`。

```javascript
window.$docsify = {
  routerMode: 'history'
}
```

#### basePath

- 类型：`String`
- 默认值：``

文档根路径。

```javascript
window.$docsify = {
  basePath: '/docs/'
}
```

#### relativePath

- 类型：`Boolean`
- 默认值：`false`

启用相对路径。

```javascript
window.$docsify = {
  relativePath: true
}
```

#### alias

- 类型：`Object`
- 默认值：`{}`

路由别名。

```javascript
window.$docsify = {
  alias: {
    '/foo/(.*)': '/bar/$1',
    '/zh-cn/changelog': '/changelog',
    '/.*/_sidebar.md': '/_sidebar.md'
  }
}
```

#### auto2top

- 类型：`Boolean`
- 默认值：`false`

切换页面时自动跳转到顶部。

```javascript
window.$docsify = {
  auto2top: true
}
```

### Markdown配置

#### markdown

- 类型：`Object | Function`
- 默认值：`{}`

自定义Markdown解析规则。

```javascript
window.$docsify = {
  markdown: {
    smartypants: true,
    renderer: {
      link: function(href, title, text) {
        return `<a href="${href}" target="_blank">${text}</a>`;
      }
    }
  }
}
```

#### mergeNavbar

- 类型：`Boolean`
- 默认值：`false`

小屏设备下合并导航栏到侧边栏。

```javascript
window.$docsify = {
  mergeNavbar: true
}
```

#### formatUpdated

- 类型：`String | Function`
- 默认值：`''`

文档更新时间格式。

```javascript
window.$docsify = {
  formatUpdated: '{YYYY}/{MM}/{DD} {HH}:{mm}',
  // 或使用函数
  formatUpdated: function(time) {
    return time;
  }
}
```

### 搜索配置

#### search

- 类型：`Object`

全文搜索配置（需要search插件）。

```javascript
window.$docsify = {
  search: {
    maxAge: 86400000,           // 过期时间（毫秒）
    paths: 'auto',              // 搜索路径
    placeholder: '搜索',        // 占位符
    noData: '没有结果',         // 无结果提示
    depth: 6,                   // 搜索标题层级
    hideOtherSidebarContent: false  // 隐藏其他侧边栏内容
  }
}
```

### 执行脚本

#### executeScript

- 类型：`Boolean`
- 默认值：`false`

执行页面中的script标签。

```javascript
window.$docsify = {
  executeScript: true
}
```

!> **警告**：谨慎使用此选项，可能存在安全风险。

### 字数统计

#### count

- 类型：`Object`

字数统计配置（需要count插件）。

```javascript
window.$docsify = {
  count: {
    countable: true,
    fontsize: '0.9em',
    color: 'rgb(90,90,90)',
    language: 'chinese'
  }
}
```

### PWA配置

#### pwa

- 类型：`Object`

PWA配置。

```javascript
window.$docsify = {
  pwa: {
    enabled: true,
    path: '/sw.js'
  }
}
```

## Hooks API

Docsify提供了完整的生命周期钩子。

### init

初始化完成后调用。

```javascript
window.$docsify = {
  plugins: [
    function(hook, vm) {
      hook.init(function() {
        console.log('初始化完成');
      });
    }
  ]
}
```

### beforeEach

每次开始解析Markdown之前调用。

```javascript
hook.beforeEach(function(content) {
  // 修改内容
  return content + '\n\n---\n\n更新时间: ' + new Date();
});
```

### afterEach

解析Markdown后，渲染到页面前调用。

```javascript
hook.afterEach(function(html, next) {
  // 修改HTML
  html = html + '<footer>页脚内容</footer>';
  next(html);
});
```

### doneEach

每次页面渲染完成后调用。

```javascript
hook.doneEach(function() {
  console.log('页面渲染完成');
});
```

### mounted

初次渲染完成后调用。

```javascript
hook.mounted(function() {
  console.log('首次渲染完成');
});
```

### ready

初始化并第一次渲染完成后调用。

```javascript
hook.ready(function() {
  console.log('应用已准备就绪');
});
```

## VM实例

插件中可以访问的vm实例属性：

```javascript
window.$docsify = {
  plugins: [
    function(hook, vm) {
      console.log(vm.route);      // 当前路由信息
      console.log(vm.config);     // 配置对象
      console.log(vm.compiler);   // Markdown编译器
    }
  ]
}
```

### vm.route

- `path`：当前路径
- `file`：当前文件路径
- `query`：查询参数

### vm.config

当前配置对象。

### vm.compiler

Markdown编译器实例。

## 下一步

- [配置说明](reference/configuration.md)
- [常见问题](reference/faq.md)

