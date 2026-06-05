# 项目缓存模板 (_template.md)

> **说明**：此文件为项目缓存的模板定义，实际缓存文件名为 `{project-name}.md`。
>
> **生成时机**：首次使用 skill-selector 时通过 Bootstrap 流程自动生成。
>
> **更新频率**：项目重大变更后或手动刷新时更新。

---

## 缓存元信息

```yaml
cache_meta:
  version: "1.0.0"                    # 缓存格式版本
  project_name: "{project-name}"       # 项目名称（从 package.json 或目录名提取）
  project_path: "{absolute-path}"      # 项目绝对路径
  generated_at: "{ISO-8601-timestamp}" # 生成时间
  updated_at: "{ISO-8601-timestamp}"   # 最后更新时间
  generator: "skill-selector v1.0.0"   # 生成工具及版本
  bootstrap_duration_sec: {float}      # Bootstrap 耗时（秒）
  total_skills_count: {integer}        # 检测到的 Skill 总数
  cache_status: "active" | "stale" | "corrupted" | "deprecated"  # 缓存状态
  integrity_hash: "{SHA-256}"          # 内容完整性校验哈希
```

---

## 项目基本信息

```yaml
project_info:
  # 项目标识
  name: "{project-name}"
  display_name: "{显示名称}"
  description: "{项目描述}"

  # 技术栈
  tech_stack:
    language: ["TypeScript", "JavaScript", "Python"]  # 主要编程语言
    framework: ["Vue 3", "React", "Express"]           # 使用框架
    ui_library: ["NaiveUI", "Element Plus", "Ant Design"]  # UI 库
    build_tool: ["Vite", "Webpack", "esbuild"]         # 构建工具
    package_manager: "pnpm" | "npm" | "yarn"            # 包管理器

  # 项目结构特征
  structure:
    src_dir: "src"                      # 源码目录
    component_dir: "src/components"     # 组件目录
    view_dir: "src/views"               # 页面目录
    api_dir: "src/service/api"          # API 目录
    store_dir: "src/store"              # 状态管理目录
    hook_dir: "src/hooks"               # Hooks 目录
    type_dir: "src/typings"             # 类型定义目录

  # 关键配置文件
  config_files:
    - path: "package.json"
      last_modified: "{timestamp}"
      key_dependencies: {list}          # 关键依赖列表
    - path: "tsconfig.json"
      strict_mode: true                 # 是否启用严格模式
    - path: "vite.config.ts"
      plugins: {list}                   # 使用的插件列表

  # 项目规范
  conventions:
    naming_convention: "kebab-case"     # 命名规范
    component_style: "Composition API"  # 组件风格
    state_management: "Pinia"           # 状态管理方案
    i18n_enabled: true                  # 是否启用国际化
```

---

## 可用 Skills 列表

