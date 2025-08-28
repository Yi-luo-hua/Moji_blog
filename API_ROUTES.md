# 墨迹博客 API 路由文档

## 基础信息

- **API 基础URL**: `http://localhost:8000/api`
- **认证方式**: Bearer Token (JWT)
- **内容类型**: `application/json`

## 认证路由 (`/api/auth`)

### 用户注册
- **POST** `/api/auth/register`
- **描述**: 创建新的管理员账户
- **请求体**:
```json
{
  "username": "admin",
  "email": "admin@example.com", 
  "password": "password123",
  "displayName": "管理员",
  "bio": "博客管理员"
}
```

### 用户登录
- **POST** `/api/auth/login`
- **描述**: 管理员登录
- **请求体**:
```json
{
  "username": "admin",
  "password": "password123"
}
```

### 获取当前用户信息
- **GET** `/api/auth/me`
- **描述**: 获取当前登录用户的信息
- **认证**: 需要

### 更新用户资料
- **PUT** `/api/auth/profile`
- **描述**: 更新用户个人信息
- **认证**: 需要
- **请求体**:
```json
{
  "displayName": "新昵称",
  "bio": "新简介",
  "email": "new@example.com"
}
```

### 修改密码
- **PUT** `/api/auth/password`
- **描述**: 修改用户密码
- **认证**: 需要
- **请求体**:
```json
{
  "currentPassword": "oldpassword",
  "newPassword": "newpassword"
}
```

## 文章路由 (`/api/posts`)

### 获取文章列表
- **GET** `/api/posts`
- **描述**: 获取文章列表，支持分页和筛选
- **查询参数**:
  - `page`: 页码 (默认: 1)
  - `limit`: 每页数量 (默认: 10)
  - `status`: 文章状态 (`published`, `draft`, `archived`, `all`)
  - `category`: 分类 slug
  - `tag`: 标签 slug
  - `search`: 搜索关键词
  - `featured`: 是否精选 (`true`, `false`)
  - `sortBy`: 排序字段 (`created_at`, `published_at`, `title`, `views_count`)
  - `sortOrder`: 排序方向 (`ASC`, `DESC`)

### 获取单篇文章
- **GET** `/api/posts/:slug`
- **描述**: 根据 slug 获取文章详情
- **查询参数**:
  - `increment_views`: 是否增加浏览量 (默认: true)

### 创建文章
- **POST** `/api/posts`
- **描述**: 创建新文章
- **认证**: 需要
- **请求体**:
```json
{
  "title": "文章标题",
  "content": "文章内容 (Markdown)",
  "excerpt": "文章摘要",
  "categoryId": "分类ID",
  "tags": ["标签ID1", "标签ID2"],
  "status": "draft",
  "featured": false,
  "coverImage": "封面图片URL"
}
```

### 更新文章
- **PUT** `/api/posts/:id`
- **描述**: 更新指定文章
- **认证**: 需要
- **请求体**: 同创建文章 (所有字段均可选)

### 删除文章
- **DELETE** `/api/posts/:id`
- **描述**: 删除指定文章
- **认证**: 需要

## 分类路由 (`/api/categories`)

### 获取分类列表
- **GET** `/api/categories`
- **描述**: 获取所有分类
- **查询参数**:
  - `include_stats`: 是否包含统计信息 (默认: false)

### 获取单个分类
- **GET** `/api/categories/:slug`
- **描述**: 根据 slug 获取分类详情

### 创建分类
- **POST** `/api/categories`
- **描述**: 创建新分类
- **认证**: 需要
- **请求体**:
```json
{
  "name": "分类名称",
  "description": "分类描述",
  "color": "#007BFF"
}
```

### 更新分类
- **PUT** `/api/categories/:id`
- **描述**: 更新指定分类
- **认证**: 需要
- **请求体**: 同创建分类 (所有字段均可选)

### 删除分类
- **DELETE** `/api/categories/:id`
- **描述**: 删除指定分类
- **认证**: 需要

## 标签路由 (`/api/tags`)

