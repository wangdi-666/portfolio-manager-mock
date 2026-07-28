# Portfolio Manager 项目分工 Git 提交 Prompt（已填写）

## 项目概览

- **项目路径**：`C:\Users\QY\Desktop\Temp\portfolio-manager-mock`
- **项目类型**：Java Web 应用（投资组合管理系统）
- **技术栈**：Java 17 + Spring Boot 3.3.2 + Spring Security + Spring JDBC + MySQL 8 + Bootstrap 5.3 + Chart.js + H2（测试）
- **CI/CD**：GitHub Actions（CI 构建+测试 / CD Docker 镜像+部署）+ Dependabot
- **现有 Git**：已有 2 次提交（`project init` + `finish portfolio manager project`），需要重置后再分工提交
- **GitHub 仓库**：`[在此填写你的仓库地址]`

> ⚠️ 重置 Git 历史：进入项目目录执行 `rm -rf .git && git init && git branch -M main`，然后按下面的指南提交。



---

## 项目目录结构

```
portfolio-manager-mock/
├── pom.xml                                    # Maven 配置，依赖管理
├── mvnw / mvnw.cmd                           # Maven Wrapper 脚本
├── .mvn/wrapper/maven-wrapper.properties      # Maven Wrapper 配置
├── .gitignore                                # Git 忽略规则
├── .gitattributes                             # Git 属性配置
├── Dockerfile                                # 容器化配置（JRE 17 Alpine）
├── README.md                                 # 项目说明文档
│
├── .github/
│   ├── workflows/
│   │   ├── ci.yml                            # CI 工作流（Maven 构建+测试+报告）
│   │   └── cd.yml                            # CD 工作流（Docker 镜像构建+推送+部署通知）
│   └── dependabot.yml                        # 依赖更新自动化（Maven/Actions/Docker）
│
├── src/main/java/com/didi/portfoliomanagermock/
│   ├── PortfolioManagerMockApplication.java  # Spring Boot 启动入口
│   │
│   ├── config/
│   │   └── SecurityConfig.java              # Spring Security 安全配置
│   │
│   ├── controller/
│   │   ├── AuthController.java               # 认证接口（/api/auth/me）
│   │   ├── PageController.java              # 页面路由（/ → index.html）
│   │   ├── PortfolioController.java         # 投资组合 CRUD 接口
│   │   └── PriceSnapshotController.java     # 价格快照接口
│   │
│   ├── dto/
│   │   ├── AddPortfolioItemRequest.java      # 新增持仓请求 DTO
│   │   ├── PortfolioItemResponse.java        # 持仓响应 DTO
│   │   ├── PortfolioSummaryResponse.java     # 组合摘要响应 DTO
│   │   └── PriceSnapshotResponse.java        # 价格快照响应 DTO
│   │
│   ├── exception/
│   │   └── GlobalExceptionHandler.java       # 全局异常处理
│   │
│   ├── model/
│   │   ├── AssetType.java                    # 资产类型枚举（STOCK/BOND/CASH）
│   │   ├── PortfolioItem.java               # 持仓实体
│   │   ├── PriceSnapshot.java               # 价格快照实体
│   │   └── User.java                         # 用户实体
│   │
│   ├── repository/
│   │   ├── PortfolioItemRepository.java      # 持仓数据访问
│   │   ├── PriceSnapshotRepository.java      # 价格快照数据访问
│   │   └── UserRepository.java               # 用户数据访问
│   │
│   └── service/
│       ├── CurrentUserService.java          # 当前登录用户服务
│       ├── DataInitializer.java             # 数据初始化（默认用户）
│       ├── PortfolioService.java            # 投资组合业务逻辑
│       ├── PriceClientService.java          # 外部价格 API 客户端
│       └── PriceSnapshotService.java        # 价格快照业务逻辑
│
├── src/main/resources/
│   ├── application.properties                # 应用配置（端口/数据库/价格API）
│   ├── schema.sql                            # 数据库建表脚本
│   └── static/
│       ├── index.html                        # 主页面（仪表盘）
│       ├── login.html                        # 登录页面
│       ├── css/style.css                     # 样式表
│       └── js/
│           ├── api.js                        # 前端 API 封装
│           └── dashboard.js                  # 仪表盘逻辑（图表/表格/快照）
│
└── src/test/java/com/didi/portfoliomanagermock/
    └── PortfolioManagerMockApplicationTests.java  # 上下文加载测试
```

---

## 四人分工方案

| 成员  | Git 用户名  | Git 邮箱                 | 负责模块                   |
| --- | -------- | ---------------------- | ---------------------- |
| 成员A | studentA | <studentA@example.com> | 项目架构 & 安全认证 & CI 流水线   |
| 成员B | studentB | <studentB@example.com> | 投资组合核心业务 & CD 流水线      |
| 成员C | studentC | <studentC@example.com> | 价格快照模块 & 容器化           |
| 成员D | studentD | <studentD@example.com> | 前端界面 & 测试 & 文档 & CI 补充 |

### 成员A — 项目架构 & 安全认证 & CI 流水线

