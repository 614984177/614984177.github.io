---
title: hexo折腾记录
date: 2026-03-21 17:24:03
categories:
  - 计算机
  - 个人网站搭建
tags:
  - Hexo
  - 静态博客
---

# 目标和组件
核心目标：无服务器化，尽量弱运维！

# 静态博客站(Hexo)搭建记录
## 1. 主流静态博客生成器选择
| 生成器 | 核心语言 | GitHub Stars | 中文资料丰富度 | 优势 | 劣势 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| [**Hexo**](https://github.com/hexojs/hexo) | Node.js | ~38k | ⭐⭐⭐⭐⭐ | 生态极其成熟，Fluid 等优秀中文主题开箱即用。 | 文章过千后构建速度明显下降，可能出现改个错别字需要构建5分钟的情况（非用户访问时延）。 |
| [**Hugo**](https://github.com/gohugoio/hugo) | Go | ~74k | ⭐⭐⭐ | 毫秒级生成速度，单文件无依赖。 | Go 模板语法存在学习门槛。 |
| [**Jekyll**](https://github.com/jekyll/jekyll) | Ruby | ~48k | ⭐⭐⭐ | GitHub Pages 默认支持，插件规范。 | Ruby 环境配置对 Windows 不友好。 |
| [**Astro**](https://github.com/withastro/astro) | JS | ~45k | ⭐⭐⭐⭐ | 现代组件化架构，极致的加载性能。 | 仍处于快速迭代期，部分配置略复杂。 |

> 最终个人看中了 Hexo 的生态成熟度和丰富的中文主题资源，决定先行部署 Hexo 博客，后续如有性能瓶颈再考虑迁移至 Hugo。

## 2. 后期迁移路径预估
若未来需从 Hexo 迁移至 Hugo，通常涉及以下流程：
* **元数据适配**：Hexo 的 `tags` 和 `categories` 在 Hugo 中属于 `taxonomies`，需批量调整 Markdown 的 Front-matter 格式。
* **短代码重构**：Hexo 依赖插件实现的特殊语法（如 `{% asset_img %}`）需替换为 Hugo 的 `Shortcodes`。
* **资源重定向**：Hugo 推荐使用 `Page Bundles` 管理资源，需移动图片存放路径并配置 `aliases` 以维持原 SEO 链接不变。

# 主题选择：Fluid
在众多主题中选择 [Fluid](https://github.com/fluid-dev/hexo-theme-fluid)，主要基于其设计美学与功能集成度的平衡：
* **视觉交互**：遵循 Material Design 理念，具备优雅的毛玻璃动效与响应式布局。
* **内置功能**：自带搜索索引、LaTeX 公式解析以及字数统计，减少了第三方插件的引入，保证了生成站点的纯净度。


# 域名备案和公安备案
## 域名备案
1. 申请和购买zhangsongchao.cn
2. zhangsongchao.cn 是一个顶级域名， 三级域名如: blog.zhangsongchao.cn, www.zhangsongchao.cn, waline.zhangsongchao.cn等无需申请和额外备案，直接在DNS中添加CNAME记录即可。子域名是可以无限免费创建的。
3. 通过配置CNAME记录将blog.zhangsongchao.cn指向614984177.github.io
4. hexo的source目录下添加CNAME文件，内容为blog.zhangsongchao.cn
5. 2026/02/10 通过阿里云进行域名备案，备案号：***豫ICP备2026012479号-1***，备案主体为个人，备案状态为已审核

## 公安备案
完成域名备案后，一般会自动给你推送短信让你进行公安备案
在"全国互联网安全管理服务平台"进行网站公安备案时，被驳回了，原因是zhangsongchao.cn打不开。因为我只部署了blog.zhangsongchao.cn

### 思路
基于前文也提到了三级域名无需申请和额外备案，直接在DNS中添加CNAME记录即可，个人主页和博客内容分开部署后，感觉更专业一些，通过两个github项目来分别部署个人主页和博客内容  
1. 发现别人的博客都是放在二级域名下的，感觉更专业一些，个人主页和博客内容分开也更清晰  
2. 之前的博客是放在个人主页下的，感觉不太好看  

| github项目名称 | 域名 | 内容 | 备注 |
| :--- | :--- | :--- | :--- |
| home-page | zhangsongchao.cn | 个人主页 | 只放一个静态网页index.html |
| 614984177.github.io | blog.zhangsongchao.cn | 博客内容 | 通过hexo/hugo等搭建的个人的博客内容 |

### 个人主页(导航)搭建
详情见[个人主页（HomePage）选型与设计方案复盘](https://zhangsongchao.cn/2026/04/12/%E4%B8%AA%E4%BA%BA%E4%B8%BB%E9%A1%B5%28%E5%AF%BC%E8%88%AA%29%E6%90%AD%E5%BB%BA/)，总结来说就是选择了html5up.net上的Read Only这个主题，部署在home-page这个github项目上，配置域名为zhangsongchao.cn，最终实现了个人主页和博客内容分开部署的目标。

> PS: 这样会导致个人主页和博客的SEO权重不一致
## 最终备案后
当前所有的DNS记录如下：
- zhangsongchao.cn -> home-page 项目
- blog.zhangsongchao.cn -> 614984177.github.io 项目


# 图床
1. 借助pico插件
2. 云选择
   * 腾讯云OCS
   * 阿里云OSS
3. 搭建详情步骤见[腾讯云COS图床配置](https://zhangsongchao.cn/2026/03/21/%E5%BC%B1%E8%BF%90%E7%BB%B4%E5%BC%8F%E9%9D%99%E6%80%81%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%99%E6%90%AD%E5%BB%BA_%E5%80%9F%E5%8A%A9github/)，总结来说就是通过腾讯云COS来搭建图床，开启数据万象功能来实现图片的智能压缩和处理，最终在博客中引用加速后的图片地址。

# 评论系统
1.  LeanCloud：本来想选用的，但是看到即将停止对外服务的公告, 就放弃了
2. waline：这套方案实现了完全零成本、全 HTTPS 化的评论系统。Vercel (服务端) + Neon (PostgreSQL 数据库) 的组合不仅提供了极佳的性能和稳定性，还能通过环境变量轻松管理数据库连接字符串，确保数据安全和访问效率。对于追求极致性能的开发者，后续可考虑为域名添加国内 CDN 加速。
3. valine：感觉功能不够强大，且不太适合国内用户，暂时放弃。PS：可能跟本人喜欢大而全，还有点完美主义的倾向有关，感觉waline的功能和体验更符合我的需求。

## waline部署记录
[Waline教程官方链接](https://waline.js.org/guide/get-started/)，写的还可以，但是vercel和neno的UI变化比较快，可以结合AI指导着操作
   - **评论框架**: [Waline](https://waline.js.org/)
   - **后端托管**: [Vercel](https://vercel.com/) (免费、支持自动部署)
   - **数据库**: [Neon](https://neon.tech/) (Serverless PostgreSQL，完美替代 LeanCloud)

Tips:
1. 安全提醒 第一个注册的用户自动成为管理员。部署完成后应立即访问 /ui/register 完成注册，并随后通过环境变量禁用注册功能。
2. 在 Vercel 项目 Settings -> Domains 中添加自定义域名（如 waline.zhangsongchao.cn）。  

# CDN加速配置
1. 