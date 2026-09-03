# aeps-public-marketplace

Claude Code marketplace 目录。把这一个仓库加进 Claude Code,即可在本地一键安装本目录列出的所有 plugin。

## 安装

在 Claude Code 中执行:

```
/plugin marketplace add https://github.com/zhigangliu-bot/aeps-public-marketplace
```

然后用 `/plugin install <name>` 安装 marketplace 中的任意 plugin。

## 当前可装 plugins

| 名称 | 版本 | 一句话功能 |
|---|---|---|
| `aeps-llm-wiki-plugin` | 0.5.5 | 把 Karpathy LLM Wiki 模式 + OKF v0.2 + Obsidian 直读前端三种范式合成一处。在自己的研究项目里跑 `/aeps-llm-wiki-init`,即可得到 OKF 兼容、Karpathy 启发、Obsidian 可直读的知识库;LLM 写、Obsidian 读、plugin 管一致性。 |

完整描述见 [.claude-plugin/marketplace.json](.claude-plugin/marketplace.json)。

## 扩展位 — 如何向 marketplace 追加新 plugin

本 marketplace 是为多 plugin 设计的。后续若需要新增 plugin,步骤如下:

1. 在 GitHub 上准备好 plugin 本体仓库(可以是 `github` source,也可以是 `git` / `url` / `directory` 等 marketplace schema 支持的其他 source)。
2. 编辑 [.claude-plugin/marketplace.json](.claude-plugin/marketplace.json),向 `plugins[]` 数组追加一项。schema 详见 https://json.schemastore.org/claude-code-marketplace.json 。
3. 字段含义:
   - `name`:plugin 的唯一标识,需与 plugin 本体 `plugin.json` 的 `name` 一致。
   - `source.source`:来源类型,常用 `github`(指向 GitHub repo),其他可选 `git` / `url` / `directory` / `file`。
   - `source.repo`:仅 `source.source == "github"` 时需要,格式 `<owner>/<repo>`。
   - `description`:建议从 plugin 本体 `plugin.json` 的 `description` 原样复制,保持单一事实源(Single Source of Truth)。
   - `version`:与 plugin 本体 `plugin.json` 的 `version` 一致,marketplace 升级时同步。
4. 提交并 push,marketplace 升级即生效(用户无需重装,只需在 Claude Code 里刷新 marketplace 列表)。

### 字段参考

完整 schema 与字段说明请参考 Claude Code 官方文档与 schema 文件:

- schema:`https://json.schemastore.org/claude-code-marketplace.json`
- Claude Code 官方文档:https://docs.claude.com/en/docs/claude-code/plugins

## 维护

- 本仓库只承担"目录"角色,plugin 本体的代码 / tag / release 请到各 plugin 仓库处理。
- marketplace 升级流程:plugin repo 打新 tag → 改本仓库 `marketplace.json` 的 `version` 与 `description` → commit push。

## License

各 plugin 的 license 以其本体仓库为准;本目录文件的 license 见 [LICENSE](LICENSE)。
