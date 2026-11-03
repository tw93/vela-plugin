# Vela plugin

Vela helps you grow a product the way each community expects. This repository holds the Vela plugin for your agent: the remote MCP configuration and the workflow skills that call Vela's tools. You need a Vela account to use it.

This repository is a read-only mirror, published from Vela's source repository. It contains only the MCP configuration and the skill files. Vela's rule cards, data and server code are not included. Issues and pull requests are closed here.

## Install in Claude Code

```
/plugin marketplace add tw93/vela-plugin
/plugin install vela@vela
```

The plugin adds the remote MCP server `vela` (`https://vela.how/mcp`) and all skills. The first time your agent calls a Vela tool, you sign in to Vela in the browser.

## Install in Codex or Cursor

1. Copy the folders you want from `skills/<name>/` into `.agents/skills/` (Codex) or `.cursor/skills/` (Cursor).
2. Add Vela as a remote MCP server in your client's settings, using the URL `https://vela.how/mcp`. If your client cannot sign in through the browser, create an API key in the Vela workspace and send it as a `Bearer` token in the `Authorization` header.

The skills only work together with the MCP server: they tell your agent which Vela tools to call and in what order. Vela never posts for you; you paste the final text into the community yourself.

## License

Proprietary. See `LICENSE`.

---

# Vela 插件

Vela 帮你按各社区的规矩做增长。本仓库是 Vela 给 agent 用的插件：远程 MCP 配置，加上调用 Vela 工具的工作流 skills。使用前需要有 Vela 账户。

本仓库是只读镜像，由 Vela 的源码仓库发布，只含 MCP 配置与 skill 文件，不含 Vela 的规则卡、数据与服务端代码。这里不收 issue 与 pull request。

## 在 Claude Code 中安装

```
/plugin marketplace add tw93/vela-plugin
/plugin install vela@vela
```

插件会加入远程 MCP 服务 `vela`（`https://vela.how/mcp`）与全部 skills。agent 第一次调用 Vela 工具时，你在浏览器里登录 Vela。

## 在 Codex 或 Cursor 中安装

1. 把需要的 `skills/<name>/` 目录拷到 `.agents/skills/`（Codex）或 `.cursor/skills/`（Cursor）。
2. 在客户端设置里把 Vela 加为远程 MCP 服务，地址 `https://vela.how/mcp`。客户端不支持浏览器登录时，在 Vela 工作台创建 API key，以 `Bearer` 令牌放进 `Authorization` 请求头。

skills 要和 MCP 服务一起用：它们告诉 agent 该调用哪些 Vela 工具、按什么顺序。Vela 不会替你发帖，最终文本由你自己粘贴到社区。

## 许可

专有许可，见 `LICENSE`。