```yaml
skills:
  # ===== 核心 Skills (core/) =====
  - id: "core-auth"
    name: "auth-handler"
    display_name: "认证授权处理"
    category: "core/auth"
    description: "处理用户登录、注册、Token 管理、权限验证等认证授权相关操作"
    version: "2.1.0"
    status: "active"  # active | deprecated | experimental | archived
    priority: P0  # P0-P4 优先级

    # 匹配关键词（用于快速匹配）
    keywords:
      - "登录"
      - "logout"
      - "认证"
      - "authorization"
      - "token"
      - "权限"
      - "permission"
      - "用户验证"

    # 触发场景
    trigger_scenarios:
      - "用户请求登录/登出功能"
      - "需要验证用户身份"
      - "Token 刷新或过期处理"
      - "角色权限检查"

    # 功能清单
    capabilities:
      - name: "用户登录"
        description: "处理用户凭证验证和会话创建"
        token_cost_est: 300  # 预估 token 消耗
      - name: "用户登出"
        description: "安全终止用户会话"
        token_cost_est: 150
      - name: "Token 管理"
        description: "Token 的生成、验证、刷新"
        token_cost_est: 400
      - name: "权限检查"
        description: "基于角色的访问控制"
        token_cost_est: 250

    # 依赖关系
    dependencies:
      - skill_id: "utils-request"
        type: "required"  # required | optional | runtime
        reason: "依赖 HTTP 请求封装"

    # 文件位置
    file_location:
      skill_md: ".trae/skills/core-auth/SKILL.md"
      main_script: "src/hooks/business/auth/index.ts"
      related_files:
        - "src/service/api/auth.ts"
        - "src/store/modules/auth/index.ts"

    # 统计信息
    statistics:
      created_at: "{timestamp}"
      last_updated: "{timestamp}"
      usage_count_30d: 45  # 最近30天使用次数
      avg_execution_time_ms: 250  # 平均执行时间
      success_rate: 0.98  # 成功率 (0-1)
      user_satisfaction: 4.5  # 用户满意度 (1-5)

    # 脚本化信息（如适用）
    modular_structure:
      is_modularized: true
      index_file_size_tokens: 350
      modules:
        - name: "login"
          file: "modules/login.md"
          size_tokens: 400
          description: "登录流程模块"
        - name: "logout"
          file: "modules/logout.md"
          size_tokens: 300
          description: "登出流程模块"
        - name: "token"
          file: "modules/token.md"
          size_tokens: 500
          description: "Token 管理模块"

  # ===== 工具 Skills (utils/) =====
  - id: "utils-format"
    name: "format-utils"
    display_name: "格式化工具集"
    category: "utils/format"
    description: "提供日期、数字、字符串等各种数据格式的统一处理"
    version: "1.5.0"
    status: "active"
    priority: P1

    keywords:
      - "格式化"
      - "format"
      - "日期格式"
      - "数字格式"
      - "货币格式"
      - "字符串处理"

    trigger_scenarios:
      - "需要格式化日期时间"
      - "数字显示格式转换"
      - "字符串模板处理"
      - "数据展示格式化"

    capabilities:
      - name: "日期格式化"
        description: "支持多种日期格式输出"
        token_cost_est: 200
      - name: "数字格式化"
        description: "千分位、小数位、百分比等"
        token_cost_est: 150
      - name: "货币格式化"
        description: "多币种金额显示"
        token_cost_est: 180

    dependencies: []

    file_location:
      skill_md: ".trae/skills/utils-format/SKILL.md"
      main_script: "src/utils/common/formatter.ts"

    statistics:
      created_at: "{timestamp}"
      last_updated: "{timestamp}"
      usage_count_30d: 120
      avg_execution_time_ms: 50
      success_rate: 0.995
      user_satisfaction: 4.8

    modular_structure:
      is_modularized: false
      total_size_tokens: 650

  # ===== 基础设施 Skills (infra/) =====
  - id: "infra-deploy"
    name: "deploy-helper"
    display_name: "部署助手"
    category: "infra/deploy"
    description: "自动化构建、测试、部署流程的辅助工具"
    version: "1.2.0"
    status: "active"
    priority: P3

    keywords:
      - "部署"
      - "deploy"
      - "发布"
      - "publish"
      - "CI/CD"
      - "构建"
      - "build"

    trigger_scenarios:
      - "准备发布新版本"
      - "配置 CI/CD 流程"
      - "环境部署操作"
      - "构建产物优化"

    capabilities:
      - name: "版本号管理"
        description: "语义化版本号自动递增"
        token_cost_est: 200
      - name: "构建脚本生成"
        description: "根据环境生成构建命令"
        token_cost_est: 350
      - name: "部署检查清单"
        description: "部署前必要检查项"
        token_cost_est: 250

    dependencies:
      - skill_id: "utils-format"
        type: "optional"
        reason: "版本号格式化"

    file_location:
      skill_md: ".trae/skills/infra-deploy/SKILL.md"
      main_script: "scripts/deploy.mjs"

    statistics:
      created_at: "{timestamp}"
      last_updated: "{timestamp}"
      usage_count_30d: 15
      avg_execution_time_ms: 2000
      success_rate: 0.95
      user_satisfaction: 4.2

    modular_structure:
      is_modularized: true
      index_file_size_tokens: 280
      modules:
        - name: "version"
          file: "modules/version.md"
          size_tokens: 220
          description: "版本管理模块"
        - name: "build"
          file: "modules/build.md"
          size_tokens: 380
          description: "构建脚本模块"
        - name: "checklist"
          file: "modules/checklist.md"
          size_tokens: 300
          description: "检查清单模块"

# ... 更多 Skills 按此格式添加 ...
```

---

## 快速匹配索引