| 文件                                          | 说明                                   |
| ------------------------------------------- | ------------------------------------ |
| `pom.xml`                                   | Maven 依赖配置                           |
| `mvnw` / `mvnw.cmd`                         | Maven Wrapper 脚本                     |
| `.mvn/wrapper/maven-wrapper.properties`     | Maven Wrapper 版本配置                   |
| `.gitignore`                                | Git 忽略规则                             |
| `.gitattributes`                            | Git 属性（换行符）                          |
| `PortfolioManagerMockApplication.java`      | Spring Boot 启动类                      |
| `config/SecurityConfig.java`                | Security 过滤链、UserDetailsService、密码编码 |
| `model/User.java`                           | 用户实体类                                |
| `repository/UserRepository.java`            | 用户 JdbcTemplate 数据访问                 |
| `controller/AuthController.java`            | `/api/auth/me` 当前用户接口                |
| `controller/PageController.java`            | `/` 重定向到 index.html                  |
| `src/main/resources/application.properties` | 端口、数据库、价格 API 配置                     |
| `.github/workflows/ci.yml`                  | CI 工作流：Maven 构建 + 单元测试               |
| `.github/dependabot.yml`                    | 依赖更新自动化配置                            |

### 成员B — 投资组合核心业务 & CD 流水线

| 文件                                        | 说明                                          |
| ----------------------------------------- | ------------------------------------------- |
| `model/AssetType.java`                    | 资产类型枚举（STOCK / BOND / CASH）                 |
| `model/PortfolioItem.java`                | 持仓实体（ticker、数量、买入价、日期）                      |
| `dto/AddPortfolioItemRequest.java`        | 新增/更新持仓请求 DTO（含校验注解）                        |
| `dto/PortfolioItemResponse.java`          | 持仓响应 DTO（含当前价、市值、盈亏）                        |
| `dto/PortfolioSummaryResponse.java`       | 组合摘要 DTO（总成本、总市值、配置比例）                      |
| `repository/PortfolioItemRepository.java` | 持仓 CRUD（JdbcTemplate）                       |
| `service/PortfolioService.java`           | 核心业务逻辑（增删改查、摘要计算、盈亏计算）                      |
| `controller/PortfolioController.java`     | REST 接口（GET/POST/PUT/DELETE /api/portfolio） |
| `.github/workflows/cd.yml`                | CD 工作流：Docker 镜像构建 + 推送 + 部署通知              |

### 成员C — 价格快照模块 & 容器化

| 文件                                        | 说明                                                  |
| ----------------------------------------- | --------------------------------------------------- |
| `model/PriceSnapshot.java`                | 价格快照实体                                              |
| `dto/PriceSnapshotResponse.java`          | 快照响应 DTO                                            |
| `repository/PriceSnapshotRepository.java` | 快照数据访问（save / findLatest）                           |
| `service/PriceClientService.java`         | 外部价格 API 调用 + 45 秒缓存 + JSON 解析                      |
| `service/PriceSnapshotService.java`       | 快照同步 & 查询业务逻辑                                       |
| `controller/PriceSnapshotController.java` | REST 接口（sync / refresh / get / live）                |
| `src/main/resources/schema.sql`           | 三张建表 SQL（users / portfolio_items / price_snapshots） |
| `Dockerfile`                              | 容器化配置（JRE 17 Alpine + 健康检查）                         |

### 成员D — 前端界面 & 测试 & 文档 & 异常处理 & CI 补充

| 文件                                                       | 说明                         |
| -------------------------------------------------------- | -------------------------- |
| `src/main/resources/static/login.html`                   | 登录页面                       |
| `src/main/resources/static/index.html`                   | 主仪表盘页面（摘要/饼图/持仓表/快照）       |
| `src/main/resources/static/css/style.css`                | 全局样式                       |
| `src/main/resources/static/js/api.js`                    | 前端 API 封装（fetch 封装）        |
| `src/main/resources/static/js/dashboard.js`              | 仪表盘核心逻辑（404 行：表格/图表/快照/统计） |
| `exception/GlobalExceptionHandler.java`                  | 全局异常处理（校验/非法参数/未授权）        |
| `src/test/.../PortfolioManagerMockApplicationTests.java` | Spring Boot 上下文加载测试        |
| `README.md`                                              | 项目说明文档（含所有代码拆解）            |

---

## 同文件协作修改说明

> 真实团队协作中，同一文件经常被不同成员修改。以下 8 个文件存在跨成员修改，提交时间线中以 ⚡ 标注。

