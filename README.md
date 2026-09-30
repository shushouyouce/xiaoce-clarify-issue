# 霄策·问题消解分析

把一个模糊议题，逐步拆成明确的问题、可信的解释、可验证的群体假设，以及有证据边界的选题命题。

`xiaoce-clarify-issue` 是一个中文 Agent Skill，适合分析社会话题、商业问题、产品营销议题和争议观点。它先检查问题是否成立，再决定需要走多远：只想理解就停在解释，需要群体洞察或内容选题时再继续。

## 它能帮你做什么

| 你的需要 | 技能的工作 | 交付结果 |
| --- | --- | --- |
| 把事情搞清楚 | 澄清概念、检查前提、区分事实与推断 | 真正的问题、证据边界、竞争解释 |
| 理解某一群体 | 按共同处境、约束、损失和期待分析 | 群体假设、内部差异、表达缺口 |
| 判断是否值得做成选题 | 检查真实问题、认知差与观点依据 | 选题命题、条件性观点、后续问题链 |

例如，“员工不用 AI，是不是因为懒？”会先被拆开：什么算“用 AI”、具体哪些任务、公司是否提供工具与培训、使用成本和收益由谁承担。模型需要比较不同解释，不能直接把“懒”当作结论。

**这个技能只交付分析材料。** 不负责生成文章正文、视频逐字稿、成品文案、标题或开头钩子，也不承诺播放量或转化效果。分析完成后，可以把底稿交给你自己的创作流程。

## 快速安装

这是由 Markdown 与 YAML 文件组成的技能，不需要安装 Python、Node.js 或额外依赖。你需要一个支持本地 Agent Skills 的 AI 客户端；以下步骤以 Codex 为例。Git 仅在选择命令行安装时需要。

### 方法一：让 Codex 帮你安装

在支持 `skill-installer` 的 Codex 中发送：

```text
$skill-installer 请从 https://github.com/shushouyouce/xiaoce-clarify-issue 安装技能。SKILL.md 位于仓库根目录，技能名为 xiaoce-clarify-issue，请同时安装 agents 和 references 目录。
```

### 方法二：Git 安装

安装到当前用户的技能目录，可在不同项目中使用。

**Windows PowerShell：**

```powershell
New-Item -ItemType Directory -Force -Path "$HOME/.agents/skills" | Out-Null
git clone https://github.com/shushouyouce/xiaoce-clarify-issue.git "$HOME/.agents/skills/xiaoce-clarify-issue"
```

