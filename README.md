# 个人工作台 · 单文件版

一个零依赖、零构建的单文件 HTML 个人精进工作台。打开即用，数据本地存储，可选 Supabase 云端多端同步。

> 访问作者实例：[gengmingjie666-ctrl.github.io/geng-workbench](https://gengmingjie666-ctrl.github.io/geng-workbench/)

## ✨ 功能特性

| 模块 | 说明 |
|------|------|
| 🏠 总览 | 当日任务、打卡、热点聚合一览 |
| 📋 今日日课 | 待办任务管理，支持标签、媒体（图片/视频） |
| 🌿 修身打卡 | 早起、金刚功、长寿功、观照、读书、早睡等习惯打卡 |
| 📖 学术研究 | 阅读笔记与文献管理 |
| 🔥 个人公众号 | 文章选题与话题管理 |
| 💼 工作公众号 | 工作号文章与话题管理 |
| 🎯 观念工夫 | 自我观念、案例分析、贪嗔痴慢疑种子觉察 |
| ✒️ 小说创作 | 素材、人物、大纲、草稿、灵感，分阶段管理 |
| 📝 读书札记 | 读书笔记，按分类归档 |
| ⭐ 灵感速记 | 快速捕捉灵感 |
| 📕 英语学习 | 英语学习记录 |
| 💪 运动锻炼 | 运动记录 |
| 💰 财经资讯 | 财经信息聚合 |
| 🤖 AI资讯 | AI 行业动态 |
| 🔥 每日热点 | 微博/知乎/B站/抖音热搜，由 GitHub Actions 每小时更新 |
| ⚙️ 设置 | Supabase 同步、AI 服务配置、数据导入导出 |

## 🚀 快速开始

### 方式一：直接使用

1. 下载 [`index.html`](./index.html)（或 [`template.html`](./template.html) 模板）
2. 双击用浏览器打开即可使用
3. 所有数据保存在浏览器本地（IndexedDB）

### 方式二：部署到 GitHub Pages

1. Fork 本仓库
2. 在仓库设置中开启 GitHub Pages（Source: `main` 分支，根目录）
3. 访问 `https://<你的用户名>.github.io/<仓库名>/`

## ⚙️ 自定义配置

### 1. 修改个人信息

打开 HTML 文件，搜索 `你的名字`（模板版）或直接替换为你的名字：

- `<title>你的名字 · 个人工作台</title>` — 浏览器标签页标题
- `<h1>你的名字工作台</h1>` — 侧边栏/顶栏标题
- `<div class="seal">你</div>` — 印章字（建议用你的姓）
- `const n='你的名字';` — 问候语中的名字
- 导出备份文件名中的 `你的名字工作台备份`

> 💡 作者版 `index.html` 已填入作者名字，**请使用 `template.html` 或自行替换**。

### 2. 配置云端同步（可选，多端同步必需）

工作台支持 Supabase 实现手机/电脑多端同步：

1. 注册 [Supabase](https://supabase.com) 并创建项目
2. 在 SQL Editor 中执行以下建表语句：

```sql
create table if not exists public.workbench (
  id text primary key,
  data jsonb not null default '{}'::jsonb,
  updated_at timestamptz not null default now()
);

alter table public.workbench enable row level security;

drop policy if exists "workbench anon all" on public.workbench;
create policy "workbench anon all"
  on public.workbench for all
  using (true) with check (true);
```

3. 打开工作台 → 设置 → 填入 Supabase `Project URL` 和 `anon key`
4. 所有设备填入相同配置即可自动同步

### 3. 配置 AI 助手（可选）

工作台内置 AI 助手，支持智谱 AI 和 DeepSeek：

1. 打开工作台 → 设置
2. 选择服务提供商（智谱 / DeepSeek）
3. 填入 API Key

## 💾 数据存储

| 存储方式 | 内容 | 说明 |
|----------|------|------|
| IndexedDB | 全部数据 | 浏览器本地，离线可用 |
| Supabase | 全部数据（同步副本） | 多端同步，需手动配置 |
| IndexedDB（视频） | 视频文件 | 视频较大，仅存本地不上云 |
| Base64 in State | 图片 | 图片压缩后参与云同步 |

数据导入导出：侧边栏底部「导出备份 / 导入数据」。

## 🔥 每日热点

仓库内置 GitHub Actions 工作流（`.github/workflows/fetch-hot.yml`），每小时自动抓取微博、知乎、B站、抖音热搜并更新 `hot-data.json`。

Fork 后自动生效，无需额外配置。

## 📄 许可证

[MIT License](./LICENSE) © 2026 耿茗傑