| 文件                         | 修改链                                                       | 说明                                                    |
| -------------------------- | --------------------------------------------------------- | ----------------------------------------------------- |
| `pom.xml`                  | A 创建(#1) → C 添加依赖(#10)                                    | C 开发价格客户端时需要 Jackson + HttpClient，在 A 的 pom.xml 上追加依赖 |
| `application.properties`   | A 创建(#2) → C 添加配置(#14)                                    | C 需要添加 `price.api.url` 和缓存参数，在 A 的配置文件上追加             |
| `schema.sql`               | C 创建(#4) → B 添加索引(#19)                                    | B 发现 portfolio_items 缺少用户外键索引，在 C 的建表脚本上补充            |
| `SecurityConfig.java`      | A 创建(#5) → B 放行接口(#13) → A 重构(#43)                        | B 的持仓 API 被 Security 拦截，在 A 的配置上添加放行规则；后期 A 统一重构权限配置  |
| `dashboard.js`             | D 创建(#26) → B 修复字段映射(#29)                                 | B 在联调时发现前端渲染字段与后端 DTO 不匹配，直接改了 D 的前端代码                |
| `.github/workflows/ci.yml` | A 创建(#15) → D 补充测试报告(#35)                                 | A 搭建 CI 基础流程后，D 添加了测试报告生成与 artifact 上传步骤              |
| `.github/workflows/cd.yml` | B 创建(#30) → A 添加安全扫描(#31)                                 | B 搭建 CD 基础流程后，A 在部署前增加了镜像安全扫描步骤                       |
| `README.md`                | D 编写(#36) → A 补充(#37) → B 补充(#38) → C 补充(#39) → D 整合(#41) | 每人各自补充负责模块的架构说明，最后由 D 统一整合格式                          |

---

## 提交时间线总表

> 开发周期：2026-03-02 ~ 2026-03-26（约 3.5 周）  
> 提交顺序按开发逻辑交叉排列  
> ⚡ 标记表示该提交修改了其他成员创建的文件

| #  | 成员 | 日期    | 时间    | 类型       | Commit Message                                           | 涉及文件                                                                                    | 协作     |
| -- | -- | ----- | ----- | -------- | -------------------------------------------------------- | --------------------------------------------------------------------------------------- | ------ |
| 1  | A  | 03-02 | 10:00 | chore    | chore: 初始化 Spring Boot 项目结构与 Maven 配置                    | pom.xml, mvnw, mvnw.cmd, .mvn/, .gitignore, .gitattributes                              |        |
| 2  | A  | 03-02 | 11:30 | feat     | feat(架构): 添加 Spring Boot 启动类与应用配置                        | PortfolioManagerMockApplication.java, application.properties                            |        |
| 3  | B  | 03-03 | 14:00 | feat     | feat(模型): 定义资产类型枚举与持仓实体                                  | AssetType.java, PortfolioItem.java                                                      |        |
| 4  | C  | 03-03 | 15:30 | feat     | feat(数据库): 创建 users/portfolio_items/price_snapshots 建表脚本 | schema.sql                                                                              |        |
| 5  | A  | 03-04 | 09:30 | feat     | feat(安全): 实现 Spring Security 表单登录与用户认证                   | SecurityConfig.java, User.java, UserRepository.java                                     |        |
| 6  | A  | 03-04 | 16:00 | feat     | feat(认证): 添加 AuthController 与 PageController             | AuthController.java, PageController.java                                                |        |
| 7  | A  | 03-05 | 10:00 | feat     | feat(服务): 实现当前用户服务与数据初始化器                                | CurrentUserService.java, DataInitializer.java                                           |        |
| 8  | B  | 03-06 | 14:00 | feat     | feat(DTO): 定义持仓请求与响应数据传输对象                               | AddPortfolioItemRequest.java, PortfolioItemResponse.java, PortfolioSummaryResponse.java |        |
| 9  | B  | 03-07 | 10:00 | feat     | feat(数据层): 实现持仓 Repository（JdbcTemplate CRUD）            | PortfolioItemRepository.java                                                            |        |
| 10 | C  | 03-07 | 15:00 | chore    | chore(依赖): 在 pom.xml 中添加 Jackson 与 HttpClient 依赖         | pom.xml                                                                                 | ⚡改A的   |
| 11 | B  | 03-09 | 15:00 | feat     | feat(业务): 实现投资组合 Service（增删改查+盈亏计算+摘要）                   | PortfolioService.java                                                                   |        |
| 12 | B  | 03-10 | 09:30 | feat     | feat(接口): 实现投资组合 REST Controller                         | PortfolioController.java                                                                |        |
| 13 | B  | 03-10 | 14:00 | fix      | fix(安全): 在 SecurityConfig 中放行 /api/portfolio 接口          | SecurityConfig.java                                                                     | ⚡改A的   |
| 14 | C  | 03-11 | 10:00 | chore    | chore(配置): 在 application.properties 中添加价格 API 地址与缓存配置    | application.properties                                                                  | ⚡改A的   |
| 15 | A  | 03-11 | 15:00 | ci       | ci: 添加 GitHub Actions CI 工作流（Maven 构建与单元测试）              | .github/workflows/ci.yml                                                                |        |
| 16 | C  | 03-11 | 16:00 | feat     | feat(模型): 定义价格快照实体与响应 DTO                                | PriceSnapshot.java, PriceSnapshotResponse.java                                          |        |
| 17 | C  | 03-12 | 10:30 | feat     | feat(数据层): 实现价格快照 Repository                             | PriceSnapshotRepository.java                                                            |        |
| 18 | C  | 03-13 | 15:00 | feat     | feat(价格客户端): 实现外部价格 API 调用与缓存机制                          | PriceClientService.java                                                                 |        |
| 19 | B  | 03-13 | 16:30 | fix      | fix(数据库): 为 portfolio_items 表添加用户外键索引                    | schema.sql                                                                              | ⚡改C的   |
| 20 | C  | 03-16 | 10:00 | feat     | feat(业务): 实现价格快照同步与查询服务                                  | PriceSnapshotService.java                                                               |        |
| 21 | C  | 03-17 | 14:00 | feat     | feat(接口): 实现价格快照 REST Controller                         | PriceSnapshotController.java                                                            |        |
| 22 | C  | 03-17 | 16:00 | docker   | docker: 添加 Dockerfile 容器化配置（JRE 17 Alpine + 健康检查）        | Dockerfile                                                                              |        |
| 23 | D  | 03-18 | 10:00 | feat     | feat(前端): 实现登录页面                                         | login.html                                                                              |        |
| 24 | D  | 03-18 | 15:00 | feat     | feat(前端): 搭建主仪表盘页面布局                                     | index.html                                                                              |        |
| 25 | D  | 03-19 | 10:00 | feat     | feat(前端): 实现前端 API 封装层                                   | api.js                                                                                  |        |
| 26 | D  | 03-19 | 16:00 | feat     | feat(前端): 实现仪表盘逻辑（表格/饼图/快照/统计）                           | dashboard.js                                                                            |        |
| 27 | D  | 03-20 | 10:00 | feat     | feat(前端): 添加全局样式表                                        | style.css                                                                               |        |
| 28 | D  | 03-20 | 14:00 | feat     | feat(异常): 实现全局异常处理器                                      | GlobalExceptionHandler.java                                                             |        |
| 29 | B  | 03-20 | 16:00 | fix      | fix(前端): 修复 dashboard.js 中持仓列表渲染字段映射错误                   | dashboard.js                                                                            | ⚡改D的   |
| 30 | B  | 03-21 | 10:00 | cd       | cd: 添加 GitHub Actions CD 工作流（Docker 镜像构建与推送）             | .github/workflows/cd.yml                                                                |        |
| 31 | A  | 03-21 | 14:00 | ci       | ci(安全): 在 CD 工作流中添加镜像安全扫描步骤                              | .github/workflows/cd.yml                                                                | ⚡改B的   |
| 32 | C  | 03-23 | 10:00 | fix      | fix(价格): 修复价格缓存失效后未清除旧数据的问题                              | PriceClientService.java                                                                 |        |
| 33 | B  | 03-23 | 14:00 | fix      | fix(业务): 修复持仓更新时未校验所属用户的问题                               | PortfolioService.java, PortfolioItemRepository.java                                     |        |
| 34 | D  | 03-24 | 10:00 | test     | test: 添加 Spring Boot 上下文加载测试                             | PortfolioManagerMockApplicationTests.java                                               |        |
| 35 | D  | 03-24 | 11:00 | ci       | ci: 在 CI 工作流中添加测试报告上传与 artifact 步骤                       | .github/workflows/ci.yml                                                                | ⚡改A的   |
| 36 | D  | 03-24 | 15:00 | docs     | docs: 编写项目 README（简介/技术栈/安装/运行/API）                      | README.md                                                                               |        |
| 37 | A  | 03-25 | 10:00 | docs     | docs(README): 补充安全认证模块架构说明                               | README.md                                                                               | ⚡改D的   |
| 38 | B  | 03-25 | 11:00 | docs     | docs(README): 补充投资组合核心业务模块说明                             | README.md                                                                               | ⚡改D的   |
| 39 | C  | 03-25 | 14:00 | docs     | docs(README): 补充价格快照模块说明                                 | README.md                                                                               | ⚡改D的   |
| 40 | A  | 03-25 | 16:00 | chore    | chore: 添加 Dependabot 依赖更新自动化配置                           | .github/dependabot.yml                                                                  |        |
| 41 | D  | 03-26 | 10:00 | docs     | docs: 在 README 中整合代码拆解与分工说明                              | README.md                                                                               | ⚡改D自己的 |
| 42 | B  | 03-26 | 14:00 | refactor | refactor(业务): 优化盈亏计算精度（BigDecimal scale）                 | PortfolioService.java                                                                   |        |
| 43 | A  | 03-26 | 16:00 | refactor | refactor(安全): 优化 SecurityConfig 权限配置，合并放行规则              | SecurityConfig.java                                                                     | ⚡改自己的  |

> 合计 43 次提交：A 10 次、B 12 次、C 11 次、D 10 次  
> 其中 14 次提交涉及修改他人创建的文件（⚡标记），涉及 8 个文件

---

## 各成员手动提交指南

### 成员A 提交指南

**你的信息**

- Git 用户名：studentA
- Git 邮箱：<studentA@example.com>
- 负责模块：项目架构 & 安全认证 & CI 流水线

**提交前准备（只需做一次）**

```bash
cd C:\Users\QY\Desktop\Temp\portfolio-manager-mock
git config user.name "studentA"
git config user.email "studentA@example.com"
```

**你的提交任务（按全局顺序执行）**

#### 第 1 次提交（全局 #1）

- 建议时间：03-02 10:00
- 提交命令：

```bash
git add pom.xml mvnw mvnw.cmd .mvn/wrapper/maven-wrapper.properties .gitignore .gitattributes
git commit -m "chore: 初始化 Spring Boot 项目结构与 Maven 配置"
```

#### 第 2 次提交（全局 #2）

- 建议时间：03-02 11:30
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/PortfolioManagerMockApplication.java src/main/resources/application.properties
git commit -m "feat(架构): 添加 Spring Boot 启动类与应用配置"
```

> ⏸ 等待成员B提交 #3、成员C提交 #4 后继续

#### 第 3 次提交（全局 #5）

- 建议时间：03-04 09:30
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/config/SecurityConfig.java src/main/java/com/didi/portfoliomanagermock/model/User.java src/main/java/com/didi/portfoliomanagermock/repository/UserRepository.java
git commit -m "feat(安全): 实现 Spring Security 表单登录与用户认证"
```

#### 第 4 次提交（全局 #6）

- 建议时间：03-04 16:00
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/controller/AuthController.java src/main/java/com/didi/portfoliomanagermock/controller/PageController.java
git commit -m "feat(认证): 添加 AuthController 与 PageController"
```

#### 第 5 次提交（全局 #7）

- 建议时间：03-05 10:00
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/service/CurrentUserService.java src/main/java/com/didi/portfoliomanagermock/service/DataInitializer.java
git commit -m "feat(服务): 实现当前用户服务与数据初始化器"
```

> ⏸ 等待成员B提交 #11~#13、成员C提交 #14 后继续

#### 第 6 次提交（全局 #15）

- 建议时间：03-11 15:00
- 说明：项目基础后端已成型，搭建 GitHub Actions CI 工作流，配置 JDK 17 + Maven 缓存 + 构建 + 单元测试
- 提交命令：

```bash
git add .github/workflows/ci.yml
git commit -m "ci: 添加 GitHub Actions CI 工作流（Maven 构建与单元测试）"
```

> ⏸ 等待成员B提交 #30 后继续

#### 第 7 次提交（全局 #31）⚡ 修改 B 创建的 cd.yml

- 建议时间：03-21 14:00
- 说明：B 刚搭建好 CD 流程(#30)，你在 Docker 推送前增加镜像安全扫描步骤（trivy/aqua 扫描），防止带漏洞的镜像进入生产环境
- 提交命令：

```bash
git add .github/workflows/cd.yml
git commit -m "ci(安全): 在 CD 工作流中添加镜像安全扫描步骤"
```

> ⏸ 等待其他成员提交 #32~#39 后继续

#### 第 8 次提交（全局 #37）⚡ 修改 D 创建的 README.md

- 建议时间：03-25 10:00
- 说明：在 README.md 中补充你负责的安全认证模块架构说明（Security 过滤链设计、UserDetailsService 实现、密码编码方案、CI/CD 流水线说明等）
- 提交命令：

```bash
git add README.md
git commit -m "docs(README): 补充安全认证模块架构说明"
```

#### 第 9 次提交（全局 #40）

- 建议时间：03-25 16:00
- 说明：添加 Dependabot 配置，自动监控 Maven 依赖、GitHub Actions 版本和 Docker 基础镜像更新
- 提交命令：

```bash
git add .github/dependabot.yml
git commit -m "chore: 添加 Dependabot 依赖更新自动化配置"
```

> ⏸ 等待成员D提交 #41、成员B提交 #42 后继续

#### 第 10 次提交（全局 #43）⚡ 修改自己创建的 SecurityConfig.java

- 建议时间：03-26 16:00
- 说明：B 在 #13 中往 SecurityConfig 添加了 /api/portfolio 放行规则，你此时统一重构权限配置，合并散乱的放行规则
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/config/SecurityConfig.java
git commit -m "refactor(安全): 优化 SecurityConfig 权限配置，合并放行规则"
```

**推送到 GitHub（所有人完成后统一执行）**

```bash
git remote add origin [你的仓库地址]
git push -u origin main
```

---

### 成员B 提交指南

**你的信息**

- Git 用户名：studentB
- Git 邮箱：<studentB@example.com>
- 负责模块：投资组合核心业务 & CD 流水线

**提交前准备（只需做一次）**

```bash
cd C:\Users\QY\Desktop\Temp\portfolio-manager-mock
git config user.name "studentB"
git config user.email "studentB@example.com"
```

**你的提交任务**

#### 第 1 次提交（全局 #3）

- 建议时间：03-03 14:00
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/model/AssetType.java src/main/java/com/didi/portfoliomanagermock/model/PortfolioItem.java
git commit -m "feat(模型): 定义资产类型枚举与持仓实体"
```

> ⏸ 等待成员C提交 #4、成员A提交 #5~#7 后继续

#### 第 2 次提交（全局 #8）

- 建议时间：03-06 14:00
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/dto/AddPortfolioItemRequest.java src/main/java/com/didi/portfoliomanagermock/dto/PortfolioItemResponse.java src/main/java/com/didi/portfoliomanagermock/dto/PortfolioSummaryResponse.java
git commit -m "feat(DTO): 定义持仓请求与响应数据传输对象"
```

#### 第 3 次提交（全局 #9）

- 建议时间：03-07 10:00
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/repository/PortfolioItemRepository.java
git commit -m "feat(数据层): 实现持仓 Repository（JdbcTemplate CRUD）"
```

> ⏸ 等待成员C提交 #10、成员A提交 #15 后继续

#### 第 4 次提交（全局 #11）

- 建议时间：03-09 15:00
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/service/PortfolioService.java
git commit -m "feat(业务): 实现投资组合 Service（增删改查+盈亏计算+摘要）"
```

#### 第 5 次提交（全局 #12）

- 建议时间：03-10 09:30
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/controller/PortfolioController.java
git commit -m "feat(接口): 实现投资组合 REST Controller"
```

#### 第 6 次提交（全局 #13）⚡ 修改 A 创建的 SecurityConfig.java

- 建议时间：03-10 14:00
- 说明：你的持仓 API `/api/portfolio/**` 被 Security 拦截返回 401，需要在 A 的 SecurityConfig 中添加放行规则
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/config/SecurityConfig.java
git commit -m "fix(安全): 在 SecurityConfig 中放行 /api/portfolio 接口"
```

#### 第 7 次提交（全局 #19）⚡ 修改 C 创建的 schema.sql

- 建议时间：03-13 16:30
- 说明：联调时发现 portfolio_items 按用户查询很慢，在 C 的建表脚本中补充用户外键索引
- 提交命令：

```bash
git add src/main/resources/schema.sql
git commit -m "fix(数据库): 为 portfolio_items 表添加用户外键索引"
```

#### 第 8 次提交（全局 #29）⚡ 修改 D 创建的 dashboard.js

- 建议时间：03-20 16:00
- 说明：前端联调时发现 dashboard.js 中持仓列表的字段名与后端 DTO 不匹配（如用了 `profitLoss` 但后端返回 `pnl`），直接改了 D 的前端代码
- 提交命令：

```bash
git add src/main/resources/static/js/dashboard.js
git commit -m "fix(前端): 修复 dashboard.js 中持仓列表渲染字段映射错误"
```

#### 第 9 次提交（全局 #30）

- 建议时间：03-21 10:00
- 说明：C 已完成 Dockerfile(#22)，你搭建 CD 工作流：Docker 镜像构建 + 推送到 Docker Hub + 部署通知
- 提交命令：

```bash
git add .github/workflows/cd.yml
git commit -m "cd: 添加 GitHub Actions CD 工作流（Docker 镜像构建与推送）"
```

> ⏸ 等待成员A提交 #31、成员C提交 #32 后继续

#### 第 10 次提交（全局 #33）

- 建议时间：03-23 14:00
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/service/PortfolioService.java src/main/java/com/didi/portfoliomanagermock/repository/PortfolioItemRepository.java
git commit -m "fix(业务): 修复持仓更新时未校验所属用户的问题"
```

#### 第 11 次提交（全局 #38）⚡ 修改 D 创建的 README.md

- 建议时间：03-25 11:00
- 说明：A 刚在 README 补充了安全模块(#37)，你接着补充投资组合核心业务模块说明（DTO 设计、Service 盈亏计算逻辑、Controller 接口列表、CD 流水线说明）
- 提交命令：

```bash
git add README.md
git commit -m "docs(README): 补充投资组合核心业务模块说明"
```

> ⏸ 等待成员C提交 #39、成员A提交 #40、成员D提交 #41 后继续

#### 第 12 次提交（全局 #42）

- 建议时间：03-26 14:00
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/service/PortfolioService.java
git commit -m "refactor(业务): 优化盈亏计算精度（BigDecimal scale）"
```

**推送到 GitHub**

```bash
# 如果你是第一个推送的：
git remote add origin [仓库地址]
git push -u origin main
# 如果已有人推送过：
# git pull --rebase origin main
# git push origin main
```

---

### 成员C 提交指南

**你的信息**

- Git 用户名：studentC
- Git 邮箱：<studentC@example.com>
- 负责模块：价格快照模块 & 容器化

**提交前准备（只需做一次）**

```bash
cd C:\Users\QY\Desktop\Temp\portfolio-manager-mock
git config user.name "studentC"
git config user.email "studentC@example.com"
```

**你的提交任务**

#### 第 1 次提交（全局 #4）

- 建议时间：03-03 15:30
- 提交命令：

```bash
git add src/main/resources/schema.sql
git commit -m "feat(数据库): 创建 users/portfolio_items/price_snapshots 建表脚本"
```

> ⏸ 等待成员A提交 #5~#7、成员B提交 #8~#9 后继续

#### 第 2 次提交（全局 #10）⚡ 修改 A 创建的 pom.xml

- 建议时间：03-07 15:00
- 说明：你开发价格客户端需要 Jackson（JSON 解析）和 Java HttpClient，在 A 的 pom.xml 中追加这两个依赖
- 提交命令：

```bash
git add pom.xml
git commit -m "chore(依赖): 在 pom.xml 中添加 Jackson 与 HttpClient 依赖"
```

> ⏸ 等待成员B提交 #11~#13、成员A提交 #15 后继续

#### 第 3 次提交（全局 #14）⚡ 修改 A 创建的 application.properties

- 建议时间：03-11 10:00
- 说明：你需要配置外部价格 API 地址和缓存超时时间，在 A 的 application.properties 中追加配置项
- 提交命令：

```bash
git add src/main/resources/application.properties
git commit -m "chore(配置): 在 application.properties 中添加价格 API 地址与缓存配置"
```

#### 第 4 次提交（全局 #16）

- 建议时间：03-11 16:00
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/model/PriceSnapshot.java src/main/java/com/didi/portfoliomanagermock/dto/PriceSnapshotResponse.java
git commit -m "feat(模型): 定义价格快照实体与响应 DTO"
```

#### 第 5 次提交（全局 #17）

- 建议时间：03-12 10:30
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/repository/PriceSnapshotRepository.java
git commit -m "feat(数据层): 实现价格快照 Repository"
```

#### 第 6 次提交（全局 #18）

- 建议时间：03-13 15:00
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/service/PriceClientService.java
git commit -m "feat(价格客户端): 实现外部价格 API 调用与缓存机制"
```

> ⏸ 等待成员B提交 #19 后继续

#### 第 7 次提交（全局 #20）

- 建议时间：03-16 10:00
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/service/PriceSnapshotService.java
git commit -m "feat(业务): 实现价格快照同步与查询服务"
```

#### 第 8 次提交（全局 #21）

- 建议时间：03-17 14:00
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/controller/PriceSnapshotController.java
git commit -m "feat(接口): 实现价格快照 REST Controller"
```

#### 第 9 次提交（全局 #22）

- 建议时间：03-17 16:00
- 说明：所有后端模块开发完成，编写 Dockerfile 配置容器化部署（JRE 17 Alpine 基础镜像 + 健康检查 + 环境变量）
- 提交命令：

```bash
git add Dockerfile
git commit -m "docker: 添加 Dockerfile 容器化配置（JRE 17 Alpine + 健康检查）"
```

> ⏸ 等待成员B提交 #29~#30、成员A提交 #31 后继续

#### 第 10 次提交（全局 #32）

- 建议时间：03-23 10:00
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/service/PriceClientService.java
git commit -m "fix(价格): 修复价格缓存失效后未清除旧数据的问题"
```

#### 第 11 次提交（全局 #39）⚡ 修改 D 创建的 README.md

- 建议时间：03-25 14:00
- 说明：A(#37) 和 B(#38) 已各自补充了模块说明，你接着补充价格快照模块（PriceClientService 缓存机制、快照同步流程、REST 接口列表、Dockerfile 容器化说明）
- 提交命令：

```bash
git add README.md
git commit -m "docs(README): 补充价格快照模块说明"
```

**推送到 GitHub**

```bash
# 如果已有人推送过：
# git pull --rebase origin main
git push origin main
```

---

### 成员D 提交指南

**你的信息**

- Git 用户名：studentD
- Git 邮箱：<studentD@example.com>
- 负责模块：前端界面 & 测试 & 文档 & 异常处理 & CI 补充

**提交前准备（只需做一次）**

```bash
cd C:\Users\QY\Desktop\Temp\portfolio-manager-mock
git config user.name "studentD"
git config user.email "studentD@example.com"
```

**你的提交任务**

> ⏸ 等待后端 API 开发完成（全局 #1~#22）后开始

#### 第 1 次提交（全局 #23）

- 建议时间：03-18 10:00
- 提交命令：

```bash
git add src/main/resources/static/login.html
git commit -m "feat(前端): 实现登录页面"
```

#### 第 2 次提交（全局 #24）

- 建议时间：03-18 15:00
- 提交命令：

```bash
git add src/main/resources/static/index.html
git commit -m "feat(前端): 搭建主仪表盘页面布局"
```

#### 第 3 次提交（全局 #25）

- 建议时间：03-19 10:00
- 提交命令：

```bash
git add src/main/resources/static/js/api.js
git commit -m "feat(前端): 实现前端 API 封装层"
```

#### 第 4 次提交（全局 #26）

- 建议时间：03-19 16:00
- 提交命令：

```bash
git add src/main/resources/static/js/dashboard.js
git commit -m "feat(前端): 实现仪表盘逻辑（表格/饼图/快照/统计）"
```

#### 第 5 次提交（全局 #27）

- 建议时间：03-20 10:00
- 提交命令：

```bash
git add src/main/resources/static/css/style.css
git commit -m "feat(前端): 添加全局样式表"
```

#### 第 6 次提交（全局 #28）

- 建议时间：03-20 14:00
- 提交命令：

```bash
git add src/main/java/com/didi/portfoliomanagermock/exception/GlobalExceptionHandler.java
git commit -m "feat(异常): 实现全局异常处理器"
```

> ⏸ 注意：B 会在 #29 修改你的 dashboard.js 修复字段映射问题，等待他提交后继续

#### 第 7 次提交（全局 #34）

- 建议时间：03-24 10:00
- 提交命令：

```bash
git add src/test/java/com/didi/portfoliomanagermock/PortfolioManagerMockApplicationTests.java
git commit -m "test: 添加 Spring Boot 上下文加载测试"
```

#### 第 8 次提交（全局 #35）⚡ 修改 A 创建的 ci.yml

- 建议时间：03-24 11:00
- 说明：你刚写完测试(#34)，在 A 搭建的 CI 流程基础上补充测试报告生成（surefire-report）和 artifact 上传步骤，让 CI 结果更完善
- 提交命令：

```bash
git add .github/workflows/ci.yml
git commit -m "ci: 在 CI 工作流中添加测试报告上传与 artifact 步骤"
```

#### 第 9 次提交（全局 #36）

- 建议时间：03-24 15:00
- 提交命令：

```bash
git add README.md
git commit -m "docs: 编写项目 README（简介/技术栈/安装/运行/API）"
```

> ⏸ 等待 A(#37)、B(#38)、C(#39) 各自补充 README 后继续

#### 第 10 次提交（全局 #41）⚡ 整合所有人修改过的 README.md

- 建议时间：03-26 10:00
- 说明：A、B、C 已各自在 README 中补充了模块说明，你此时统一整合格式、添加目录树、补充所有代码文件拆解和分工表
- 提交命令：

```bash
git add README.md
git commit -m "docs: 在 README 中整合代码拆解与分工说明"
```

**推送到 GitHub**

```bash
# 如果已有人推送过：
# git pull --rebase origin main
git push origin main
```

---

## 执行顺序说明

四人按以下顺序交替操作（每人只需在自己标记的时间点提交）：

```
第1周 (03/02-03/05):  A→A→B→C→A→A→A           （项目初始化 + 安全认证）
第2周 (03/06-03/13):  B→B→C⚡→B→B→B⚡→C⚡→A(ci)→C→C→C→B⚡  （核心业务+价格模块+CI+跨文件修改）
第3周 (03/16-03/21):  C→C→C(docker)→D→D→D→D→D→D→B⚡→B(cd)→A⚡(ci)  （前端+容器化+CD+联调修复）
第4周 (03/23-03/26):  C→B→D(test)→D⚡(ci)→D(docs)→A⚡(docs)→B⚡(docs)→C⚡(docs)→A(deps)→D⚡(docs)→B→A⚡  （修复+测试+文档协作+收尾）
```

> 💡 实际操作时不需要严格按分钟执行，只要大致日期对、顺序对即可。建议用一个共享文档跟踪当前进度，确认上一个人提交后再开始自己的部分。  
> ⚡ 标记的提交涉及修改其他成员的文件，执行前建议先 `git pull` 拉取最新代码，避免冲突。

## CI/CD 文件说明

### `.github/workflows/ci.yml` — 持续集成

- **触发条件**：push 到 main/develop 分支，或 PR 到 main
- **流程**：Checkout → JDK 17 → Maven 缓存 → 构建（跳过测试）→ 运行测试 → 上传 artifact → 生成测试报告
- **创建**：A 搭建基础流程(#15) → D 补充测试报告与 artifact 上传(#35)

### `.github/workflows/cd.yml` — 持续部署

- **触发条件**：push 到 main 分支、打 tag（v*）、手动触发、CI 完成后自动触发
- **流程**：Checkout → JDK 17 → 构建 JAR → 提取版本号 → Docker Buildx → 登录 Docker Hub → 构建推送镜像 → 部署通知
- **创建**：B 搭建基础流程(#30) → A 添加镜像安全扫描步骤(#31)

### `Dockerfile` — 容器化

- **基础镜像**：eclipse-temurin:17-jre-alpine
- **配置**：JVM 参数、数据源环境变量、健康检查（/api/auth/me）
- **创建**：C(#22)

### `.github/dependabot.yml` — 依赖管理

- **监控范围**：Maven 依赖（每周）、GitHub Actions（每周）、Docker 基础镜像（每月）
- **创建**：A(#40)

## 重置 Git 并开始

```bash
cd C:\Users\QY\Desktop\Temp\portfolio-manager-mock

# 1. 删除旧 Git 历史
rm -rf .git

# 2. 重新初始化
git init
git branch -M main

# 3. 按上面的指南开始提交
# 第一个提交的人（成员A）执行：
git add pom.xml mvnw mvnw.cmd .mvn/wrapper/maven-wrapper.properties .gitignore .gitattributes
git commit -m "chore: 初始化 Spring Boot 项目结构与 Maven 配置"

# 4. 所有提交完成后推送到 GitHub
git remote add origin [你的仓库地址]
git push -u origin main
```

## 同文件修改注意事项

当多人修改同一文件时，需特别注意以下操作：

1. **提交前先拉取**：每次提交前执行 `git pull --rebase origin main`，确保本地是最新代码
2. **修改别人文件时**：只改你需要改的部分，不要重构别人的代码格式
3. **README 协作流程**：D 先写好整体框架(#36) → A/B/C 各自追加模块说明(#37-39) → D 统一整合格式(#41)
4. **SecurityConfig 协作流程**：A 写好初始配置(#5) → B 追加放行规则(#13) → A 后期统一重构(#43)
5. **CI/CD 协作流程**：A 搭建 CI 基础(#15) → B 搭建 CD 基础(#30) → A 在 CD 加安全扫描(#31) → D 在 CI 加测试报告(#35)
6. **冲突处理**：如果 `git pull --rebase` 出现冲突，手动解决后 `git add <文件>` → `git rebase --continue`
