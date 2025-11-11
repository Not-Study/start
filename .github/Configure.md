# GitHub 配置说明

本目录包含组织的自动化配置文件。

## 目录结构

```
.github/
├── ISSUE_TEMPLATE/          # Issue 模板
│   ├── join-organization.md
│   └── request-repository.md
└── workflows/               # GitHub Actions
    ├── daily-stats.yml
    ├── auto-approve-join.yml
    └── auto-approve-repo.yml
```

## Issue 模板

### 申请加入组织

用户填写 GitHub 用户名和申请理由，管理员审核后邀请加入。

### 申请个人仓库

成员申请创建 `not-study-用户名` 格式的学习仓库。

## GitHub Actions

### 每日统计 (daily-stats.yml)

- **运行时间**: 每天北京时间 00:00
- **功能**: 统计所有 `not-study-*` 仓库的 commit
- **输出**: `records/YYYY-MM-DD/`

### 自动审批 (auto-approve-\*.yml)

管理员在 Issue 添加 `approved` 标签或评论 `/approve` 触发。

**基础模式** (默认)：提供操作指引
**完全自动化** (可选)：自动邀请用户/创建仓库

## 启用完全自动化

需要配置 Personal Access Token：

1. 创建 PAT (需要 `admin:org` 和 `repo` 权限)
2. 在仓库 Settings > Secrets 添加 `ORG_ADMIN_TOKEN`
3. 在 Variables 启用：
   - `AUTO_INVITE_ENABLED=true`
   - `AUTO_CREATE_REPO_ENABLED=true`

### 创建 PAT 步骤

```
Settings > Developer settings > Personal access tokens > Tokens (classic)
勾选权限：
- repo (Full control)
- admin:org (Full control)
```

## 权限配置

### 组织设置

- 默认成员权限：Read
- 仓库创建权限：仅管理员

### 仓库权限

- 仓库所有者：Write
- 其他成员：Read (继承组织默认)

## 故障排查

### Workflow 失败

1. 检查 Actions 日志
2. 确认 Token 权限
3. 验证仓库命名格式

### 统计数据缺失

- 检查仓库命名是否为 `not-study-*`
- 确认提交时间在北京时间当天
- 查看 API 调用是否成功

---

详细文档: [GitHub Actions](https://docs.github.com/actions) | [API 文档](https://docs.github.com/rest)