**macOS / Linux：**

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/shushouyouce/xiaoce-clarify-issue.git ~/.agents/skills/xiaoce-clarify-issue
```

如果只希望在某个项目中使用，也可以把整个技能目录放到该项目的 `.agents/skills/xiaoce-clarify-issue/` 下。不要重复安装到多个扫描目录，以免出现同名条目。

### 方法三：下载 ZIP，手动安装

1. 点击本仓库页面的 **Code → Download ZIP**。
2. 解压后，将文件夹重命名为 `xiaoce-clarify-issue`。
3. 将整个文件夹放进你的用户目录下的 `.agents/skills/`。
4. 确认最终路径为 `~/.agents/skills/xiaoce-clarify-issue/SKILL.md`，没有多套一层文件夹，并保留 `agents/` 和 `references/`。

Windows 中，`~` 对应你的用户文件夹，通常为 `C:\Users\你的用户名`。

Codex 会检测技能变化；如果没有出现，请重启客户端或开启新会话。安装位置和发现机制参见 [OpenAI 官方技能文档](https://learn.chatgpt.com/docs/build-skills)。其他支持 Agent Skills 的客户端可使用同一套技能文件，但安装路径与调用方式请以对应客户端文档为准；本仓库未逐一验证其他客户端。

## 怎么使用

在 Codex 中明确提及 `$xiaoce-clarify-issue`，然后提供议题与用途。最好附上原始说法、发生背景、涉及人群、时间范围，以及你已有的材料。

### 1. 只想把事情搞清楚

```text
$xiaoce-clarify-issue
有人说“员工不用 AI 是因为懒”。请检查这个问题的前提和概念，
比较可能的解释，区分事实、推断和未知。我的用途只是理解问题。
背景：一家 20 人的服务企业，已提供工具，但尚未记录任务使用情况。
```

### 2. 需要群体洞察

```text
$xiaoce-clarify-issue
我想理解“买过很多课程但很少实践”的人。
请基于我随后提供的访谈和评论，划分共同处境与内部差异，
找出表达缺口。材料不够的地方只列待验证假设，不替整个群体发言。
```

### 3. 判断内容选题是否成立

```text
$xiaoce-clarify-issue
议题：小企业老板为什么觉得 AI 很重要，却迟迟不推动落地？
用途：判断是否值得持续做成一个内容系列。
请先分析问题，再判断目标群体、选题资格、观点边界和后续问题链。
我还没有访谈数据；请标明假设，不写文章、标题或脚本。
```

## 工作方式

技能按需经过四道闸门：

1. **问题是否成立**：拆关键词、检查前提，区分定义、事实、因果、预测、价值、决策、冲突与行动问题。
2. **解释是否可信**：建立证据账本，选择必要的学科镜头，比较主解释与替代解释。
3. **是否存在真实群体问题**：分析共同经验、认同、差异与表达缺口，同时检查廉价迎合风险。
4. **是否具备选题资格**：判断观点能否成立，以及它能否连接作者可持续解释的问题链。

四道闸门不是每次都要填满的模板。前提已被澄清、证据不足，或者已满足你的用途时，就应停止。

## 你会得到什么

输出会随任务调整，通常包括：

- 真正的问题：原句、大白话改写、主次问题。
- 我们知道到哪里：事实、推断、假设、未知与证据边界。
- 竞争解释：机制、成立条件、反例，以及能区分解释的证据。
- 处理结果：已消解、已解释、条件性成立、待验证、需要决策等。
- 可选附录：群体地图、选题命题和后续问题链。

涉及当前事实时，核验能力取决于你所用客户端是否具备联网或资料检索工具。技能本身不附带搜索服务；无法核验时，应明确降低结论确定性。

## 目录说明

```text
xiaoce-clarify-issue/
├── SKILL.md                         # 技能入口、四道闸门与停止条件
├── agents/
│   └── openai.yaml                  # 显示名称、简介与默认调用提示
├── references/
│   ├── discipline-lenses.md         # 学科镜头的选择与使用边界
│   ├── group-recognition.md         # 群体、认同与廉价迎合检查
│   └── topic-continuity.md          # 选题资格与作者连续性
├── README.md                        # 介绍、安装与使用说明
└── CHANGELOG.md                     # 发布记录
```

## 更新与常见问题

**通过 Git 安装后如何更新？**

```bash
git -C ~/.agents/skills/xiaoce-clarify-issue pull --ff-only
```

Windows PowerShell 使用：

```powershell
git -C "$HOME/.agents/skills/xiaoce-clarify-issue" pull --ff-only
```

若你修改过本地文件，请先保存自己的修改再处理更新冲突。通过 ZIP 安装的用户，可以重新下载并备份旧目录后替换。

**安装后找不到技能？** 检查 `SKILL.md` 的位置、文件名大小写、是否保留完整目录，以及是否存在同名重复安装。再重启客户端，尝试明确输入技能名。

**为什么它不直接给我一个确定结论？** 当关键材料不足时，交付待验证假设与验证方向是预期行为。

**为什么它不写正文？** 本技能的职责到分析底稿为止。需要成品内容时，请在后续独立的创作任务中使用这份底稿。

**如何反馈？** 请在 [Issues](https://github.com/shushouyouce/xiaoce-clarify-issue/issues) 中提供输入示例、预期结果与实际问题，并移除私人或客户敏感信息。

## 作者

[霄策 / shushouyouce](https://github.com/shushouyouce)
