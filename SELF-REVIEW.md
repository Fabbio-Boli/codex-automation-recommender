# Self-review: Codex Automation Recommender

This review applies the workflow described by the packaged skill to this repository itself. It is a static review of the package files; it does not claim that installation or invocation was exercised in a live Codex client.

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

## Still to do before calling it fully validated

- Install from the published GitHub repository in a supported Codex desktop version and confirm the marketplace catalog resolves the plugin folder.
- Start a fresh Codex conversation, explicitly invoke the skill, and inspect whether the host presents and follows the skill instructions as intended.
- Repeat the review on a small sample repository and a repository with existing Codex setup. Compare output against the skill's evidence, safety, and report requirements.
- If desired, submit the package separately for the universal public Plugins Directory. A public GitHub repository or Git marketplace does not by itself publish it there.

These checks require an available Codex client and a public remote repository. They have not been represented as complete by this static review.

## Current requirements

- A supported Codex host with plugin and skill support.
- Read access to the repository being reviewed.
- Internet access only when up-to-date external documentation or vendor setup details need verification.
- No separate API key or external service for the plugin itself.