```yaml
quick_index:
  # 关键词 → Skill ID 映射（用于 O(1) 查找）
  keyword_mapping:
    "登录": ["core-auth"]
    "认证": ["core-auth"]
    "权限": ["core-auth"]
    "token": ["core-auth"]
    "格式化": ["utils-format"]
    "日期": ["utils-format"]
    "数字": ["utils-format"]
    "部署": ["infra-deploy"]
    "发布": ["infra-deploy"]
    "构建": ["infra-deploy"]

  # 场景 → Skill ID 映射
  scenario_mapping:
    "用户身份验证": ["core-auth"]
    "数据展示格式": ["utils-format"]
    "生产环境发布": ["infra-deploy"]

  # 操作类型 → 推荐 Skill 列表
  operation_recommendations:
    create:
      - skill_id: "core-auth"
        confidence: 0.95
        reason: "高频使用场景"
      - skill_id: "utils-format"
        confidence: 0.85
        reason: "通用需求"
    update:
      - skill_id: "infra-deploy"
        confidence: 0.90
        reason: "版本迭代必需"
    delete:
      warning: "删除操作需谨慎，建议先备份"
```

---

## 互斥关系矩阵

```yaml
mutual_exclusion_matrix:
  # 记录已检测到的互斥关系
  detected_conflicts:
    - conflict_id: "EX-20240101-001"
      type: "EX-05"  # 版本不兼容
      skills:
        - id: "database-mysql"
          version_requirement: "mysql2@^2.0"
        - id: "database-postgres"
          version_requirement: "pg@^8.0"
      confidence: 1.0
      detected_at: "{timestamp}"
      status: "open"  # open | resolved | ignored
      resolution: null
      notes: "两个数据库驱动不能同时安装"

    - conflict_id: "EX-20240101-002"
      type: "EX-01"  # 功能冲突
      skills:
        - id: "state-pinia"
          version_requirement: "pinia@^2.0"
        - id: "state-vuex"
          version_requirement: "vuex@^4.0"
      confidence: 0.98
      detected_at: "{timestamp}"
      status: "resolved"
      resolution: "项目已统一使用 Pinia，移除 Vuex 相关代码"
      resolved_at: "{timestamp}"
```

---

## 废弃与归档记录

```yaml
deprecation_records:
  deprecated_skills:
    - skill_id: "old-ajax-wrapper"
      name: "ajax-wrapper"
      deprecated_at: "{timestamp}"
      deprecation_reason: "已被 utils-request 完全替代"
      coverage_by_alternative: 0.95  # 替代方案的覆盖度
      alternative_skill_id: "utils-request"
      migration_guide_available: true
      retention_until: "{timestamp}"  # 保留至该时间
      status: "archived"  # archived | pending_deletion | deleted

  deprecation_statistics:
    total_deprecated: 2
    archived_count: 1
    pending_deletion_count: 1
    auto_clean_scheduled: "{timestamp}"
```

---

## 性能基线

```yaml
performance_baselines:
  # 各 Skill 的性能基准
  skill_baselines:
    core-auth:
      avg_token_cost: 350
      p95_token_cost: 600
      avg_execution_time_ms: 250
      p95_execution_time_ms: 500
      cache_hit_rate: 0.85  # 缓存命中率

    utils-format:
      avg_token_cost: 180
      p95_token_cost: 300
      avg_execution_time_ms: 50
      p95_execution_time_ms: 100
      cache_hit_rate: 0.92

  # 整体性能指标
  overall_metrics:
    total_avg_token_per_call: 280
    total_p95_token_per_call: 500
    cache_overall_hit_rate: 0.88
    bootstrap_time_last_run_sec: 12.5
    cache_size_kb: 45
```

---

## 健康状态

```yaml
health_status:
  last_check: "{timestamp}"
  check_interval_days: 7
  overall_health: "healthy"  # healthy | warning | critical

  checks:
    - check_type: "dependency_freshness"
      status: "pass"
      details: "所有依赖均为最新稳定版"
      last_check: "{timestamp}"

    - check_type: "skill_file_integrity"
      status: "pass"
      details: "所有 SKILL.md 文件完整且可解析"
      last_check: "{timestamp}"

    - check_type: "usage_anomaly_detection"
      status: "warning"
      details: "infra-deploy 使用率下降 40%，可能存在替代方案"
      recommendation: "建议评估是否需要合并或废弃"
      last_check: "{timestamp}"

    - check_type: "mutual_exclusion_drift"
      status: "pass"
      details: "未检测到新的互斥冲突"
      last_check: "{timestamp}"

  alerts:
    - alert_id: "HLT-20240101-001"
      severity: "warning"
      message: "Skill infra-deploy 使用频率异常下降"
      triggered_at: "{timestamp}"
      acknowledged: false
```

