Mengyu Notes


📝 Mengyu 的个人笔记站点，记录技术与生活


🌐 在线访问: imengyu.space


关于本站


Mengyu Notes 是一个基于 Hugo 构建的个人博客，使用 PaperMod 主题，部署在 Cloudflare Pages 上。在这里分享技术学习笔记、开发经验总结和日常生活记录。
技术栈


组件	技术
静态站点生成	Hugo
主题	PaperMod
部署	Cloudflare Pages
评论系统	Giscus（基于 GitHub Discussions）
语言	中文
站点特性


🌗 深色/浅色模式 — 自动跟随系统切换
🔍 全文搜索 — 基于 Hugo JSON 输出的客户端搜索
📑 文章目录 — 自动生成 TOC，默认展开
⏱ 阅读时间 & 字数统计 — 文章元信息自动展示
🍞 面包屑导航 — 清晰的页面层级关系
💬 Giscus 评论 — 基于 GitHub Discussions，支持表情反馈
📄 版权声明 — 文章底部自动添加 CC BY-NC-SA 4.0 版权信息
📋 代码复制按钮 — 一键复制代码块
🔝 返回顶部 — 长页面快速回到顶部
项目结构


plaintext
mengyu-notes/
├── archetypes/
│   └── default.md           # 文章模板
├── assets/
│   └── css/extended/
│       └── custom.css       # 自定义样式
├── content/
│   ├── about/
│   │   └── index.md         # 关于页面
│   ├── posts/               # 博客文章
│   │   ├── hello-world.md
│   │   ├── why-choose-cloudflare.md
│   │   ├── online-exam-system.md
│   │   └── daily-hn-archives.md
│   ├── archives.md          # 归档页
│   └── search.md            # 搜索页
├── layouts/
│   ├── _default/
│   │   └── single.html      # 文章单页模板（含版权声明）
│   ├── partials/
│   │   ├── comments.html    # Giscus 评论组件
│   │   └── post_copyright.html  # 版权声明组件
│   └── index.html           # 首页模板
├── static/                  # 静态资源
├── themes/PaperMod/         # PaperMod 主题
├── hugo.toml                # Hugo 配置文件
└── public/                  # 构建输出目录

本地开发
前置要求


Hugo (_extended 版本，建议 v0.159+)
Git
快速开始


bash
# 克隆仓库
git clone https://github.com/L5T2Y0/mengyu-notes.git
cd mengyu-notes

# 启动本地开发服务器
hugo server -D

# 浏览器访问 http://localhost:1313

创建新文章


bash
# 使用自定义模板创建新文章
hugo new posts/my-new-post.md



新文章会自动套用 archetypes/default.md 模板，包含预设的 front matter 结构。
构建生产版本


bash
hugo --minify



构建产物输出到 public/ 目录。
部署


本站部署在 Cloudflare Pages 上，每次推送到 main 分支会自动触发部署。
Cloudflare Pages 构建配置


配置项	值
框架预设	Hugo
构建命令	hugo --minify
输出目录	public
环境变量	HUGO_VERSION = 0.159.2
导航结构


菜单	路径	说明
首页	/	博客首页，含个人简介
归档	/archives/	按时间归档所有文章
标签	/tags/	文章标签云
分类	/categories/	文章分类列表
搜索	/search/	全文搜索
关于	/about/	关于我
文章分类


技术分享 — 技术学习笔记、项目实战经验、开源项目推荐
随笔 — 日常生活记录与感悟
版权说明


博客原创文章采用 CC BY-NC-SA 4.0 许可协议，转载请注明出处。
相关项目


online-student-exam-system — 在线考试系统（SpringBoot + Vue）
daily-hn-archives — Hacker News 每日热文自动归档
致谢


Hugo — 闪电般的静态站点生成器
PaperMod — 简洁优雅的 Hugo 主题
Cloudflare Pages — 快速可靠的静态网站托管
Giscus — 基于 GitHub Discussions 的评论系统
