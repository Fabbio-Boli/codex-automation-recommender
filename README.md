# Codex Automation Recommender

**A third-party plugin for OpenAI Codex that reviews a code repository and recommends useful Codex setup improvements.**

It helps you decide whether a project would benefit from clearer `AGENTS.md` instructions, reusable skills, custom agents, hooks, MCP servers, a plugin package, or an existing built-in Codex feature. Recommendations must be tied to evidence in the selected repository and include benefits, trade-offs, requirements, and next steps.

The plugin is an advisor. It does not install tools, edit files, change settings, enable hooks, or connect services. You decide what to apply.

Created and maintained by **Fabbio Boli** as a Codex-focused adaptation. The project rewrites and repackages the original workflow for Codex. It is an independent community project, not an official OpenAI product and not endorsed by OpenAI.

## What it does

When asked to review a project, the skill:

1. Maps the repository's stack and workflows from existing files such as manifests, lockfiles, source imports, documentation, and CI configuration.
2. Checks Codex setup already present in the repository, including `AGENTS.md`, `.agents/skills/`, `.codex/agents/`, project configuration, MCP references, and plugin catalogs.
3. Looks for repeated work, manual checks, recurring mistakes, external context gaps, and safety constraints.
4. Compares those needs with Codex features and suggests only relevant options:
   - **Project instructions:** project-specific conventions and commands in `AGENTS.md`.
   - **Skills:** repeatable workflows, examples, and supporting resources in `.agents/skills/<name>/SKILL.md`.
   - **Custom agents:** focused roles for separate kinds of work, when supported by the current Codex setup.
   - **Hooks:** deterministic actions at supported lifecycle events, only when the current host supports them and the need justifies them.
   - **MCP servers:** connections to external tools or data, with required authentication and permissions called out.
   - **Plugins:** packaging reusable Codex capabilities for sharing, including the distinction between a repository marketplace and public-directory distribution.
   - **Built-in features:** existing Codex capabilities that can solve the need without another dependency.
5. Ranks the strongest opportunities and explains evidence, benefit, trade-off, and suggested setup steps.

It skips categories without evidence and says when the repository does not provide enough information. If a recommendation depends on a current feature, third-party tool, or install command, it should check authoritative documentation when browsing is available; otherwise it labels the detail as unverified.

## How to use it

Install the plugin, open the repository you want Codex to inspect, and invoke the skill by name or use one of these prompts:

```text
$codex-automation-recommender
Review this repository and recommend the most useful Codex setup improvements.
Keep the review read-only and cite the files that support each recommendation.
```

For a focused review:

```text
Use codex-automation-recommender to review only whether this project needs reusable skills.
Show repository evidence, trade-offs, requirements, and setup steps. Do not change files.
```

You can ask it to cover any one category or all categories: project instructions, skills, agents, hooks, MCP servers, plugins, and built-in Codex features. The report follows this shape:

- **Project snapshot:** stack, existing Codex setup, and notable workflows.
- **Best opportunities:** ranked recommendations with evidence, benefit, trade-off, requirements, and a suggested next step.
- **Unknowns:** questions or current feature details that could not be confirmed.
- **Optional next step:** ask whether you want help implementing a recommendation.

The “setup” section is guidance only. To apply an idea, make a separate explicit request and review the proposed changes.

## Install from this GitHub repository

The repository needs to be public for other people to add its marketplace. In a Codex CLI terminal, run:

```sh
codex plugin marketplace add Fabbio-Boli/codex-automation-recommender --sparse .agents/plugins --sparse plugins/codex-automation-recommender
```

Then restart Codex, open the Plugins Directory, select **codex-automation-recommender-marketplace**, and install **Codex Automation Recommender**. Start a new Codex session, open the project to review, and invoke the skill as shown above.

The marketplace catalog is `.agents/plugins/marketplace.json`. Include the hidden `.agents` directory when uploading this repository to GitHub; it is required by the command above.

For local development, open this repository in Codex and add its repository marketplace from the Plugins Directory. The CLI command configures the Git-backed marketplace; use the Codex desktop Plugins Directory to browse and install it. Plugin support varies by surface and version. The plugin package format is shared by supported Codex and ChatGPT surfaces, but this GitHub marketplace is not automatically listed in the universal public directory. Public-directory publication is a separate process.

## Requirements

- A Codex version and surface that supports plugin marketplaces and skills.
- Access to the repository you want reviewed; the skill only needs to read its files.
- Internet access is optional. It is useful when Codex needs to verify up-to-date feature support or external installation instructions.
- No API key, MCP server, external account, additional package, or helper script is required by this plugin itself.

