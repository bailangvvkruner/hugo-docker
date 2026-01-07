# 阿里云容器镜像仓库配置说明

本文档说明如何配置GitHub Actions以同时推送到DockerHub和阿里云容器镜像仓库。

## 已完成的配置

在 `.github/workflows/build.yml` 中已经添加了以下配置：

1. **环境变量**：
   - `ALIYUN_REPO`: 阿里云镜像仓库地址 `registry.cn-hangzhou.aliyuncs.com/bailangvvk/hugo`

2. **登录步骤**：
   - 添加了阿里云容器仓库登录步骤
   - 保留了DockerHub登录步骤

3. **构建推送**：
   - 同时推送到DockerHub和阿里云仓库
   - 支持多平台架构

## 需要配置的GitHub Secrets

在GitHub仓库的 Settings → Secrets and variables → Actions 中添加以下Secrets：

### 1. DockerHub Secrets（已存在）
- `DOCKERHUB_USERNAME`: 你的DockerHub用户名
- `DOCKERHUB_TOKEN`: 你的DockerHub访问令牌

### 2. 阿里云Secrets（需要添加）
- `ALIYUN_USERNAME`: 阿里云容器仓库用户名
- `ALIYUN_PASSWORD`: 阿里云容器仓库密码/访问令牌

## 如何获取阿里云凭证

1. 登录阿里云控制台
2. 进入容器镜像服务（ACR）
3. 选择地域（如杭州）
4. 创建命名空间（如 `bailangvvk`）
5. 获取访问凭证：
   - 在实例详情页找到"访问凭证"标签
   - 创建访问凭证（如果还没有）
   - 记录用户名和密码

## 镜像地址说明

配置完成后，镜像将被推送到：

- **DockerHub**: `bailangvvking/hugo:latest`
- **阿里云**: `registry.cn-hangzhou.aliyuncs.com/bailangvvk/hugo:latest`

## 验证配置

配置完成后，可以：

1. 手动触发workflow运行
2. 检查两个仓库是否都成功推送了镜像
3. 验证镜像是否可以正常拉取和运行

## 注意事项

- 确保阿里云仓库的命名空间已创建
- 阿里云的地域需要与仓库地址匹配（当前配置为杭州）
- 如果需要推送其他标签，可以修改 `IMAGE_TAG` 环境变量
- 当前配置支持多平台架构，如需调整请修改 `platforms` 参数