# pstack 插件仓库

这是 [cursor/plugins](https://github.com/cursor/plugins) 的精简 fork，只保留 [pstack](pstack/) 一个插件。用法和技能说明见 [pstack/README.md](pstack/README.md)。

## 安装

Cursor 读 `.cursor-plugin/marketplace.json`，直接使用 `pstack/`。

Claude Code 读 `.claude-plugin/marketplace.json`，安装生成的 `harness/pstack/claude-code/`：

```bash
/plugin marketplace add Leon-An07/plugins-pstack
/plugin install pstack@cursor-plugins
```

## 依赖的外部插件

pstack 的部分步骤会调用 `cursor-team-kit` 插件的技能（如 `/deslop`、`control-ui`、`control-cli`）。本仓库已不包含它，需要时从 [cursor/plugins](https://github.com/cursor/plugins/tree/main/cursor-team-kit) 另行安装。

## 目录

| 路径 | 作用 |
|:-----|:-----|
| `pstack/` | 插件源码：技能、agents、文档 |
| `harness/pstack/` | 由 `pstack/` 生成的 Claude Code 版本，不要手改 |
| `schemas/` | 市场索引和 `plugin.json` 的 JSON Schema |
| `scripts/` | 校验与生成脚本 |

## 修改 pstack 之后

```bash
npm install --no-save ajv ajv-formats
node scripts/validate-plugins.mjs
node scripts/generate-pstack-harness-trees.mjs   # 重新生成 harness/pstack，并一起提交
node scripts/check-pstack-docs.mjs
node --test pstack/skills/*/scripts/test/*.test.mjs
```

CI（`.github/workflows/validate-plugins.yml`）会在 PR 上运行 `validate-plugins`、生成副本检查（`--check`）和脚本测试，生成副本过期时会失败。
