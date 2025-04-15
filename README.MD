# Greenbone Community Kubernetes 部署方案

本仓库提供了一个基于 [Greenbone Community Containers](https://greenbone.github.io/docs/latest/22.4/container/index.html) 生成的 Kubernetes 部署方案。通过该方案，您可以在 Kubernetes 集群中快速部署 Greenbone Vulnerability Management (GVM) 环境。

## 项目结构

- **`greenbone-community-kubernetes.yaml`**: 包含多个 Kubernetes 资源定义文件，用于部署 GVM 的各个组件，包括 Redis、PostgreSQL、GVMD、GSA、OpenVAS 等。
- **`gvm-feed-sync.yaml`**: 定义了一个定时任务（CronJob），用于定期同步 GVM 的 Feed 数据。
- **`LICENSE`**: 项目使用的许可证（GNU Affero General Public License v3）。
- **`README.MD`**: 项目说明文档。

## 部署说明

1. **准备工作**:
   - 确保您的 Kubernetes 集群已正确配置并可用。
   - 确保集群中已安装 `kubectl` 并可以正常访问。
   - 确保GVM资源被部署到同一个Kubernetes节点上，如果不能保证部署到相同节点，请使用 PersistentVolume 替代yaml中 hostPath 类型的 Volume 声明。

2. **部署Kubernetes资源**:
   ```bash
   kubectl apply -f greenbone-community-kubernetes.yaml

3. **等待GVM部署完成后，设置更新Feed的周期计划**
   ```bash
   kubectl apply -f gvm-feed-sync.yaml

4. **访问GVM**
通过 (http://your-kubernetes-node-ip:30001) 访问 GVM 服务，默认用户名密码为 `admin`，请在登录后在 settings 中自行修改密码。
