---
name: gcloud
description: Provides gcloud CLI commands and patterns for Google Cloud Platform. Use when answering questions about GCP services, creating cloud infrastructure, managing Kubernetes clusters (GKE), deploying serverless applications (Cloud Run, App Engine, Cloud Functions), handling IAM and authentication, or working with Cloud Storage and databases.
allowed-tools: Bash(gcloud *, gsutil *)
argument-hint: "[service-name or command]"
user-invocable: true
disable-model-invocation: false
---

# gcloud CLI 命令参考

## 初始化与版本管理

```bash
# 初始化 gcloud，包括授权和配置
gcloud init

# 显示版本和已安装的组件
gcloud version

# 安装特定组件
gcloud components install COMPONENT_ID

# 更新所有已安装的组件
gcloud components update

# 列出可用组件
gcloud components list
```

## 配置管理

```bash
# 设置配置属性
gcloud config set PROPERTY VALUE

# 常用配置示例
gcloud config set project PROJECT_ID
gcloud config set compute/zone ZONE
gcloud config set compute/region REGION

# 获取配置属性值
gcloud config get PROPERTY

# 列出所有配置属性
gcloud config list

# 取消设置配置属性
gcloud config unset PROPERTY
```

### 多配置管理

```bash
# 创建新的命名配置
gcloud config configurations create CONFIG_NAME

# 列出所有配置
gcloud config configurations list

# 激活指定配置
gcloud config configurations activate CONFIG_NAME

# 描述配置详情
gcloud config configurations describe CONFIG_NAME

# 删除配置
gcloud config configurations delete CONFIG_NAME
```

## 身份验证与凭证

```bash
# 使用用户账号登录授权
gcloud auth login

# 使用服务账号授权
gcloud auth activate-service-account --key-file=KEY_FILE

# 列出已授权的账号
gcloud auth list

# 打印当前账号的访问令牌
gcloud auth print-access-token

# 撤销账号凭证
gcloud auth revoke ACCOUNT

# 配置 Docker 使用 gcloud 凭据
gcloud auth configure-docker

# 为应用程序设置默认凭据 (ADC)
gcloud auth application-default login
```

## 项目管理

```bash
# 列出所有项目
gcloud projects list

# 描述项目详情
gcloud projects describe PROJECT_ID

# 创建新项目
gcloud projects create PROJECT_ID --name="PROJECT_NAME"

# 删除项目
gcloud projects delete PROJECT_ID

# 设置当前项目
gcloud config set project PROJECT_ID
```

## IAM 与服务账号

```bash
# 创建服务账号
gcloud iam service-accounts create SA_NAME \
    --display-name="DISPLAY_NAME"

# 列出服务账号
gcloud iam service-accounts list

# 创建服务账号密钥
gcloud iam service-accounts keys create KEY_FILE \
    --iam-account=SA_EMAIL

# 为项目添加 IAM 策略绑定
gcloud projects add-iam-policy-binding PROJECT_ID \
    --member="MEMBER" \
    --role="ROLE"

# 查看项目 IAM 策略
gcloud projects get-iam-policy PROJECT_ID

# 创建自定义角色
gcloud iam roles create ROLE_ID \
    --project=PROJECT_ID \
    --title="ROLE_TITLE" \
    --permissions="PERMISSIONS"
```

## Compute Engine (虚拟机)

```bash
# 创建虚拟机实例
gcloud compute instances create INSTANCE_NAME \
    --zone=ZONE \
    --machine-type=MACHINE_TYPE \
    --image-family=IMAGE_FAMILY \
    --image-project=IMAGE_PROJECT

# 列出所有实例
gcloud compute instances list

# 描述实例详情
gcloud compute instances describe INSTANCE_NAME --zone=ZONE

# 启动/停止/删除实例
gcloud compute instances start INSTANCE_NAME --zone=ZONE
gcloud compute instances stop INSTANCE_NAME --zone=ZONE
gcloud compute instances delete INSTANCE_NAME --zone=ZONE

# SSH 连接到实例
gcloud compute ssh INSTANCE_NAME --zone=ZONE

# 通过 SSH 在实例上执行命令
gcloud compute ssh INSTANCE_NAME --zone=ZONE --command="COMMAND"

# 复制文件到/从实例
gcloud compute scp LOCAL_FILE INSTANCE_NAME:REMOTE_PATH --zone=ZONE
gcloud compute scp INSTANCE_NAME:REMOTE_PATH LOCAL_FILE --zone=ZONE
```

### 磁盘与快照

```bash
# 创建磁盘
gcloud compute disks create DISK_NAME --zone=ZONE --size=SIZE

# 创建磁盘快照
gcloud compute disks snapshot DISK_NAME --zone=ZONE --snapshot-names=SNAPSHOT_NAME

# 列出快照
gcloud compute snapshots list

# 从快照创建磁盘
gcloud compute disks create DISK_NAME --source-snapshot=SNAPSHOT_NAME --zone=ZONE
```

### 网络

```bash
# 列出防火墙规则
gcloud compute firewall-rules list

# 创建防火墙规则
gcloud compute firewall-rules create RULE_NAME \
    --allow=PROTOCOL:PORT \
    --source-ranges=CIDR \
    --target-tags=TAGS

# 列出 VPC 网络
gcloud compute networks list

# 列出子网
gcloud compute networks subnets list
```

## Google Kubernetes Engine (GKE)

