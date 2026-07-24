# 文献综述生成 Skill（literature-review）

一个 [Claude Code](https://docs.claude.com/en/docs/claude-code) 的 Skill，用来分四部分生成一篇结构完整的文献综述：**研究背景与目的 → 文献梳理与分析 → 研究现状总结与评述 → 参考文献**。

设计上把人工干预都集中在动笔之前——先对齐题目、文献来源、输出格式，文献清单经用户核验，然后一口气写完整篇初稿，不再一段段停下来确认。

## 特点

- **文献必须真**：写入正文的每一篇文献都要有可核验来源。用户自己粘贴的照用；让 AI 联网搜索的必须带出处链接、先给用户核对，严防凭记忆编造标题、作者、年份。
- **前期对齐、一次成稿**：开场用交互式提问把题目、文献来源、输出格式一次问清，文献清单确认后，四部分连着写完整篇再交付。
- **压 AI 腔**：内置《行文要求》，段落叙述、长短错开、少用程式化连接词、全角标点，尽量淡化翻译腔和套路感。
- **多种输出格式**：对话 / Markdown / Word / LaTeX。选 LaTeX 时会去搜目标期刊的真实官方模板并让用户确认，找不到才降级到通用模板并如实告知。
- **抗遗忘**：各部分提示词正文和《行文要求》单独存在 `references/prompts.md`，动笔前重新读进上下文，缓解长流程里的文风漂移和上下文压缩丢失。

## 安装

这个仓库本身就是一个 Claude Code plugin marketplace。在 Claude Code 里执行：

```
/plugin marketplace add yzbbds520/literature-review-skill
/plugin install literature-review@yzbbds520-skills
```

装好后重启 Claude Code 即可。

如果你不想走 plugin 方式，也可以直接把 skill 目录拷进自己项目：clone 本仓库后，把 `plugins/literature-review/skills/literature-review/` 整个目录复制到你项目的 `.claude/skills/` 下（或用户级 `~/.claude/skills/`），Claude Code 会自动识别。

## 触发

在 Claude Code 里说「帮我写文献综述」「写一篇 XXX 的国内外研究现状」「literature review」之类即可触发。

## 目录结构

```
.claude-plugin/marketplace.json          # 市场目录
plugins/literature-review/
├── .claude-plugin/plugin.json           # 插件清单
└── skills/literature-review/
    ├── SKILL.md                         # 主流程:三条铁律、交互总则、Phase 0~3、LaTeX 流程、检查清单
    └── references/prompts.md            # 四部分提示词正文 +《行文要求》,动笔前按需加载
```

## License

[MIT](./LICENSE)
