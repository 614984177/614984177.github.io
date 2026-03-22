---
title: hexo折腾记录
date: 2026-03-21 17:24:03
tags:
---

# 图床
1. 借助pico插件
2. 云选择
  * 腾讯云OCS：开启数据万象
    * "?imageSlim"参数为极智压缩，它利用 AI 视觉模型对图片进行内容识别，在不改变格式（保留你的 JPG/PNG）的情况下，最大限度减小体积。
    * "imageMogr2"参数为图像处理
    * "/interlace/1"为渐进式显示
    * "quality/80"压缩这是一个兜底参数。虽然 Slim 会智能处理，但强制设定为 80% 质量能确保图片在体积和画质之间有一个稳定的平衡点。
    * "/thumbnail/800x"为缩略图参数，指定宽度为800px，高度自适应
  * 阿里云OSS
3.  



## 成果展示
![这是我的头像测试图](https://image-1300512664.cos.ap-shanghai.myqcloud.com/blog-img/1581928963662.jpg?imageMogr2/format/webp)

![风景大图测试](https://image-1300512664.cos.ap-shanghai.myqcloud.com/blog-img/Shanghai_Huawei_Lianqiuhu_20250902.jpg?imageSlim&imageMogr2/interlace/1/quality/80)

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

