# Cloudflare Pages Demo Collection

这个仓库收集了几套从入门到实战的 Cloudflare Pages 示例，重点演示这几类能力：

- 文本变量
- 密钥
- KV 绑定
- D1 绑定
- Pages Functions

适合用来理解 Cloudflare Pages 里最常见的几个概念，以及它们在博客场景里的实际用法。

## 仓库结构

- `变量demo/`
  - 演示文本变量和密钥
  - 适合先理解 `context.env.xxx` 怎么读普通配置和敏感配置
- `绑定demo/`
  - 演示 KV 绑定
  - 用一个最小计数器说明“绑定”不是普通字符串，而是可操作的资源对象
- `D1评论demo/`
  - 演示 D1 数据库绑定
  - 用评论写入和读取说明数据库绑定怎么用
- `博客实战demo/`
  - 把文本变量、密钥、KV、D1 串起来
  - 更接近真实博客项目

## 推荐阅读顺序

1. `变量demo`
2. `绑定demo`
3. `D1评论demo`
4. `博客实战demo`

这样看下来会比较顺：

- 先理解“变量和密钥是什么”
- 再理解“绑定是什么”
- 再理解“数据库绑定怎么用”
- 最后看“怎么把它们组合进一个博客”

## 各 Demo 说明

### 1. 变量demo

目录：[`变量demo`](./变量demo)

这个示例包含：

- `SITE_NAME`：文本变量
- `MY_TOKEN`：密钥

演示内容：

- 页面调用 `/api/site` 读取文本变量
- 页面调用 `/api/check` 演示密钥校验

适合用来理解：

- 文本变量适合放普通配置
- 密钥适合放 token、API key、密码等敏感值

### 2. 绑定demo

目录：[`绑定demo`](./绑定demo)

这个示例使用：

- `COUNTER`：KV 绑定

演示内容：

- `/api/counter` 读取当前计数
- `/api/increment` 写入并自增

适合用来理解：

- 绑定不是字符串
- `context.env.COUNTER` 是一个 KV 资源对象
- 可以直接调用 `.get()` 和 `.put()`

### 3. D1评论demo

目录：[`D1评论demo`](./D1评论demo)

这个示例使用：

- `DB`：D1 绑定

演示内容：

- `/api/comment` 写入评论
- `/api/comments` 读取评论列表

适合用来理解：

- D1 绑定怎么接入 Pages
- `context.env.DB.prepare(...).bind(...).run()` 的基本用法
- 评论、留言、文章元数据这类结构化数据为什么更适合数据库

### 4. 博客实战demo

目录：[`博客实战demo`](./博客实战demo)

这个示例组合了：

- 文本变量
  - `SITE_NAME`
  - `SITE_DESCRIPTION`
  - `ADMIN_EMAIL`
- 密钥
  - `ADMIN_TOKEN`
- KV 绑定
  - `VIEWS`
- D1 绑定
  - `DB`

演示内容：

- 页面加载时读取站点配置
- 文章阅读量通过 KV 自增
- 评论通过 D1 读取和写入
- 管理接口通过密钥校验保护

这个目录最接近真实博客项目结构。

## 如何部署

推荐方式：

1. 把这个仓库连接到 Cloudflare Pages
2. 选择你要部署的某一个 demo 目录作为项目根目录
3. 配置对应的变量、密钥和绑定
4. 重新部署

如果你是给每个 demo 分别建一个 Pages 项目，通常这样配：

- `变量demo`
  - 根目录：`变量demo`
- `绑定demo`
  - 根目录：`绑定demo`
- `D1评论demo`
  - 根目录：`D1评论demo`
- `博客实战demo`
  - 根目录：`博客实战demo`

## Pages 构建设置建议

这些 demo 都是最简单的静态文件 + `functions/` 目录结构，一般这样填：

- 框架预设：`无`
- 构建命令：留空
- 构建输出目录：`/`
- 根目录：填写对应 demo 文件夹名

## 补充说明

- 每个 demo 目录里都有自己的 `README.md`
- 具体变量名、绑定名、建表 SQL 都写在各自目录里
- 如果你只是想先跑通一个，建议从 `变量demo` 开始

## 学完这几个 demo 你会掌握什么

- Pages 静态文件和 Pages Functions 的区别
- 文本变量和密钥的区别
- KV 绑定和 D1 绑定的基本用法
- 怎么把这些能力组合成一个简单博客
