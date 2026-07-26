# 文献综述生成 Skill（awesome-literature-review）

一个 [Claude Code](https://docs.claude.com/en/docs/claude-code) 的 Skill，用来分四部分生成一篇结构完整的文献综述：**研究背景与目的 → 文献梳理与分析 → 研究现状总结与评述 → 参考文献**。

设计上把人工干预都集中在动笔之前——先对齐题目、文献来源、输出格式，文献清单经用户核验，然后一口气写完整篇初稿，不再一段段停下来确认。

## 特点

- **文献必须真**：写入正文的每一篇文献都要有可核验来源。用户自己粘贴的照用；让 AI 联网搜索的必须带出处链接、先给用户核对，严防凭记忆编造标题、作者、年份。
- **前期对齐、一次成稿**：开场用交互式提问把题目、文献来源、输出格式一次问清，文献清单确认后，四部分连着写完整篇再交付。
- **能用你的现成材料**：手里有开题报告、初稿、任务书或导出的参考文献列表，直接发进去——读完先抽出题目、方向、文献清单，**只问缺的那几项**，不用重新走一遍问答。多份材料还会交叉核对，把矛盾（比如开题报告写"近五年"但初稿引了十年前的文献）单独列出来让你拍板。
- **压 AI 腔**：内置《行文要求》，段落叙述、长短错开、少用程式化连接词、全角标点，尽量淡化翻译腔和套路感。
- **引用格式有细则**：参考文献默认国标 GB/T 7714-2015，文献类型标识、三名以上作者截断、DOI 处理、缺项省略规则都写进了 `references/citation-format.md`，不靠模型即兴发挥。
- **交付前两轮自查**：一轮查文风（有没有冒出列表体、排比、"综上所述"、半角标点），一轮查内容完整性（文献用全了没、指出的空白够不够具体、范围表述和清单对不对得上）。
- **可选配图**：文献较多、主题分支清晰时，可以调 **Image2** 生成文献分类框架图（把正文的主题结构可视化）或研究演进时间线图。图里内容全部来自已定稿正文，不新增文献和结论，出图后逐框核对。做系统综述的另附 PRISMA 2020 筛选流程图提示词。
- **多种输出格式**：对话 / Markdown / Word / LaTeX。Word 有明确格式规格（A4、边距、字体字号、行距、内置标题样式、三线表、表题在上图题在下）并在生成后验证文件有效性；选 LaTeX 时会去搜目标期刊的真实官方模板并让用户确认，找不到才降级到通用模板并如实告知。
- **抗遗忘**：提示词正文、引用细则、完整性清单、配图提示词分成四份独立 reference，在各自需要的节点就近读进上下文，缓解长流程里的文风漂移和上下文压缩丢失。

## 安装

这是一个标准的 Agent Skill 仓库，`SKILL.md` 就在根目录。

**从 GitHub 引入**（网页端 Agent / ClawsGO 等）：把仓库地址填进"从 GitHub 引入"，拉取后点安装即可。

```
https://github.com/yzbbds520/awesome-literature-review
```

**手动放入项目**：clone 本仓库后，把 `SKILL.md` 和 `references/` 一起拷进你项目的 `.claude/skills/awesome-literature-review/` 下（或用户级 `~/.claude/skills/awesome-literature-review/`），Claude Code 会自动识别。

```
.claude/skills/awesome-literature-review/
├── SKILL.md
└── references/
    ├── prompts.md
    ├── citation-format.md
    ├── completeness-checklist.md
    └── diagrams.md
```

## 触发

在 Agent 里说「帮我写文献综述」「写一篇 XXX 的国内外研究现状」「literature review」之类即可触发。

## 目录结构

```
SKILL.md                              # 主流程:三条铁律、交互总则、Phase 0~3、Word/LaTeX 流程、检查清单
references/prompts.md                 # 四部分提示词正文 +《行文要求》 → 动笔前必读
references/citation-format.md         # GB/T 7714-2015 引用格式细则 → 写参考文献前必读
references/completeness-checklist.md  # 内容完整性清单 → 交付前必读
references/diagrams.md                # Image2 配图提示词(框架图/时间线/PRISMA) → 决定出图时读
```

reference 拆成独立文件是为了在各自需要的节点就近 `Read` 一次，而不是一开始全灌进上下文——长流程里更抗遗忘。

## License

[MIT](./LICENSE)