### 获取标签列表
- **GET** `/api/tags`
- **描述**: 获取所有标签
- **查询参数**:
  - `include_stats`: 是否包含统计信息 (默认: false)
  - `limit`: 限制数量

### 搜索标签
- **GET** `/api/tags/search`
- **描述**: 搜索标签
- **查询参数**:
  - `q`: 搜索关键词
  - `limit`: 结果数量限制 (默认: 10)

### 获取单个标签
- **GET** `/api/tags/:slug`
- **描述**: 根据 slug 获取标签详情

### 创建标签
- **POST** `/api/tags`
- **描述**: 创建新标签
- **认证**: 需要
- **请求体**:
```json
{
  "name": "标签名称"
}
```

### 批量创建标签
- **POST** `/api/tags/batch`
- **描述**: 批量创建标签
- **认证**: 需要
- **请求体**:
```json
{
  "names": ["标签1", "标签2", "标签3"]
}
```

### 更新标签
- **PUT** `/api/tags/:id`
- **描述**: 更新指定标签
- **认证**: 需要
- **请求体**:
```json
{
  "name": "新标签名称"
}
```

### 删除标签
- **DELETE** `/api/tags/:id`
- **描述**: 删除指定标签
- **认证**: 需要

## 评论路由 (`/api/comments`)

### 获取文章评论
- **GET** `/api/comments/posts/:postId`
- **描述**: 获取指定文章的评论
- **查询参数**:
  - `status`: 评论状态 (`approved`, `pending`, `rejected`, `spam`, `all`)
  - `include_replies`: 是否包含回复 (默认: true)

### 创建评论
- **POST** `/api/comments/posts/:postId`
- **描述**: 为指定文章创建评论
- **请求体**:
```json
{
  "content": "评论内容",
  "authorName": "评论者姓名",
  "authorEmail": "评论者邮箱",
  "authorWebsite": "评论者网站 (可选)",
  "parentId": "父评论ID (回复时需要)"
}
```

### 获取所有评论 (管理员)
- **GET** `/api/comments`
- **描述**: 获取所有评论列表
- **认证**: 需要
- **查询参数**:
  - `page`: 页码
  - `limit`: 每页数量
  - `status`: 评论状态
  - `sort_by`: 排序字段
  - `sort_order`: 排序方向

### 更新评论状态 (管理员)
- **PUT** `/api/comments/:id/status`
- **描述**: 更新评论状态
- **认证**: 需要
- **请求体**:
```json
{
  "status": "approved"
}
```

### 删除评论 (管理员)
- **DELETE** `/api/comments/:id`
- **描述**: 删除指定评论
- **认证**: 需要

## 文件上传路由 (`/api/upload`)

### 上传单个图片
- **POST** `/api/upload/image`
- **描述**: 上传单个图片文件
- **认证**: 需要
- **请求类型**: `multipart/form-data`
- **字段**: `image` (文件)

### 上传多个图片
- **POST** `/api/upload/images`
- **描述**: 上传多个图片文件
- **认证**: 需要
- **请求类型**: `multipart/form-data`
- **字段**: `images` (文件数组)

## 响应格式

### 成功响应
```json
{
  "success": true,
  "message": "操作成功",
  "data": {
    // 具体数据
  }
}
```

### 错误响应
```json
{
  "success": false,
  "message": "错误信息",
  "errors": [
    {
      "field": "字段名",
      "message": "错误描述",
      "value": "错误值"
    }
  ]
}
```

### 分页响应
```json
{
  "success": true,
  "data": {
    "items": [],
    "pagination": {
      "page": 1,
      "limit": 10,
      "total": 100,
      "totalPages": 10
    }
  }
}
```

## 状态码说明

- `200`: 成功
- `201`: 创建成功
- `400`: 请求错误
- `401`: 未认证
- `403`: 无权限
- `404`: 资源不存在
- `409`: 冲突 (如重复数据)
- `422`: 验证失败
- `429`: 请求过于频繁
- `500`: 服务器错误

## 认证说明

需要认证的接口需要在请求头中包含：
```
Authorization: Bearer <JWT_TOKEN>
```

JWT Token 通过登录接口获取，有效期为 7 天。
