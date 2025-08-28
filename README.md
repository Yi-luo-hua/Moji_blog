# 墨迹 - 个人博客平台

现代、简洁、注重内容展示的个人博客网站，提供卓越的阅读和写作体验。

## ✨ 功能特性

### 🔐 用户认证与管理
- 安全的管理员认证系统 (JWT)
- 用户信息管理和密码修改
- 基于角色的权限控制

### 📝 内容管理系统
- 强大的文章管理系统 (创建、编辑、删除、发布)
- Markdown 编辑器支持
- 文章状态管理 (草稿、已发布、归档)
- 文章封面图片上传
- 文章摘要和SEO优化

### 🏷️ 内容组织
- 分类系统 (支持颜色标记)
- 标签系统 (支持批量创建)
- 精选文章功能
- 文章浏览量统计

### 💬 互动功能
- 评论系统 (支持回复)
- 评论审核机制
- 访客信息收集 (昵称、邮箱、网站)

### 🔍 搜索与导航
- 全站搜索功能
- 分类筛选和标签筛选
- 文章归档页面
- 相关文章推荐

### 🎨 用户界面
- 响应式设计 (完美适配桌面、平板、手机)
- 现代化的UI设计
- 优雅的动画效果
- 暗色模式支持准备

### ⚡ 性能与SEO
- 服务端渲染 (SSR)
- 静态站点生成 (SSG) 支持
- 图片优化和懒加载
- SEO友好的URL结构
- Open Graph和Twitter Card支持

## 🛠️ 技术栈

### 前端技术
- **框架**: Next.js 14 (React 18)
- **样式**: Tailwind CSS + Headless UI
- **动画**: Framer Motion
- **图标**: Heroicons
- **编辑器**: React Markdown + Rehype/Remark
- **表单**: React Hook Form + Zod
- **状态管理**: SWR
- **HTTP客户端**: Axios

### 后端技术
- **运行时**: Node.js
- **框架**: Express.js
- **数据库**: PostgreSQL
- **认证**: JWT + bcrypt
- **文件上传**: Multer
- **验证**: Express Validator
- **限流**: Express Rate Limit
- **日志**: Morgan

### 开发工具
- **语言**: TypeScript
- **代码检查**: ESLint
- **包管理**: NPM
- **构建工具**: Next.js CLI
- **容器化**: Docker + Docker Compose

## 🚀 快速开始

### 使用 Docker (推荐)

```bash
# 克隆项目
git clone <repository-url>
cd mojie-blog

# 使用 Docker Compose 启动
npm run docker:up
```

### 本地开发

```bash
# 安装根目录依赖
npm install

# 安装前端依赖
cd frontend && npm install

# 安装后端依赖
cd ../backend && npm install

# 设置环境变量
cp backend/env.example backend/.env
# 编辑 backend/.env 文件，配置数据库连接

# 启动开发服务器 (在项目根目录)
cd .. && npm run dev
```

### 首次运行设置

1. **数据库初始化**:
   - 确保 PostgreSQL 服务运行
   - 执行 `database/init.sql` 初始化数据库结构和示例数据

2. **默认管理员账户**:
   - 用户名: `admin`
   - 密码: `admin123`
   - 邮箱: `admin@mojie.blog`

3. **访问地址**:
   - 前端: http://localhost:3000
   - 后端 API: http://localhost:8000
   - API 文档: http://localhost:8000/api

## 📁 项目结构

```
mojie-blog/
├── 📁 frontend/                    # Next.js 前端应用
│   ├── 📁 public/                  # 静态资源
│   ├── 📁 src/
│   │   ├── 📁 components/          # React 组件
│   │   ├── 📁 pages/               # Next.js 页面
│   │   ├── 📁 hooks/               # 自定义 Hooks
│   │   ├── 📁 utils/               # 工具函数
│   │   └── 📁 styles/              # 样式文件
│   ├── 📄 next.config.js           # Next.js 配置
│   ├── 📄 tailwind.config.js       # Tailwind 配置
│   └── 📄 package.json
├── 📁 backend/                     # Express.js 后端 API
│   ├── 📁 src/
│   │   ├── 📁 config/              # 配置文件
│   │   ├── 📁 controllers/         # 控制器
│   │   ├── 📁 middleware/          # 中间件
│   │   ├── 📁 routes/              # 路由定义
│   │   ├── 📁 utils/               # 工具函数
│   │   └── 📄 index.js             # 应用入口
│   ├── 📁 uploads/                 # 文件上传目录
│   └── 📄 package.json
├── 📁 database/                    # 数据库相关
│   └── 📄 init.sql                 # 数据库初始化脚本
├── 📄 docker-compose.yml           # Docker 编排配置
├── 📄 API_ROUTES.md                # API 接口文档
├── 📄 package.json                 # 根项目配置
└── 📄 README.md                    # 项目说明
```

## 🚢 部署

### Vercel 部署 (推荐，仅前端)

Vercel 是 Next.js 官方推荐的部署平台，提供全球 CDN、自动 SSL 和即时部署。

