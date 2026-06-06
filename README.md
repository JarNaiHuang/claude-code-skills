# Claude Code 自定义 Skills

个人的 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 自定义 Skills 集合。

## Skills 列表

| Skill | 文件 | 说明 |
|-------|------|------|
| api-test-cases | [commands/api-test-cases.md](commands/api-test-cases.md) | 根据API接口文档生成全面的接口测试用例 |

## 使用方法

### 方式一：复制到用户级命令目录

```powershell
# Windows
Copy-Item commands\api-test-cases.md $env:USERPROFILE\.claude\commands\

# macOS/Linux
cp commands/api-test-cases.md ~/.claude/commands/
```

然后在 Claude Code 中使用：
```
/user:api-test-cases <粘贴API文档或文件路径>
```

### 方式二：克隆后软链接

```powershell
# Windows（管理员 PowerShell）
New-Item -ItemType SymbolicLink -Path "$env:USERPROFILE\.claude\commands\api-test-cases.md" -Target "path\to\commands\api-test-cases.md"
```

## 自定义 Skills 格式

每个 Skill 是一个 Markdown 文件，放在 `.claude/commands/` 目录下：

```
.claude/commands/
├── skill-name.md       # 用户级命令，通过 /user:skill-name 调用
└── another-skill.md
```

文件格式：
```markdown
---
description: 简短描述
argument-hint: <参数提示>
allowed-tools: [Read, Write, Edit]
model: opus
---

你的 prompt 内容...
```

- `$ARGUMENTS` 会被替换为用户输入的参数
- `!`command`` 会执行 shell 命令并将输出插入 prompt
