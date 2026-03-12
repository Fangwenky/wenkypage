# {{ 你的名字 }}的个人主页

基于 Hugo + Congo 主题构建的轻量级个人主页，适配 1C1G 服务器部署。

## ✨ 特性

- 🚀 **轻量快速**：纯静态生成，1C1G 服务器轻松运行
- 🌙 **暗黑模式**：支持明暗主题切换
- 📱 **响应式设计**：完美适配手机、平板、桌面
- 💬 **评论系统**：集成 Waline 评论功能
- 📝 **Markdown 支持**：使用 Markdown 编写内容
- 🎨 **代码高亮**：内置代码高亮功能

## 🛠 技术栈

- [Hugo](https://gohugo.io/) - 静态网站生成器
- [Congo 主题](https://github.com/jpanther/congo) - 轻量级 Hugo 主题
- [Waline](https://waline.js.org/) - 评论系统

## 🚀 快速开始

### 1. 克隆项目

```bash
git clone https://github.com/{{ 你的GitHub用户名 }}/wenkypage.git
cd wenkypage
```

### 2. 安装主题

Congo 主题作为 Git 子模块安装：

```bash
git submodule add https://github.com/jpanther/congo.git themes/congo
```

### 3. 本地预览

```bash
hugo server
```

然后访问 http://localhost:1313 查看网站。

### 4. 构建静态文件

```bash
hugo
```

生成的静态文件位于 `public/` 目录。

## 📝 配置说明

### 1. 修改配置文件

编辑 `config.toml` 文件，修改以下内容：

```toml
baseURL = "https://your-domain.com/"
languageCode = "zh-cn"
title = "你的名字"

[params]
  author = "你的名字"
  description = "你的个人简介"
  
  [params.social]
    github = "你的GitHub用户名"
    email = "你的邮箱"
```

### 2. 修改个人信息

编辑以下文件替换为你自己的信息：

- `content/_index.md` - 首页内容
- `content/about.md` - 关于我页面
- `content/projects.md` - 项目展示页面
- `content/contact.md` - 联系方式页面

### 3. 配置 Waline 评论

1. 部署 Waline 服务（参考 [Waline 官方文档](https://waline.js.org/deploy/vercel/)）
2. 在 `config.toml` 中配置你的 Waline 服务地址：

```toml
[params.waline]
  serverURL = "https://your-waline-service.vercel.app"
```

## 📂 目录结构

```
wenkypage/
├── config.toml          # 配置文件
├── content/             # 内容文件
│   ├── _index.md       # 首页
│   ├── about.md        # 关于我
│   ├── projects.md     # 项目展示
│   ├── contact.md      # 联系方式
│   └── posts/          # 博客文章
├── layouts/            # 布局文件
│   └── shortcodes/     # 短代码
│       └── waline.html # Waline 评论短代码
├── static/             # 静态资源
├── themes/             # 主题文件
└── .gitignore         # Git 忽略文件
```

## 🖥️ 部署到 Nginx 服务器

### 1. 构建静态文件

```bash
hugo
```

### 2. 上传到服务器

使用 scp 命令上传：

```bash
scp -r public/* user@your-server:/var/www/html/
```

或使用 rsync：

```bash
rsync -avz --delete public/ user@your-server:/var/www/html/
```

### 3. 配置 Nginx

确保 Nginx 已安装，然后配置：

```nginx
server {
    listen 80;
    server_name your-domain.com;
    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }

    # 开启 gzip 压缩
    gzip on;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

    # 缓存静态资源
    location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
        expires 30d;
        add_header Cache-Control "public, no-transform";
    }
}
```

### 4. 重启 Nginx

```bash
sudo nginx -t
sudo systemctl reload nginx
```

## 💬 Waline 集成说明

### 使用短代码

在任意 Markdown 文件中使用：

```markdown
{{< waline >}}
```

### 自定义配置

```markdown
{{< waline serverURL="https://your-waline.vercel.app" wordLimit="500" >}}
```

### 配置参数

| 参数 | 说明 | 默认值 |
|------|------|--------|
| serverURL | Waline 服务地址 | config.toml 中的配置 |
| emoji | 表情包配置 | weibo 表情包 |
| requiredMeta | 必填项 | nick, mail |
| login | 登录模式 | enable |
| wordLimit | 评论字数限制 | 1000 |
| pageSize | 每页评论数 | 10 |

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 许可证

MIT License - 欢迎自由使用和修改！

---

如有问题，欢迎在 [GitHub Issues](https://github.com/{{ 你的GitHub用户名 }}/wenkypage/issues) 中提出。