1. **部署步骤**:
   - Fork 项目到你的 GitHub 账户
   - 访问 [vercel.com](https://vercel.com) 并登录
   - 导入项目，选择 GitHub 仓库
   - 设置根目录为 `frontend`
   - 配置环境变量（参考 `frontend/.env.example`）
   - 点击部署

2. **环境变量**:
   ```env
   NEXT_PUBLIC_API_URL=你的后端API地址
   NEXT_PUBLIC_SITE_NAME=墨迹博客
   NEXT_PUBLIC_SITE_DESCRIPTION=现代个人博客平台
   ```

详细部署指南请参考 [VERCEL_DEPLOYMENT.md](./VERCEL_DEPLOYMENT.md)

### Docker 部署 (全栈)

```bash
# 构建镜像
npm run docker:build

# 启动所有服务
npm run docker:up

# 停止服务
npm run docker:down
```

### 手动部署

1. **准备环境**:
   ```bash
   # 确保系统已安装
   - Node.js 18+
   - PostgreSQL 13+
   - Git
   ```

2. **数据库设置**:
   ```bash
   # 创建数据库
   createdb mojie_blog
   
   # 执行初始化脚本
   psql -d mojie_blog -f database/init.sql
   ```

3. **配置环境变量**:
   ```bash
   # 复制并编辑环境变量文件
   cp backend/env.example backend/.env
   ```

4. **构建和启动**:
   ```bash
   # 安装依赖
   npm install
   cd frontend && npm install
   cd ../backend && npm install
   
   # 构建前端
   cd ../frontend && npm run build
   
   # 启动服务
   cd .. && npm start
   ```

## ⚙️ 环境变量配置

在 `backend/.env` 文件中配置以下变量：

```env
# 服务器配置
PORT=8000
NODE_ENV=production

# JWT 密钥 (生产环境请使用复杂密钥)
JWT_SECRET=your-super-secret-jwt-key-change-in-production
JWT_EXPIRES_IN=7d

# 数据库配置
DB_HOST=localhost
DB_PORT=5432
DB_NAME=mojie_blog
DB_USER=your-db-user
DB_PASSWORD=your-db-password

# 文件上传配置
UPLOAD_MAX_SIZE=5242880
UPLOAD_PATH=./uploads

# CORS 配置
CORS_ORIGIN=http://localhost:3000

# 限流配置
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=100
```

## 📝 使用指南

### 管理后台功能

1. **文章管理**:
   - 支持 Markdown 编写
   - 实时预览功能
   - 封面图片上传
   - 分类和标签管理
   - 文章状态控制

2. **内容组织**:
   - 创建和编辑分类
   - 批量管理标签
   - 设置精选文章

3. **评论审核**:
   - 查看所有评论
   - 批准/拒绝评论
   - 删除垃圾评论

### API 使用

详细的 API 文档请参考 [API_ROUTES.md](./API_ROUTES.md)

## 🔧 自定义配置

### 主题定制

1. **颜色方案**: 编辑 `frontend/tailwind.config.js`
2. **字体设置**: 修改 `frontend/src/styles/globals.css`
3. **布局调整**: 更新 `frontend/src/components/Layout.tsx`

### 功能扩展

1. **添加新页面**: 在 `frontend/src/pages/` 目录下创建新文件
2. **扩展 API**: 在 `backend/src/routes/` 和 `backend/src/controllers/` 中添加新功能
3. **数据库修改**: 更新 `database/init.sql` 并进行数据迁移

## 🎯 路线图

- [ ] 管理员后台界面
- [ ] 文章编辑器增强
- [ ] 多语言支持
- [ ] 暗色模式
- [ ] PWA 支持
- [ ] 邮件通知系统
- [ ] 统计分析功能
- [ ] 备份和恢复功能

## 🐛 问题排查

### 常见问题

1. **数据库连接失败**:
   - 检查 PostgreSQL 服务是否运行
   - 确认数据库连接参数正确
   - 验证用户权限设置

2. **文件上传失败**:
   - 检查 `backend/uploads/` 目录权限
   - 确认文件大小不超过限制
   - 验证文件类型是否支持

3. **前端页面无法访问**:
   - 确认后端 API 服务正常运行
   - 检查 CORS 配置
   - 验证环境变量设置

### 日志查看

```bash
# Docker 环境查看日志
docker-compose logs -f

# 查看特定服务日志
docker-compose logs -f backend
docker-compose logs -f frontend
```

## 🤝 贡献指南

我们欢迎所有形式的贡献！

### 提交 Issue

- 使用清晰的标题描述问题
- 提供详细的复现步骤
- 包含相关的错误信息和截图

### 提交 Pull Request

1. Fork 项目到您的 GitHub 账户
2. 创建新的功能分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

### 开发规范

- 遵循 ESLint 规则
- 编写清晰的提交信息
- 为新功能添加适当的测试
- 更新相关文档

## 📄 许可证

本项目基于 [MIT 许可证](LICENSE) 开源。

## 🙏 致谢

感谢以下开源项目的支持：

- [Next.js](https://nextjs.org/) - React 框架
- [Express.js](https://expressjs.com/) - Node.js Web 框架
- [PostgreSQL](https://www.postgresql.org/) - 数据库
- [Tailwind CSS](https://tailwindcss.com/) - CSS 框架
- [Framer Motion](https://www.framer.com/motion/) - 动画库

## 📞 联系方式

如有问题或建议，请通过以下方式联系：

- 📧 Email: akesakiko@gmail.com
- 🐛 Issues: [GitHub Issues](https://github.com/Yi-luo-hua/Moji_blog/issues)
- 💬 Discussions: [GitHub Discussions](https://github.com/Yi-luo-hua/Moji_blog/discussions)

---

⭐ 如果这个项目对您有帮助，请给个 star 支持一下！

