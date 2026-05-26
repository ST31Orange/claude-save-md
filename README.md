# SaveMD - Claude Code 文档保存技能

将当前项目的总结文档和提示词文档保存到指定文件夹，便于后续查阅和管理。

## 功能

- `/SaveMD` - 保存文档到指定文件夹
- `/ThisMD` - 总结项目并生成总结文档
- `/ThisSkill` - 总结项目并生成可复用 Skill

## 安装方法

### 方法一：复制 SKILL.md

1. 在 Claude Code 中打开项目
2. 将 `save-md/SKILL.md` 的内容复制到项目 `.claude/skills/save-md/SKILL.md`

### 方法二：创建 skill 文件夹

```bash
mkdir -p ~/.claude/skills/save-md
# 将 SKILL.md 复制到该目录
```

## 配置

首次使用 `/SaveMD` 时会提示设置目标文件夹路径，配置会自动保存到 `~/.claude/save-md-config.json`

## 使用示例

```
/SaveMD                              # 使用默认 ~/ClaudeWork
/SaveMD targetFolder=~/Documents/归档 # 指定目标文件夹
/SaveMD targetFolder=C:\Backup\Docs # Windows绝对路径
/SaveMD targetFolder=/mnt/storage    # Unix绝对路径

/ThisMD                              # 生成项目总结文档
/ThisSkill                           # 生成项目Skill
```

## 配置参数

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `targetFolder` | `~/ClaudeWork` | 目标文件夹路径 |
| `createProjectSubfolder` | `true` | 是否创建项目子文件夹 |

## 路径格式支持

- `~/ClaudeWork` - 用户目录
- `C:\Users\XXX\Docs` - Windows 绝对路径
- `/mnt/storage` - Unix 绝对路径
- `./output` - 相对路径

## License

MIT