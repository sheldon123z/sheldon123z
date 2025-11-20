# GitHub Profile 统计配置指南

这份指南将帮助你配置 GitHub Profile，使其能够正确显示包括私有仓库在内的所有贡献统计。

## 为什么统计信息不准确?

默认情况下，第三方统计服务只能访问你的公开仓库数据。如果你的大部分贡献在私有仓库中，统计信息就会显得不完整。

## 解决方案

### 1. 创建 GitHub Personal Access Token (PAT)

要让统计服务访问你的私有仓库，需要创建一个具有适当权限的 token。

#### 步骤：

1. 访问 GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
2. 点击 "Generate new token" → "Generate new token (classic)"
3. 给 token 起个名字，比如 `GitHub Stats Token`
4. 设置过期时间（建议选择 "No expiration" 或较长时间）
5. 选择以下权限范围 (scopes)：
   - ✅ `repo` (完整的仓库访问权限)
   - ✅ `read:user` (读取用户信息)
   - ✅ `user:email` (读取用户邮箱)
6. 点击 "Generate token"
7. **重要**: 立即复制生成的 token，它只会显示一次！

### 2. 将 Token 添加到仓库 Secrets

1. 进入你的 profile 仓库 (`sheldon123z/sheldon123z`)
2. 点击 Settings → Secrets and variables → Actions
3. 点击 "New repository secret"
4. 创建以下 secret：
   - **Name**: `STATS_TOKEN`
   - **Value**: 粘贴刚才创建的 Personal Access Token
5. 点击 "Add secret"

### 3. 启用 GitHub Actions

1. 进入仓库的 Actions 标签页
2. 如果 Actions 被禁用，点击 "Enable Actions"
3. 推送代码后，GitHub Actions 将自动运行

### 4. 设置工作流权限

1. 进入 Settings → Actions → General
2. 滚动到 "Workflow permissions"
3. 选择 "Read and write permissions"
4. 勾选 "Allow GitHub Actions to create and approve pull requests"
5. 点击 "Save"

## 已配置的自动化功能

配置完成后，以下功能将自动运行：

### 🐍 贡献蛇图动画
- **运行频率**: 每天自动更新 + 每次推送
- **功能**: 生成展示你贡献历史的动画蛇图
- **文件**: `.github/workflows/snake.yml`

### 📊 GitHub 统计数据
- **运行频率**: 每天一次
- **功能**: 生成包含私有仓库的详细统计信息
- **文件**: `.github/workflows/github-stats.yml`
- **需要**: `STATS_TOKEN` secret

### ⚡ 最近活动更新
- **运行频率**: 每 6 小时
- **功能**: 自动更新 README 中的最近活动列表
- **文件**: `.github/workflows/update-activity.yml`

## 验证配置

1. 推送代码到仓库
2. 访问 Actions 标签页查看工作流运行状态
3. 等待几分钟让工作流完成
4. 刷新你的 profile 页面查看更新后的统计

## 常见问题

### Q: 为什么 Actions 运行失败？
A: 检查以下几点：
- 确保 `STATS_TOKEN` secret 已正确添加
- 确保 token 具有 `repo` 权限
- 确保工作流权限设置为 "Read and write permissions"

### Q: 统计数据多久更新一次？
A:
- 贡献蛇图: 每天自动更新
- GitHub 统计: 每天更新一次
- 最近活动: 每 6 小时更新一次
- 你也可以在 Actions 标签页手动触发更新

### Q: 某些服务显示不出来？
A: 有些第三方服务可能会临时不可用或有访问限制。主要的统计服务（github-readme-stats, streak-stats）都是可靠的。

### Q: 如何手动触发更新？
A:
1. 进入 Actions 标签页
2. 选择要运行的工作流
3. 点击 "Run workflow"
4. 点击绿色的 "Run workflow" 按钮

## 增强统计显示

如果你想要更详细的统计，可以考虑：

1. **部署自己的 github-readme-stats 实例**
   - Fork [github-readme-stats](https://github.com/anuraghazra/github-readme-stats)
   - 部署到 Vercel
   - 使用你自己的 PAT 配置

2. **配置 WakaTime**
   - 安装 WakaTime 插件到你的 IDE
   - 创建 WakaTime account
   - 在 README 中取消注释 WakaTime 部分

3. **自定义主题和样式**
   - 修改 README.md 中的颜色参数
   - 调整显示的语言数量
   - 选择不同的图表布局

## 技术支持

如果遇到问题：
1. 检查 Actions 运行日志
2. 确认所有 secrets 都已正确配置
3. 查看各个服务的文档链接（在 workflow 文件中）

---

配置完成后，你的 GitHub Profile 将展示完整的贡献统计，包括私有仓库的数据！🎉
