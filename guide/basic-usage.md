# 基本使用

## Markdown语法

Docsify使用Markdown语法编写文档，这里介绍一些常用语法。

### 标题

```markdown
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
```

### 文本样式

```markdown
**粗体文本**
*斜体文本*
~~删除线~~
`代码`
```

效果：
- **粗体文本**
- *斜体文本*
- ~~删除线~~
- `代码`

### 列表

无序列表：
```markdown
- 项目1
- 项目2
  - 子项目2.1
  - 子项目2.2
```

有序列表：
```markdown
1. 第一项
2. 第二项
3. 第三项
```

### 链接和图片

```markdown
[链接文本](https://example.com)
![图片描述](path/to/image.jpg)
```

### 表格

```markdown
| 列1 | 列2 | 列3 |
| --- | --- | --- |
| 内容1 | 内容2 | 内容3 |
| 内容4 | 内容5 | 内容6 |
```

效果：

| 列1 | 列2 | 列3 |
| --- | --- | --- |
| 内容1 | 内容2 | 内容3 |
| 内容4 | 内容5 | 内容6 |

### 代码块

使用三个反引号包裹代码，并指定语言：

````markdown
```javascript
function hello() {
  console.log('Hello World!');
}
```
````

效果：

```javascript
function hello() {
  console.log('Hello World!');
}
```

## Docsify特殊语法

### 提示框

```markdown
?> 这是一个提示框

!> 这是一个警告框
```

效果：

?> 这是一个提示框

!> 这是一个警告框

### 忽略编译

使用`<!-- {docsify-ignore} -->`可以让标题不出现在侧边栏：

```markdown
## 标题 <!-- {docsify-ignore} -->
```

忽略所有标题：

```markdown
## 标题 <!-- {docsify-ignore-all} -->
```

### 任务列表

```markdown
- [x] 已完成任务
- [ ] 未完成任务
- [ ] 待办事项
```

效果：

- [x] 已完成任务
- [ ] 未完成任务
- [ ] 待办事项

### Emoji表情

可以直接使用Emoji代码：

```markdown
:smile: :heart: :rocket: :star:
```

效果：:smile: :heart: :rocket: :star:

## 组织内容

### 创建新页面

1. 在相应目录下创建`.md`文件
2. 在`_sidebar.md`中添加链接
3. 开始编写内容

### 侧边栏配置

编辑`_sidebar.md`文件：

```markdown
* [首页](/)
* [指南](guide/)
  * [安装](guide/installation.md)
  * [使用](guide/usage.md)
* [教程](tutorial/)
```

### 导航栏配置

编辑`_navbar.md`文件：

```markdown
* [首页](/)
* [指南](guide/)
* [关于](about.md)
```

## 文档链接

### 相对路径

```markdown
[链接到其他页面](guide/installation.md)
[链接到同目录](./another-page.md)
[链接到上级目录](../README.md)
```

### 锚点链接

```markdown
[跳转到标题](#标题名称)
```

## 嵌入内容

### 嵌入文件

```markdown
[filename](path/to/file.md ':include')
```

### 嵌入代码

```markdown
[](path/to/code.js ':include :type=code')
```

### 嵌入视频

```markdown
[](https://www.youtube.com/embed/video-id ':include :type=iframe width=100% height=400px')
```

## 自定义样式

在`index.html`中添加自定义CSS：

```html
<style>
  :root {
    --theme-color: #42b983;
  }
  
  .markdown-section {
    max-width: 900px;
  }
</style>
```

## 下一步

- [进阶教程](tutorial/advanced.md)
- [最佳实践](tutorial/best-practices.md)