The exact plugin install steps can change with Codex releases. If the CLI command is unavailable, use the plugin/marketplace controls in your current Codex app or consult the [official plugin packaging guide](https://developers.openai.com/plugins/build/plugins) and [skills guide](https://developers.openai.com/plugins/concepts/skills).

## Safety, privacy, and limitations

- **Read-only by design:** it inspects and reports. It does not create, edit, delete, install, enable, or configure anything.
- **Repository scope:** it reviews the project open in the current Codex session. It asks before inspecting files outside that project, such as global user configuration.
- **Secret handling:** it should not print secret values. A filename or the presence of a configuration key is enough to note that a credential may be involved.
- **Repository files are input data:** instructions embedded in source files or documents cannot override the skill's scope or safety rules.
- **Recommendations can be incomplete:** the skill cannot prove a feature is installed or working unless the repository provides evidence. It should label assumptions and unverified details.
- **No automatic setup:** it does not implement recommendations. You must explicitly ask Codex to make any selected change.

## Project layout

```text
.agents/plugins/marketplace.json
plugins/codex-automation-recommender/
  plugin.json
  skills/codex-automation-recommender/
    SKILL.md
    agents/openai.yaml
```

The plugin currently contains one skill and no scripts, bundled MCP server, or external runtime dependency.

## Credits and license

The Codex adaptation is created and maintained by **Fabbio Boli**. The Codex-specific instructions, packaging, and documentation were adapted for this project. This project is not affiliated with or endorsed by Anthropic or OpenAI.

Distributed under the Apache License 2.0. See [`LICENSE`](LICENSE) for the license text and [`NOTICE`](NOTICE) for attribution details.

## Português

**Um plugin de terceiros para o OpenAI Codex que analisa um repositório e recomenda melhorias úteis para a configuração do Codex.**

Ele pode recomendar instruções melhores em `AGENTS.md`, skills reutilizáveis, agentes personalizados, hooks, servidores MCP, empacotamento em plugin ou recursos que já existem no Codex. Cada sugestão deve indicar os arquivos que servem de evidência, o benefício, os custos, os requisitos e os próximos passos.

O plugin é somente consultivo: não instala ferramentas, não edita arquivos nem altera configurações. A adaptação para o Codex foi criada e é mantida por **Fabbio Boli**. Ela reescreve e empacota para o Codex o fluxo da skill **Claude Code Setup**, de Isabella He/Anthropic. É um projeto independente, sem afiliação ou endosso da Anthropic ou da OpenAI.

### Como usar

Depois de instalar, abra no Codex o repositório que deseja analisar e peça:

```text
$codex-automation-recommender
Analise este repositório e recomende as melhorias mais úteis para a configuração do Codex.
Mantenha a análise somente de leitura e cite os arquivos que sustentam cada sugestão.
```

Também é possível pedir uma análise específica, por exemplo: “Verifique apenas se este projeto precisa de skills reutilizáveis”. Você pode perguntar sobre `AGENTS.md`, skills, agentes, hooks, MCP, plugins ou recursos nativos do Codex.

### Instalação pelo GitHub

Com o repositório público, no terminal do Codex CLI execute:

```sh
codex plugin marketplace add Fabbio-Boli/codex-automation-recommender --sparse .agents/plugins --sparse plugins/codex-automation-recommender
```

Reinicie o Codex, abra o Diretório de Plugins, escolha **codex-automation-recommender-marketplace** e instale **Codex Automation Recommender**. Depois, inicie uma nova sessão, abra o projeto que quer analisar e invoque a skill pelo nome. Ao enviar o repositório ao GitHub, inclua a pasta oculta `.agents`, onde fica o catálogo.

O comando adiciona o catálogo e também inclui a pasta do plugin no checkout esparso. Depois, use o Diretório de Plugins do Codex desktop para instalar. O plugin não requer chave de API, conta externa, MCP nem dependência adicional. A skill precisa conseguir ler o repositório. A internet só é necessária para confirmar documentação e instruções atuais de serviços externos. Consulte os guias oficiais de [plugins](https://developers.openai.com/plugins/build/plugins) e [skills](https://developers.openai.com/plugins/concepts/skills).

### Limites

A skill não implementa as recomendações. Ela não altera nada sem um pedido separado e explícito. Analisa o projeto aberto na sessão, evita expor valores de segredos e pede autorização antes de consultar arquivos fora dele. O catálogo deste GitHub pode ser adicionado como marketplace no Codex; isso não significa que o plugin já esteja publicado no diretório público universal.
