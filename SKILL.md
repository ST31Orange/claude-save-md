---
name: save-md
description: |
  将当前项目的总结文档和提示词文档保存到指定文件夹。 Use this whenever the user says "保存MD", "SaveMD", "/SaveMD", "备份文档", "整理文档", or wants to organize project markdown files into categorized folders. This skill helps organize and archive project documentation and prompts.
---

# SaveMD - 文档保存技能

## 功能说明

将当前项目的总结文档和提示词文档分类保存到指定文件夹，便于后续查阅和管理。
**配置会自动保存，首次使用后后续无需重新配置。**

## 可用指令

| 指令 | 说明 |
|------|------|
| `/SaveMD` | 保存文档到指定文件夹 |
| `/ThisMD` | 总结当前项目并生成总结文档 |
| `/ThisSkill` | 总结当前项目并生成Skill |

---

## /SaveMD - 保存文档

### 配置参数

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `targetFolder` | `~/ClaudeWork` | 目标文件夹路径（支持绝对路径和相对路径） |
| `createProjectSubfolder` | `true` | 是否创建项目子文件夹 |

### 路径格式说明

**支持以下路径格式：**

| 格式 | 示例 | 说明 |
|------|------|------|
| 用户目录 | `~/ClaudeWork` | 自动展开为用户主目录 |
| Windows绝对路径 | `C:\Users\XXX\Documents` | Windows盘符路径 |
| Windows UNC路径 | `\\server\share\folder` | 网络路径 |
| Unix绝对路径 | `/home/user/work` | Linux/Mac路径 |
| 相对路径 | `./output` 或 `../backup` | 相对于当前项目目录 |

### 使用示例

```
/SaveMD                              # 使用默认 ~/ClaudeWork
/SaveMD targetFolder=C:\Backup\Docs  # Windows绝对路径
/SaveMD targetFolder=/mnt/storage    # Unix绝对路径
/SaveMD targetFolder=./output       # 相对路径（项目目录下）
/SaveMD createProjectSubfolder=false # 不创建项目子文件夹
```

### 执行流程

1. 检查/加载配置
2. 扫描 `.md` 文件
3. 分类识别（提示词文档/总结文档/其他文档）
4. 确认文件列表
5. 执行保存
6. 显示保存结果

### 配置命令

```
/SaveMD --config    # 查看当前配置
/SaveMD --reset      # 重置配置
```

---

## /ThisMD - 项目总结文档

### 功能

总结当前项目的完成情况，分析关键决策点，思考如何写提示词才能下次一步到位，最终生成一份总结文档。

### 执行流程

**第一步：扫描项目**
- 扫描项目目录结构
- 读取所有 `.md` 文件内容
- 了解项目背景和当前状态

**第二步：总结完成情况**
- 完成了哪些内容
- 达到什么效果/成品

**第三步：分析关键决策**
- 过程中的关键选择点
- 为什么这样选择
- 有哪些替代方案

**第四步：思考提示词优化**
- 如果重头来，如何写提示词一次达到最终效果
- 需要包含哪些关键信息
- 避免哪些常见错误

**第五步：生成总结文档**
生成 `项目总结.md`，包含：

```markdown
# [项目名称] - 项目总结

## 项目概述
[项目背景和目标]

## 完成情况
### 已完成
- [列表]
### 效果/成品
- [描述]

## 关键决策点
| 决策 | 选择 | 原因 |
|------|------|------|
| ... | ... | ... |

## 提示词优化建议
### 如何一步到位
1. [关键提示词要素]
2. [需要包含的信息]
3. [常见错误避免]

## 踩坑记录
| 坑 | 问题 | 解决方案 |
|----|------|----------|
| ... | ... | ... |

## 下次参考
```
[可直接使用的提示词模板]
```
```

**第六步：保存**
询问用户是否保存到目标文件夹

---

## /ThisSkill - 项目Skill

### 功能

总结当前项目的完成情况，分析关键决策点，思考如何写提示词才能下次一步到位，最终打包成一个可复用的 Skill。

### 执行流程

**第一步~第四步：** 与 `/ThisMD` 相同

**第五步：生成 Skill 结构**

在项目目录下创建 Skill 文件：
```
[项目名]/
├── SKILL.md          # Skill定义文件
└── references/       # 参考资料目录（可选）
    ├── README.md
    └── templates/
```

**SKILL.md 结构：**

```markdown
---
name: [skill-name]
description: |
  [一句话描述技能用途和触发场景]
---

# [Skill名称]

## 功能说明
[详细说明这个Skill能做什么]

## 使用场景
[何时使用这个Skill]

## 使用示例
```
/[command] [参数]
```

## 执行流程
[详细执行步骤]

## 提示词模板
[可直接使用的提示词模板]

## 注意事项
[重要提醒]
```

**第六步：打包**
- 使用 skill-creator 打包
- 或者直接提供给用户

### Skill 命名建议

| 项目类型 | 建议名称 |
|----------|----------|
| 代码生成 | `code-gen-[语言/框架]` |
| 文档撰写 | `doc-writer-[类型]` |
| 数据分析 | `data-analysis-[场景]` |
| 特定领域 | `[领域]-helper` |

---

## 配置文件

配置保存在 `~/.claude/save-md-config.json`

---

## 错误处理

- 如果没有找到任何 .md 文件：提示用户并询问是否继续
- 如果目标文件夹创建失败：显示错误信息并终止
- 如果文件复制失败：跳过该文件并记录，继续处理其他文件

## 注意事项

1. 只会复制文件，不会移动或删除原始文件
2. 如果目标位置已有同名文件，自动覆盖
3. 使用中文回复用户