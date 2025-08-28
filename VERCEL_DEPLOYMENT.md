# Vercel 部署指南

## 🚀 部署到 Vercel

Vercel 是 Next.js 应用的官方部署平台，提供全球 CDN、自动 SSL、即时部署等特性。

### 前置要求

- GitHub 账户
- Vercel 账户（可通过 GitHub 登录）
- 项目已推送到 GitHub 仓库

### 部署步骤

#### 方法一：通过 Vercel Dashboard（推荐）

1. **登录 Vercel**
   - 访问 [vercel.com](https://vercel.com)
   - 使用 GitHub 账户登录

2. **导入项目**
   - 点击 "New Project"
   - 选择你的 GitHub 仓库
   - 授权 Vercel 访问仓库

3. **配置项目**
   - 框架预设：Next.js
   - 根目录：`frontend`（重要！）
   - 构建命令：`npm run build`
   - 输出目录：`.next`（默认）

4. **环境变量配置**
   - 在项目设置 → Environment Variables 中添加：
     - `NEXT_PUBLIC_API_URL`: 你的后端 API 地址
     - `NEXT_PUBLIC_SITE_NAME`: 站点名称
     - `NEXT_PUBLIC_SITE_DESCRIPTION`: 站点描述

5. **部署**
   - 点击 "Deploy"
   - 等待构建完成

#### 方法二：通过 Vercel CLI

1. **安装 Vercel CLI**
   ```bash
   npm i -g vercel
   ```

2. **登录**
   ```bash
   vercel login
   ```

3. **部署**
   ```bash
   cd frontend
   vercel
   ```

### 环境变量配置

在 Vercel 控制台中设置以下环境变量：

| 变量名 | 描述 | 示例值 |
|--------|------|--------|
| `NEXT_PUBLIC_API_URL` | 后端 API 地址 | `https://api.yourdomain.com` |
| `NEXT_PUBLIC_SITE_NAME` | 站点名称 | `墨迹博客` |
| `NEXT_PUBLIC_SITE_DESCRIPTION` | 站点描述 | `现代个人博客平台` |

### 自定义域名

1. 在 Vercel 项目设置 → Domains 中添加自定义域名
2. 在域名注册商处配置 CNAME 记录指向 Vercel
3. Vercel 会自动配置 SSL 证书

### 部署类型

#### 1. 前端静态部署（推荐）
- 只部署前端 Next.js 应用
- 后端 API 需要单独部署（如 Railway、Heroku、自有服务器）
- 适合：前后端分离架构

#### 2. 全栈部署（需要调整）
- 需要修改项目结构
- 使用 Vercel Serverless Functions 或 Edge Functions
- 可能需要迁移后端代码

### 注意事项

1. **API 跨域问题**
   - 确保后端配置了正确的 CORS
   - 或者在 `next.config.js` 中配置 rewrites

2. **文件上传**
   - Vercel 是无服务器环境，不支持本地文件存储
   - 需要使用云存储（如 AWS S3、Cloudinary）

3. **数据库连接**
   - 使用云数据库服务（如 PlanetScale、Neon、Supabase）
   - 避免在 Serverless Functions 中使用长连接

4. **环境变量**
   - 生产环境变量必须在 Vercel 控制台中设置
   - 不要将敏感信息提交到代码仓库

### 性能优化

1. **图片优化**
   - 使用 Next.js 内置的 Image 组件
   - 配置 `next.config.js` 中的 images 域名

2. **CDN 缓存**
   - Vercel 自动提供全球 CDN
   - 配置合适的缓存策略

3. **Serverless Functions**
   - 保持函数轻量级
   - 优化冷启动时间

### 监控和分析

1. **Vercel Analytics**
   - 内置性能监控
   - 实时流量分析

2. **Web Vitals**
   - Next.js 内置 Core Web Vitals 监控

### 故障排除

#### 常见问题

1. **构建失败**
   - 检查 Node.js 版本兼容性
   - 查看构建日志中的具体错误

2. **环境变量未生效**
   - 确保在 Vercel 控制台中正确设置
   - 重启部署

3. **API 请求失败**
   - 检查 CORS 配置
   - 验证 API 地址是否正确

### 相关链接

- [Vercel Documentation](https://vercel.com/docs)
- [Next.js on Vercel](https://nextjs.org/docs/deployment)
- [Environment Variables](https://vercel.com/docs/projects/environment-variables)

---

⭐ 如果部署成功，记得给项目点个 star！