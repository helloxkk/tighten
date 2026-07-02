# Tighten

一个给 AI 编码代理（Claude Code / Codex / ZCode 等）用的 skill：识别并删除技术文档里的废话、重复、过度解释，顺手收紧中文措辞与排版。

适合 README、AGENTS.md、API 文档、注释这类**被带着明确目的快速扫读**的文档（读者是人或 AI 代理）。废话降低信噪比、抬高定位关键内容的成本。

## 它做什么

- **结构层**：按六类废话逐类排查——自我介绍式、画蛇添足、元废话、重复、重复罗列、过度解释。
- **语言层**：中文留白、直角引号、易错词（登录/登陆、截至/截止、阈值/阀值）、数量表达逻辑（"缩小 3 倍" → "1/3"）。主要面向中文文档；英文文档只做结构层。
- **绕过代码**：只作用于自然语言正文，不碰代码字面量、JSON 键名、URL、API 路径、字段名。

## 设计哲学

借鉴 [tw93/Waza](https://github.com/tw93/Waza) 的 `write` skill 的结构设计：

- **smell 目录，不是查找替换清单**——命中但语境里读着自然的，保留。
- **过度删减 = 失败**，等于不删。
- **作者的声音优先**，规则是默认值不是法律。
- Hard Rules / Pre-flight / Gotchas / Output 契约 / 防膨胀维护规则。

## 安装

仓库根目录就是 skill 本体（含 `SKILL.md`）。clone 后整个目录放进对应代理的 skills 目录，加载器按目录名 `tighten` 识别。

### Claude Code / 通用（`.agents/skills/`）

```bash
git clone https://github.com/helloxkk/tighten.git ~/.agents/skills/tighten
```

### ZCode / 其他支持 skill 的代理

把 clone 下来的 `tighten/` 目录放到对应代理的 skills 目录即可。

## 触发示例

skill 装好后，在支持 skill 的代理里直接说人话即可触发：

- 「精简下这个 README」
- 「检查这个文档有没有废话」
- 「我刚写完 AGENTS.md，顺手收紧下措辞」
- "trim this doc" / "declutter these release notes"

## 文件

```
tighten/
├── SKILL.md      # skill 本体（frontmatter + 全部规则）
├── README.md
├── LICENSE
└── .gitignore
```

## License

MIT
