# oralenglish-skill

专四（TEM-4）英语口语思辨陪练 Skill。纯文本对话式陪练，**不支持网页抓取、PDF、图形界面**。

## 项目解决什么问题

备考 TEM-4 口语时，很多人知道要"多开口说"，但缺少一套有引导、有反馈的训练方式：

- 面对一个观点性问题，不知道从哪切入、怎么组织理由；
- 说出来的英语带有明显中式痕迹（中文直译语序、中式搭配、母语负迁移），但没人指出来；
- 自己练没有节奏，说一句就结束，缺乏递进。

本项目用 **"话题 → 参考句型 → 口头作答 → 转写 + 优化 + 点评 → 继续/重答"** 的闭环，解决"没话题可练、练了没人改、改了没进步"三个问题。

## 主要功能

1. **思辨话题引导**：每轮抛出一个具体可辩论的英文 Topic。
2. **参考句型支架**：Topic 后附一正一反两句纯英文句型，给作答思路。
3. **原句转写**：原样保留你口述的英文，不润色、不补口误。
4. **优化句**：生成 1 版适配专四口语的改写，优先修正中式英语，改动的核心内容加粗标出。
5. **简短点评**：点名本次的中式英语问题，并说明句式、用词地道度。
6. **循环推进**：反馈后提供【继续】（同话题深度追问）和【重新回答】（不换话题重新作答）两个选项，支持逐轮迭代。

## 目录结构

```
oralenglish-skill/
├── SKILL.md            # 技能主体：流程规则与中式英语修正要点
└── agents/
    └── openai.yaml     # Agent 配置（模型、指令、工具声明）
```

## 安装方法

本 Skill 不含可执行脚本，也不依赖第三方包，安装即"把它放到 Agent 能加载到的地方"。

1. 将 `oralenglish-skill/` 目录（含 `SKILL.md` 与 `agents/openai.yaml`）放入支持该 Skill 格式的 Agent 的 Skill 加载目录。
   - 例如支持 `agents/openai.yaml` 的 Agent 环境（如 OpenAI Agents SDK 的 skills 目录），把整个 `oralenglish-skill/` 拷贝进去即可。
2. 可选校验：在装好 `pyyaml` 的 Python 环境中运行官方验证脚本检查结构：

   ```bash
   python <skill-creator>/scripts/quick_validate.py oralenglish-skill/
   # 输出：Skill is valid!
   ```

   > `quick_validate.py` 属于 skill 创建工具集，不包含在本项目内，仅为结构校验用。

## 使用方法

加载后，直接对 Agent 说一句触发语即可开始：

- “帮我练一下专四口语思辨”
- “陪我练口语，出一个话题”
- “专四口语陪练”

训练流程：

1. AI 给出一个英文 Topic + 2 句参考句型（一正一反）。
2. 你口头作答（可直接语音转文字输入）。
3. AI 输出三件套反馈：【我的原句】【优化句】【简短点评】。
4. 选择【继续】（同一话题深度追问，开启新一轮作答）或【重新回答】（不换话题，重新作答后再次优化点评，直到你选【继续】）。

## 输入输出示例

**输入（触发后 AI 给出）：**

```
📌 Topic: Should college students take a gap year before starting their studies?

💡 Reference:
✅ For: A gap year lets students explore the world before they commit to a major.
❌ Against: Delaying college may make it harder for students to stay motivated.
```

**你的作答（输入）：**

```
I think gap year is good because students can relax and find what they really want to do.
```

**AI 反馈（输出）：**

```
【我的原句】
I think gap year is good because students can relax and find what they really want to do.

【优化句】
I think **taking a gap year is a good idea**, because it gives students time to relax **and figure out what they really want to do**.

【简短点评】
1. 中式搭配：英文里不说 "gap year is good"，要说 "taking a gap year is a good idea"。
2. 中式搭配/母语负迁移："find what they want to do" 表意略生硬，口语更常说 "figure out what they want to do"。
3. 句式：主从结构 "because ... and ..." 通顺，逻辑连贯，整体口语化程度较好。

【继续】 / 【重新回答】
```

## License

MIT
