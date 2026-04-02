# wechat-mp-reader

OpenClaw skill for reading WeChat Official Account articles and account timelines.

## Included files

- `SKILL.md`
- `CURRENT_TASK.md`
- `references/`
- `scripts/`

## Main capabilities

- extract full article content from a WeChat article URL
- identify the account behind an article
- list recent articles from that account
- search candidate accounts by name (with a valid MP backend session)
- manage MP backend session state, including QR login flow
- output structured JSON and cleaned markdown

## Recommended entry

Use an article URL first whenever possible.

## See also

- `references/usage.md`
- `references/design.md`