```bash
# 创建 GKE 集群
gcloud container clusters create CLUSTER_NAME \
    --zone=ZONE \
    --num-nodes=NUM_NODES

# 列出集群
gcloud container clusters list

# 获取集群凭据 (配置 kubectl)
gcloud container clusters get-credentials CLUSTER_NAME --zone=ZONE

# 调整集群节点数
gcloud container clusters resize CLUSTER_NAME \
    --zone=ZONE \
    --num-nodes=NUM_NODES

# 删除集群
gcloud container clusters delete CLUSTER_NAME --zone=ZONE

# 升级集群
gcloud container clusters upgrade CLUSTER_NAME --zone=ZONE
```

## App Engine

```bash
# 部署应用到 App Engine
gcloud app deploy

# 部署特定配置文件
gcloud app deploy app.yaml

# 查看应用日志
gcloud app logs read

# 实时查看日志
gcloud app logs tail

# 在浏览器中打开应用
gcloud app browse

# 列出服务
gcloud app services list

# 列出版本
gcloud app versions list

# 描述应用
gcloud app describe
```

## Cloud Functions

```bash
# 部署函数
gcloud functions deploy FUNCTION_NAME \
    --runtime=RUNTIME \
    --trigger-http \
    --entry-point=ENTRY_POINT

# 列出函数
gcloud functions list

# 调用函数
gcloud functions call FUNCTION_NAME --data='DATA'

# 查看函数日志
gcloud functions logs read FUNCTION_NAME

# 删除函数
gcloud functions delete FUNCTION_NAME
```

## Cloud Run

```bash
# 部署服务到 Cloud Run
gcloud run deploy SERVICE_NAME \
    --image=IMAGE_URL \
    --platform=managed \
    --region=REGION

# 列出服务
gcloud run services list

# 描述服务
gcloud run services describe SERVICE_NAME --region=REGION

# 删除服务
gcloud run services delete SERVICE_NAME --region=REGION

# 查看服务日志
gcloud run services logs read SERVICE_NAME --region=REGION
```

## Cloud Storage (gsutil)

```bash
# 创建存储桶
gsutil mb gs://BUCKET_NAME

# 列出存储桶
gsutil ls

# 列出存储桶内容
gsutil ls gs://BUCKET_NAME

# 复制文件到存储桶
gsutil cp LOCAL_FILE gs://BUCKET_NAME/

# 从存储桶下载文件
gsutil cp gs://BUCKET_NAME/OBJECT LOCAL_FILE

# 同步目录
gsutil rsync -r LOCAL_DIR gs://BUCKET_NAME/

# 删除对象
gsutil rm gs://BUCKET_NAME/OBJECT

# 删除存储桶
gsutil rb gs://BUCKET_NAME
```

## Cloud SQL

```bash
# 创建 Cloud SQL 实例
gcloud sql instances create INSTANCE_NAME \
    --database-version=DATABASE_VERSION \
    --tier=MACHINE_TYPE \
    --region=REGION

# 列出实例
gcloud sql instances list

# 连接到实例
gcloud sql connect INSTANCE_NAME --user=USER

# 创建数据库
gcloud sql databases create DATABASE_NAME --instance=INSTANCE_NAME

# 列出数据库
gcloud sql databases list --instance=INSTANCE_NAME
```

## Pub/Sub

```bash
# 创建主题
gcloud pubsub topics create TOPIC_NAME

# 列出主题
gcloud pubsub topics list

# 创建订阅
gcloud pubsub subscriptions create SUBSCRIPTION_NAME --topic=TOPIC_NAME

# 发布消息
gcloud pubsub topics publish TOPIC_NAME --message="MESSAGE"

# 拉取消息
gcloud pubsub subscriptions pull SUBSCRIPTION_NAME
```

## 全局标志

这些标志适用于大多数 gcloud 命令：

```bash
# 获取命令帮助
gcloud COMMAND --help

# 指定项目
gcloud COMMAND --project=PROJECT_ID

# 格式化输出
gcloud COMMAND --format=json
gcloud COMMAND --format=yaml
gcloud COMMAND --format="table(field1,field2)"
gcloud COMMAND --format="value(field)"

# 过滤结果
gcloud COMMAND --filter="EXPRESSION"

# 静默模式（跳过确认提示）
gcloud COMMAND --quiet

# 详细输出
gcloud COMMAND --verbosity=debug
```

## 常用过滤与格式化示例

```bash
# 列出特定区域的实例
gcloud compute instances list --filter="zone:us-central1-a"

# 列出运行中的实例
gcloud compute instances list --filter="status=RUNNING"

# 仅输出实例名称
gcloud compute instances list --format="value(name)"

# JSON 格式输出
gcloud compute instances list --format=json

# 表格格式输出指定字段
gcloud compute instances list --format="table(name,zone,status)"
```

## 常用区域与可用区

```bash
# 列出所有区域
gcloud compute regions list

# 列出所有可用区
gcloud compute zones list

# 常用区域示例
# - us-central1 (爱荷华)
# - us-east1 (南卡罗来纳)
# - europe-west1 (比利时)
# - asia-east1 (台湾)
# - asia-northeast1 (东京)
```

## 故障排查

```bash
# 查看当前配置
gcloud info

# 检查连接性
gcloud auth print-access-token

# 查看详细日志
gcloud COMMAND --verbosity=debug --log-http

# 重新初始化
gcloud init --console-only
```
