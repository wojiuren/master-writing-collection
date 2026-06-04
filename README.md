# 大师写作合集：中文 AI 写文模块库

这是一个面向中文小说创作者的 AI 写作辅助模块库。它按写作流程组织，不按书目、作者或来源组织。

## 当前版本

- 发布版本：`v0.1.2`
- 版本文件见 [VERSION](VERSION)

## 安装到写作项目

发布版不需要额外安装。最简单的用法就是：

1. 下载 GitHub 发布页里的压缩包。
2. 直接解压到你的写作项目文件夹里。
3. 保持 `agents/`、`modules/`、`web-copy/` 这三个目录的相对位置不要拆散。

推荐目录结构：

```text
你的写作项目/
├── master-writing-collection/
│   ├── agents/
│   ├── modules/
│   └── web-copy/
├── 成稿/
├── 设定/
└── 章节草稿/
```

如果你只是想把发布版放进现有工程里，直接解压进去即可，不需要再跑安装命令。

## 适合谁

- 使用 DeepSeek、Kimi、豆包、通义、ChatGPT 等网页端工具写中文小说的人。
- 需要构思、人物关系、情节推进、悬念伏笔、章节节奏、草稿修订、语言润色的人。
- 希望按模块复制提示词，而不是一次性塞给模型一大堆资料的人。

## 使用方式

### 网页端版本

如果你只是网页端用户，不需要理解 Skills，也不需要 API：

1. 直接进入 [web-copy/](web-copy/)。
2. 选择 `写作前`、`写作中`、`写作后` 对应文件。
3. 复制提示词，把 `{变量}` 换成你的正文、设定或目标。
4. 粘贴到 DeepSeek、Kimi、豆包、通义、ChatGPT 等网页端工具里使用。

如果你想看每个提示词背后的方法说明，再进入 [INDEX.md](INDEX.md) 和 [modules/](modules/)。

### Agent / 技能版

如果你使用支持本地技能或本地知识目录的 agent，把整个发布版文件夹保留在你的写作工作区里即可。

推荐做法：

1. 把发布包解压到写作项目目录中。
2. 让 agent 从 [agents/SKILL.md](agents/SKILL.md) 作为入口。
3. 先让它读 `agents/skill-vector-table.md` 做粗分流。
4. 再按需读取 `agents/references/request-router.md` 和 `modules/` 里的对应模块。

典型调用方式可以是：

```text
使用 $master-writing-collection，帮我诊断这一章为什么太平。
```

或者在不支持自动发现 skill 名称时，直接说明路径：

```text
请读取 ./master-writing-collection/agents/SKILL.md，并按它的路由规则帮我处理这段小说。
```

### API 集成版

如果你走的是 API 或自建工作流，可以把这个发布版当作一个本地 skill 包来用。

最稳的接法是：

1. 把发布包解压到与你的正文同一个工作区。
2. 先加载 [agents/SKILL.md](agents/SKILL.md)。
3. 再加载 `agents/skill-vector-table.md` 和 `agents/references/request-router.md`。
4. 最后只按需加载 1-2 个相关模块，不要整库全塞进上下文。

如果你的 API 工作流不支持动态读本地文件，也可以退一步：

- 直接把 `web-copy/*.md` 当成可复制提示词模板使用。
- 或者手动注入 `agents/SKILL.md` 加一个目标模块，例如 `modules/02-drafting/02-scene-craft.md`。

## 三层结构

- 第一层：写作前、写作中、写作后。
- 第二层：23 个任务模块，完整名称和入口见 [INDEX.md](INDEX.md)。
- 第三层：具体问题，例如“中段塌了”“人物动机不可信”“对话太白”“结尾没有钩子”。

## 公开版边界

这个仓库只保留原创整理后的写作模块和提示词，不包含原始电子书、逐章笔记、私人小说项目资料或来源索引。

公开边界说明见 [PUBLICATION_BOUNDARY.md](PUBLICATION_BOUNDARY.md)。

## 许可证

仓库内文档默认使用 [CC BY 4.0](LICENSE) 共享。后续如果加入脚本或网页代码，建议为代码部分单独声明许可证。

如果你只想润色几句话，不需要启动复杂模块，直接使用 [语言风格润色](modules/03-revision/05-line-style-polish.md)。

如果你不确定该用哪个模块，网页端用户先用 [web-copy/00-router.md](web-copy/00-router.md)，想看方法说明再用 [modules/00-router.md](modules/00-router.md)。

## Token 参考

本仓库内容为中文 Markdown。以下为模块大小和 token 消耗估算（基于 Claude 系列模型，中文约 2-3 bytes/token）：

| 项目 | 大小 | 预估 tokens |
|------|------|------------|
| 每模块平均 | 4-6 KB | 2-3K tokens |
| Agent 入口文件（SKILL.md + 向量表 + 路由表） | 约 9 KB | 4-5K tokens |
| 典型首次加载（agent 入口 + 1-2 模块） | 约 20-30 KB | 12-18K tokens |

Agent 端一次写作辅助请求通常只加载 1-2 个模块，入口文件在后续同一次会话中不再重复加载。

对比早期薄版本（约 2.4 KB/模块），每个模块多消耗约 2-3K tokens，但内容深度显著提升：包含多视角操作法、诊断清单、常见陷阱和可用示例。
