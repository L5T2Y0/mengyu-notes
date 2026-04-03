---
title: "开源项目分享：Daily HN Archives - 自动归档 Hacker News 热门文章"
date: 2026-04-03T18:00:00+08:00
draft: false
tags:
  - 开源项目
  - Python
  - GitHub Actions
  - 自动化
categories:
  - 技术分享
comments: true
---

## 项目简介

最近开源了一个自动化项目 [Daily HN Archives](https://github.com/L5T2Y0/daily-hn-archives)，它能每天自动获取 Hacker News 的热门文章并归档保存。

这个项目基于 GitHub Actions 实现全自动运行，无需服务器，完全免费。每天 UTC 0点自动执行，获取当天的 Top 10 热门文章，并以 Markdown 格式保存到仓库中。

## 核心功能

- **每日归档** - 自动获取并保存 Hacker News Top 10 文章
- **周报汇总** - 每周日生成 Top 20 热门文章周报
- **月报精选** - 每月1号生成 Top 50 热门文章月报
- **智能分类** - 自动识别文章类别（AI、Web、DevOps 等 12+ 标签）
- **动态索引** - README 自动更新，历史记录一目了然

## 技术亮点

### 1. 全自动化流程

使用 GitHub Actions 实现完全自动化：

```yaml
每天 UTC 0点 → 获取 HN Top 10 → 生成归档文件 → 更新 README → 自动提交
```

无需人工干预，失败自动重试，确保数据不丢失。

### 2. 企业级代码质量

- **自定义异常处理** - 完善的错误恢复机制
- **指数退避重试** - 网络请求失败自动重试（最多3次）
- **完整测试覆盖** - 22个单元测试用例全部通过
- **代码规范** - 使用 black、flake8、mypy 保证代码质量

### 3. 模块化设计

项目采用清晰的模块化架构：

- `hn_fetcher.py` - 与 Hacker News API 交互
- `markdown_generator.py` - 生成 Markdown 内容
- `file_manager.py` - 文件系统操作
- `weekly_summary.py` - 生成周报
- `monthly_summary.py` - 生成月报
- `tag_classifier.py` - 文章智能分类

## 使用方法

### 方式一：Fork 自动运行（推荐）

1. Fork 本仓库
2. 启用 GitHub Actions
3. 等待每天自动运行

就这么简单！

### 方式二：本地运行

```bash
# 克隆仓库
git clone https://github.com/L5T2Y0/daily-hn-archives.git
cd daily-hn-archives

# 安装依赖
pip install -r requirements.txt

# 运行脚本
python main.py
```

## 技术栈

- **Python 3.12** - 核心开发语言
- **requests** - HTTP 请求库
- **GitHub Actions** - CI/CD 自动化
- **Hacker News API** - 数据来源

开发工具：
- pytest - 单元测试
- black - 代码格式化
- flake8 - 静态检查
- mypy - 类型检查

## 项目收获

通过这个项目，我学到了：

1. **GitHub Actions 实战** - 从零搭建完整的 CI/CD 流程
2. **Python 最佳实践** - 异常处理、类型注解、模块化设计
3. **API 交互技巧** - 重试机制、超时处理、错误恢复
4. **开源项目管理** - README 编写、文档维护、版本控制

## 未来计划

- [ ] 添加更多数据源（Reddit、Product Hunt 等）
- [ ] 支持自定义归档规则
- [ ] 生成数据可视化图表
- [ ] 提供 RSS 订阅功能

## 开源地址

项目地址：[https://github.com/L5T2Y0/daily-hn-archives](https://github.com/L5T2Y0/daily-hn-archives)

如果觉得有用，欢迎 Star ⭐ 支持一下！

## 总结

这是一个简单但实用的自动化项目，适合：

- 想了解 GitHub Actions 的开发者
- 需要追踪科技趋势的技术爱好者
- 学习 Python 爬虫和 API 调用的初学者

代码完全开源，欢迎 Fork 和贡献！
