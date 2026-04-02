# wechat-mp-reader

一个用于读取微信公众号文章与公众号时间线的 OpenClaw Skill。

## 仓库内容

当前仓库仅包含这个 skill 本身所需的核心文件：

- `SKILL.md`
- `CURRENT_TASK.md`
- `references/`
- `scripts/`

## 主要能力

- 根据微信公众号**文章 URL**提取全文
- 根据文章识别其所属公众号
- 拉取该公众号最近发布的文章列表
- 根据公众号名称搜索候选账号（需有效的 MP 后台 session）
- 管理 MP 后台 session，包括二维码登录流程
- 输出结构化 JSON 与清理后的 markdown 正文

## 推荐入口

只要可以，优先使用**文章 URL**作为输入。

这是当前最稳定的调用方式：

1. 提供一篇公众号文章链接
2. 提取文章正文
3. 识别公众号
4. 拉取该公众号最近文章

## 关于 MP session

这里的 **MP** 指的是 **微信公众平台后台**（`mp.weixin.qq.com`）。

这个 skill 里有两类能力：

1. **公开文章页能力**：例如根据文章 URL 提取正文、标题、发布时间等，很多时候可以直接通过文章页完成。
2. **公众号后台能力**：例如按公众号名称搜索账号、按账号拉取最近文章列表，这类能力依赖有效的 **MP 后台 session**。

这里的 **session**，可以理解为 skill 当前持有的一份“已登录微信公众号后台”的会话状态（通常由 cookie / token 等凭证组成）。

它主要决定 skill 能不能正常访问微信公众平台后台接口，从而影响：

- 公众号名称搜索
- 按账号拉取最近文章列表
- 更稳定的账号级查询

如果你已经有一篇公开文章 URL，正文提取很多时候仍然可以工作；但一旦需要“从账号维度继续向下查”，就通常需要有效的 MP session。

## 文档入口

- 使用说明：`references/usage.md`
- 设计说明：`references/design.md`
- 当前 handoff：`CURRENT_TASK.md`

## 命令行示例

```bash
python3 scripts/wechat_mp_reader.py session check
python3 scripts/wechat_mp_reader.py article "https://mp.weixin.qq.com/s/xxxx" --with-account-articles --list-count 5
```

## 自然语言调用示例

你也可以直接通过 agent 用自然语言触发这个 skill，例如：

- 帮我提取这篇公众号文章全文：`文章链接`
- 帮我读取这篇文章，并列出这个号最近 5 篇
- 帮我检查 wechat-mp-reader 的 session 是否有效
- 帮我启动微信后台二维码登录

## 说明

- URL-first 是当前最可靠的路径
- 遇到非 canonical 微信文章页时，会回退到本地 Playwright WebKit
- 公众号名称搜索依赖有效的 MP 后台 session
