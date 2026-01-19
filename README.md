# 周周更新 (Rabbica Update)



## 功能特性

### 📋 更新检查机制
- **定时自动检查**：每日在指定时间点（0点、3点、5点、6点、8点、12点、15点、18点、23点）自动拉取更新信息
- **智能版本比对**：
  - 提取README.md中"--version tag"后的版本号与当前版本号进行比对
  - 若发现新版本：触发系统通知，提示"收到新版本更新，请前往查看"
  - 若版本号一致：比对补丁版本信息
  - 提取"--patch version"条目，对年、月、日分别进行比对
  - 若发现补丁更新：触发系统通知，提示"收到新版本参数补丁，请前往查看"

### 🎨 应用界面与交互
- **更新日志显示**：显示README文件中"--update log ch-"后的中文内容
- **操作按钮**：
  - 检测更新：主动触发拉取检查
  - 测试通知：测试通知功能
  - 拉取OA通知：手动拉取OA文件
  - 强制监听：3秒后执行监听逻辑
- **状态提示**：
  - 拉取失败："请检查网络环境，有的时候你需要一些外界帮助"
  - 无更新："已是最新版本"

### ⚙️ 技术特性
- **请求频率限制**：每分钟最多10次检查请求
- **网络请求优化**：超时控制，避免长时间阻塞
- **服务稳定性**：异常处理机制，确保单个拉取失败不会导致服务终止
- **资源优化**：暂停拉取期间释放不必要的系统资源

## 技术栈

- **开发语言**：Kotlin
- **构建工具**：Gradle
- **网络请求**：OkHttp
- **异步处理**：Kotlin Coroutines
- **后台任务**：WorkManager
- **UI组件**：Material Components
- **布局**：ConstraintLayout
- **依赖管理**：Gradle Version Catalog

## 安装方法

### 系统要求
- Android 16 (API Level 36) 及以上
- ROOT权限（用于读取系统分区文件）

### 安装步骤
1. 下载最新的APK文件
2. 允许安装未知来源应用
3. 安装APK文件
4. 授予应用所需权限

## 使用说明

### 首次启动
1. 应用启动后会自动初始化通知渠道
2. 请求通知权限
3. 加载更新日志

### 手动检查更新
1. 点击"检测更新"按钮
2. 应用会拉取最新的README.md文件
3. 显示检查结果和更新日志
4. 如有更新，触发系统通知

### 测试通知
1. 点击"测试通知"按钮
2. 10秒后会发送一条测试通知

### 拉取OA通知
1. 点击"拉取OA通知"按钮
2. 5秒后会拉取OA文件
3. 如有新通知，触发系统通知

### 强制监听
1. 点击"强制监听"按钮
2. 3秒后会执行监听逻辑
3. 拉取OA文件并处理

## 配置说明

### 定时检查时间点
应用每日在以下时间点自动检查更新：
- 0:00、3:00、5:00、6:00、8:00
- 12:00、15:00、18:00、23:00

### 请求频率限制
- 每分钟最多10次请求
- 超过限制后，请求会被拒绝

## 开发环境

### 环境要求
- JDK 11 及以上
- Android Studio 2023.1.1 及以上
- Gradle 8.13.1 及以上

### 构建命令
```bash
# 构建Debug版本
./gradlew assembleDebug

# 构建Release版本
./gradlew assembleRelease

# 运行测试
./gradlew test
```

## 项目结构

```
├── app/
│   ├── src/main/
│   │   ├── java/com/rabbica/update/
│   │   │   ├── MainActivity.kt           # 主界面
│   │   │   ├── UpdateChecker.kt          # 更新检查器
│   │   │   ├── UpdateApplication.kt      # 应用程序类
│   │   │   ├── UpdateService.kt          # 更新服务
│   │   │   ├── model/                    # 数据模型
│   │   │   ├── service/                  # 后台服务
│   │   │   │   ├── KeepAliveService.kt   # 保活服务
│   │   │   │   ├── NotificationService.kt # 通知服务
│   │   │   │   ├── OAMonitorService.kt   # OA监听服务
│   │   │   │   └── LowPowerNotificationService.kt # 低功耗服务
│   │   │   └── utils/                    # 工具类
│   │   │       ├── NetworkUtils.kt       # 网络工具
│   │   │       ├── NotificationUtils.kt  # 通知工具
│   │   │       ├── RootUtils.kt          # ROOT工具
│   │   │       └── WorkSchedulerUtils.kt # 任务调度工具
│   │   ├── res/                          # 资源文件
│   │   └── AndroidManifest.xml           # 应用清单
│   └── build.gradle.kts                  # 模块构建配置
├── gradle/                               # Gradle配置
└── README.md                             # 项目说明
```

## 贡献指南

欢迎提交Issue和Pull Request！

### 提交代码
1. Fork本仓库
2. 创建特性分支：`git checkout -b feature/feature-name`
3. 提交更改：`git commit -am 'Add some feature'`
4. 推送到分支：`git push origin feature/feature-name`
5. 提交Pull Request

### 代码规范
- 遵循Kotlin编码规范
- 使用Android Studio默认的代码格式化
- 添加必要的注释
- 编写测试用例

## 许可证

[MIT License](LICENSE)

## 联系方式

- 项目地址：https://gitee.com/RabbicaY/RabbicaUpdateApplication
- GitHub镜像：https://github.com/RabbicaY/RabbicaUpdateApplication

## 更新日志

### --update log ch-20260119
- 修复正则表达式转义序列错误
- 改进版本检查逻辑
- 优化补丁版本比对
- 增强错误处理

### --update log ch-20260108
- 添加强制监听按钮
- 实现3秒后执行监听逻辑
- 优化UI设计
- 修复已知bug

### --update log ch-20260107
- 实现系统更新检查机制
- 支持定时自动拉取
- 实现版本比对和通知提醒
- 优化请求频率限制

## 注意事项

1. 本应用需要ROOT权限才能读取系统分区文件
2. 应用依赖网络连接进行更新检查
3. 请确保应用有通知权限，否则无法接收更新提醒
4. 应用会在后台运行服务，可能会消耗一定的电池电量

## 免责声明

本应用仅供学习和研究使用，请勿用于商业用途。使用本应用造成的任何损失，作者不承担任何责任。

---

**周周更新**  🚀