---

## 自主创建候选池

```yaml
auto_create_candidates:
  # 检测到可能需要自主创建的模式
  detected_patterns:
    - pattern_id: "PAT-20240101-001"
      pattern_name: "重复验证逻辑"
      detection_count: 8  # 检测次数
      confidence: 0.92  # 创建置信度
      suggested_skill_name: "validator-common"
      suggested_category: "core/validate"
      estimated_benefit: "节省约 60% 重复代码编写时间"
      estimated_token_cost: 450
      trigger_conditions_met: 5  # 满足的触发条件数
      status: "pending_review"  # pending_review | approved | rejected | created
      created_at: "{timestamp}"

  creation_history:
    - skill_id: "auto-created-format-date"
      original_pattern: "日期格式化重复请求"
      created_at: "{timestamp}"
      post_creation_usage_count: 25
      user_feedback: "positive"
```

---

## 配置覆写记录

```yaml
configuration_overrides:
  # 项目级别的配置覆写（如有）
  overrides:
    - config_key: "deprecated_threshold"
      default_value: 4
      overridden_value: 3  # 此项目更严格
      reason: "高质量要求，更早发现废弃 Skill"
      applied_at: "{timestamp}"

    - config_key: "health_check_interval_days"
      default_value: 7
      overridden_value: 3  # 更频繁的健康检查
      reason: "快速迭代项目，需及时发现问题"
      applied_at: "{timestamp}"
```

---

## 变更日志

```yaml
changelog:
  - version: "1.0.0"
    date: "{timestamp}"
    type: "initial"  # initial | update | refresh | manual
    changes:
      - "初始缓存生成"
      - "检测到 {count} 个 Skills"
      - "Bootstrap 耗时 {duration} 秒"
    author: "skill-selector-bootstrap"

  - version: "1.0.1"
    date: "{timestamp}"
    type: "update"
    changes:
      - "新增 Skill: deploy-helper"
      - "更新 auth-handler 至 v2.1.0"
      - "修复互斥冲突 EX-20240101-002"
    author: "auto-sync"

  - version: "1.1.0"
    date: "{timestamp}"
    type: "refresh"
    changes:
      - "全量刷新缓存"
      - "重新计算性能基线"
      - "更新健康状态"
    author: "manual-refresh"
```

---

## 附录：字段说明

### 必填字段 vs 可选字段

| 字段类别 | 字段名 | 是否必填 | 说明 |
|---------|-------|---------|------|
| 缓存元信息 | `version` | ✅ | 缓存格式版本 |
| 缓存元信息 | `project_name` | ✅ | 项目唯一标识 |
| 缓存元信息 | `generated_at` | ✅ | 生成时间戳 |
| 缓存元信息 | `cache_status` | ✅ | 当前缓存状态 |
| 项目信息 | `tech_stack.language` | ✅ | 至少一种语言 |
| Skill 列表 | `id` | ✅ | Skill 唯一标识 |
| Skill 列表 | `name` | ✅ | Skill 名称 |
| Skill 列表 | `keywords` | ✅ | 至少 3 个关键词 |
| Skill 列表 | `status` | ✅ | 当前状态 |
| Skill 列表 | `modular_structure` | ❌ | 仅脚本化 Skill 需要 |
| 互斥矩阵 | `detected_conflicts` | ❌ | 有冲突时才填写 |
| 废弃记录 | `deprecated_skills` | ❌ | 有废弃 Skill 时才填写 |

### 数据类型约定

| 类型 | 格式示例 | 说明 |
|-----|---------|------|
| 时间戳 | `2026-06-04T12:00:00+08:00` | ISO 8601 格式，含时区 |
| 版本号 | `1.2.3` | 语义化版本号 |
| 百分比 | `0.95` | 0-1 之间的小数 |
| 持续时间 | `12.5` | 单位为秒（字段名含 `_sec`）或毫秒（`_ms`）|
| 状态枚举 | `"active"` | 使用预定义的枚举值 |

### 命名规范

- **Skill ID**：使用 kebab-case，格式为 `{category}-{name}`
- **配置键**：使用 snake_case
- **枚举值**：使用 kebab-case 或 lowerCamelCase
- **文件引用**：使用相对于项目根目录的路径

---

> **模板版本**：1.0.0
> **最后更新**：2026-06-04
> **适用范围**：skill-selector v1.0.0+
