# SaveMD - Claude Code 文档保存技能

将当前项目的总结文档和提示词文档保存到指定文件夹，便于后续查阅和管理。

## 功能说明

将当前项目的总结文档和提示词文档分类保存到指定文件夹，并可生成项目总结和 Skill。
**配置会自动保存，首次使用后后续无需重新配置。**

## 可用指令

| 指令 | 说明 |
|------|------|
| `/SaveMD` | 保存文档到指定文件夹 |
| `/SaveMD --thismd` | 生成项目总结文档，保存到 `.SaveMD/` 目录 |
| `/SaveMD --this-skill` | 生成 Skill，保存到 `.SaveMD/` 目录 |
| `/SaveMD --config` | 查看当前配置 |
| `/SaveMD --reset` | 重置配置 |

---

## 安装方法

### 方法一：复制 SKILL.md

1. 在 Claude Code 中打开项目
2. 将 `save-md/SKILL.md` 的内容复制到项目 `.claude/skills/save-md/SKILL.md`

### 方法二：创建 skill 文件夹

```bash
mkdir -p ~/.claude/skills/save-md
# 将 SKILL.md 复制到该目录
```

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
/SaveMD targetFolder=C:\Backup\Docs # Windows绝对路径
/SaveMD targetFolder=/mnt/storage    # Unix绝对路径
/SaveMD targetFolder=./output        # 相对路径（项目目录下）
/SaveMD createProjectSubfolder=false # 不创建项目子文件夹
```

### 执行流程

1. 检查/加载配置
2. 扫描 `.md` 文件
3. 分类识别（提示词文档/总结文档/其他文档）
4. 确认文件列表
5. 执行保存
6. 显示保存结果

## License

AmberNya-2026
