# Self-review: Codex Automation Recommender

I reviewed this package with its own skill and then validated the published GitHub marketplace installation in a fresh Codex conversation. This document records what I observed and which checks remain open.

## What this project is

This is a third-party plugin package for OpenAI Codex. Its only capability is one instruction-based skill, `codex-automation-recommender`. It reads the repository that the user has open in Codex and recommends ways to tailor Codex to that project.

It does not contain a scanner program, web service, model/API integration, MCP server, lifecycle hook, or setup installer. The Codex host supplies the model and file-reading tools; the skill supplies the review procedure and report format.

## Capabilities described by the skill

| Area | What the skill should look for |
| --- | --- |
| Project snapshot | Stack and workflow evidence in manifests, lockfiles, source imports, docs, tests, CI, and deployment files |
| Existing Codex setup | Repository instructions, skills, agent definitions, project configuration, MCP references, plugin catalogs, and hooks visible inside the project |
| Improvement options | Project instructions, reusable skills, custom agents, hooks, MCP servers, plugins, and built-in Codex capabilities |
| Recommendation quality | Evidence, benefit, trade-off, requirements, and setup guidance for each relevant suggestion |
| Safety | Read-only inspection, no project commands or scripts, secret-value avoidance, and permission before looking outside the project |

## Gaps found and addressed

1. **The original usage guide was incomplete.** It did not show how to explicitly invoke the skill or request a category-specific review. The README and skill metadata now include invocation examples and explain the report format.
2. **The previous marketplace command selected only the catalog directory.** The plugin itself lives under `plugins/`, so the sparse checkout also needs that plugin directory. The documented command now includes both sparse paths.
3. **The scope was described too generally.** The skill now lists what it may inspect, forbids running project scripts during review, defines evidence and trade-off fields, and distinguishes a detected config from a working integration.
4. **Requirements and non-features were unclear.** The README now states that no API key, MCP server, account, extra package, or helper script is required, and that recommendations are never applied automatically.
5. **Publisher identity and product status were ambiguous.** The package now identifies Fabbio Boli as developer and calls itself an independent third-party Codex plugin. It does not claim to be made or endorsed by OpenAI.
6. **Package metadata was sparse.** The portable manifest now contains OpenAI-specific display metadata and a read-only capability declaration, in addition to portable identity and license fields.

## Live validation performed

On 2026-11-02, I completed these checks:

- **GitHub catalog:** Added `Fabbio-Boli/codex-automation-recommender` with sparse paths `.agents/plugins` and `plugins/codex-automation-recommender`. Codex resolved the remote marketplace and its plugin folder.
- **Installation:** Installed `codex-automation-recommender@codex-automation-recommender-marketplace`; Codex reported version `1.0.0` installed and enabled.
- **Fresh conversation:** Started a new Codex conversation and explicitly invoked `$codex-automation-recommender`. The skill activated, followed its report format, and cited repository paths including the skill, plugin manifest, and marketplace catalog.
- **Read-only behavior:** The review did not run project scripts or change repository files. `git status` remained clean after the review.
- **Package consistency:** The GitHub marketplace checkout and installed plugin copies of `plugin.json`, `SKILL.md`, and `agents/openai.yaml` matched after normalizing line endings. The marketplace catalog resolved the expected `./plugins/codex-automation-recommender` directory.

The live review also suggested concise maintainer guidance in a root `AGENTS.md`. This is optional; the plugin works without that file.

## Still to do

- Review at least one separate sample repository, ideally one with no Codex setup and one that already has Codex instructions or skills. The live review above analyzed this plugin repository itself.
- If desired, submit the package separately for the universal public Plugins Directory. A public GitHub repository or Git marketplace does not publish it there automatically.

The checks above validate the GitHub marketplace catalog and a fresh-session invocation in the Codex environment used for this review. They do not guarantee identical behavior in every Codex version or surface.

## Current requirements

- A supported Codex host with plugin and skill support.
- Read access to the repository being reviewed.
- Internet access only when up-to-date external documentation or vendor setup details need verification.
- No separate API key or external service for the plugin itself.
