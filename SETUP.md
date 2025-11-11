# 部署说明

## 快速部署

### 1. 组织设置

进入组织 Settings：

- **Member privileges** > Base permissions: `Read`
- **Repository defaults**: 仅管理员可创建仓库

### 2. 仓库设置

进入 `start` 仓库 Settings：

- **General** > Features: 启用 `Issues`
- **Actions** > General > Workflow permissions: `Read and write permissions`

### 3. 测试运行

手动触发 workflow 测试：

```
Actions > Daily Study Stats > Run workflow
```

检查 `records/` 目录是否生成统计数据。

---

## 启用完全自动化（可选）

### 创建 Personal Access Token

```
Settings > Developer settings > Personal access tokens > Tokens (classic)

勾选权限：
- repo (Full control)
- admin:org (Full control)

生成后复制 token
```

### 配置 Secret

```
仓库 Settings > Secrets and variables > Actions > Secrets

Name: ORG_ADMIN_TOKEN
Secret: [粘贴 token]
```

### 启用自动化

```
仓库 Settings > Secrets and variables > Actions > Variables

变量 1:
Name: AUTO_INVITE_ENABLED
Value: true

变量 2:
Name: AUTO_CREATE_REPO_ENABLED
Value: true
```

### 测试自动化

1. 创建测试 Issue（使用模板）
2. 添加 `approved` 标签
3. 查看 Actions 运行结果

---

## 日常使用

### 管理员审批

在 Issue 上：
- 添加 `approved` 标签，或
- 评论 `/approve`

系统自动处理（基础模式提供指引，完全自动化模式直接执行）

### 查看统计

浏览 `records/YYYY-MM-DD/` 查看每日打卡数据。

---

## 故障排查

**Workflow 失败**: 查看 Actions 日志
**统计数据缺失**: 检查仓库命名是否为 `not-study-*`
**Token 权限不足**: 重新生成 token 并确认权限

---

详细文档: [.github/README.md](./.github/README.md)
