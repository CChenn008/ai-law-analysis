# AI 法律解读技能

`ai-law-analysis` 是一个基于 Agent Skills 目录格式编写、主要在 Codex 中开发和验证的可复用技能，用于系统解读人工智能法律、法规、草案、监管指南、行为准则和政策文件，并将规则转化为适用性判断、角色与监管分类、合规义务、业务影响和产品改造要求。其核心 `SKILL.md`、参考文件和模板也可以由支持 Agent Skills 格式的其他智能体使用。

## 主要能力

- 核验法律文件身份、效力、版本、生效与适用时间；
- 处理外文网页和文件下载链接，保留官方原文并在完整分析前形成全量中文译文；
- 按目标法自身结构判断适用范围、法定主体、角色和监管类别；
- 将正文、附件和清单拆解为可追溯的原子化规则；
- 生成法律解读、法务规则底表、业务合规指引和业务自查表；
- 将适用义务映射为产品、研发、运营、合同和证据要求；
- 使用跨法域测试和质量检查降低错误套用其他法域概念的风险。

## 目录结构

```text
ai-law-analysis/
├── SKILL.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── foreign-source-and-translation.md
│   └── ...
├── assets/
│   └── AI法律合规工作簿模板.xlsx
├── LICENSE
├── NOTICE.md
└── CHANGELOG.md
```

## 兼容平台与安装方法

下载或克隆本仓库后，请始终保留完整的 `ai-law-analysis` 文件夹。不同平台的安装位置如下。

### Codex

复制到个人 Codex 技能目录：

```text
~/.codex/skills/ai-law-analysis
```

Windows 默认用户目录的写法通常是：

```text
%USERPROFILE%\.codex\skills\ai-law-analysis
```

然后在任务中调用：

```text
$ai-law-analysis
```

### Claude Code

个人级安装：

```text
~/.claude/skills/ai-law-analysis
```

也可以安装到具体项目：

```text
<项目根目录>/.claude/skills/ai-law-analysis
```

安装后，Claude Code 会根据 `SKILL.md` 的名称和描述发现相关任务。参见 [Anthropic Agent Skills 文档](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview)。

### GitHub Copilot

个人级安装：

```text
~/.copilot/skills/ai-law-analysis
```

也可以安装到具体仓库：

```text
<仓库根目录>/.github/skills/ai-law-analysis
```

GitHub Copilot 还支持 `.agents/skills/` 等兼容位置。参见 [GitHub Copilot Agent Skills 文档](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/add-skills)。

### Gemini CLI

安装到项目级 Agent Skills 目录：

```text
<项目根目录>/.agents/skills/ai-law-analysis
```

启动 Gemini CLI 后，可以使用 `/skills` 检查是否已经发现该技能。参见 [Google Gemini CLI Agent Skills 指南](https://codelabs.developers.google.com/gemini-cli/how-to-create-agent-skills-for-gemini-cli)。

## 兼容性说明

- 本技能目前主要在 Codex 中开发和验证；其他平台的上述路径依据其 Agent Skills 文档列出，不代表所有功能均已完成逐平台回归测试；
- `agents/openai.yaml` 是 Codex/OpenAI 的界面元数据，其他平台可以忽略；核心工作流位于 `SKILL.md`；
- 部分任务需要按 `SKILL.md` 的路由读取 `references/`，创建多工作表成果时还可能使用 `assets/` 中的模板；
- PDF、OCR、电子表格、联网检索和文件生成效果取决于目标平台实际提供的工具、权限和运行环境；
- 对不支持 Agent Skills 自动发现机制的智能体，可以把 `SKILL.md` 作为项目指令，并按需提供 `references/` 和 `assets/`，但触发和文件路由可能需要人工完成。

## 外文法律文件处理

输入为非中文法律文件、外文网页或网页中的文件下载链接时，本技能会核验官方详情页和实际文件，保存原始控制版本，提取或OCR全文，并建立翻译覆盖记录。完整分析非中文法律时，默认先形成并单独交付包含正文、定义、附件、表格和脚注的全量中文译文，再开展法律分析。

登录页、验证码页、失败下载页、损坏文件或缺失附件不得被视为已经读取全文。无法取得必要材料时，本技能会披露证据缺口和有限结论，不会绕过访问控制。详细流程见 [外文来源获取与全量翻译](references/foreign-source-and-translation.md)。

## 法律与来源边界

本技能提供的是法律研究、合规分析和交付物设计工作流，不构成针对任何主体、产品或事项的法律意见，也不替代律师、法务人员、监管机关或依法必须进行的正式评估。

使用者应当自行核验：

- 适用法域及最新官方控制文本；
- 文件是否正式通过、公布、生效或开始适用；
- 法律、指南、标准、草案和内部建议的效力差异；
- 具体企业、产品、模型、功能和业务场景事实；
- 自动生成内容、译文、引用和附件是否准确、完整。

仓库不因提及、引用或链接第三方法律文件、官方材料、译文、标准、模板或其他内容而取得或重新授予其权利。相关材料适用其自身的权利声明和法律规则，详见 [NOTICE.md](NOTICE.md)。

## 许可证

除非文件中另有明确说明，本仓库中的原创内容，包括 `SKILL.md`、`agents/`、`references/` 和 `assets/` 中的技能模板，依据 [MIT License](LICENSE) 开源。

Copyright (c) 2026 ChenYu

