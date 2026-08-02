<p align="center">
  <a href="https://datarobot.com">
    <img src="https://af.datarobot.com/img/datarobot_logo.avif" width="600px" alt="DataRobot Logo"/>
  </a>
</p>
<h2 align="center">DataRobot Community</h2>
<p align="center">
  <a href="https://datarobot.com">Homepage</a>
  ·
  <a href="https://docs.datarobot.com">Documentation</a>
  ·
  <a href="https://af.datarobot.com">App Framework</a>
  ·
  <a href="https://docs.datarobot.com/en/docs/get-started/troubleshooting/general-help.html">Support</a>
</p>
<p align="center">
  <a href="https://join.slack.com/t/datarobot-community/shared_invite/zt-3uzfp8k50-SUdMqeux25ok9_5wr4okrg">
    <img src="https://img.shields.io/badge/%23all--datarobot--community-a?label=Slack&labelColor=30373D&color=81FBA6" alt="Slack #all-datarobot-community">
  </a>
</p>

Welcome! 👋 This is where DataRobot's **code-first building blocks** live — application templates you can clone and deploy today, the components they're assembled from, infrastructure-as-code providers, and hundreds of worked examples.

Everything here is public, permissively licensed, and meant to be forked and changed. Start from a template, keep what works, replace what doesn't.

---

## 🧭 DataRobot on GitHub

DataRobot's public code is spread across four organizations. Here's how to tell them apart:

| Organization | What lives there | Supported? |
|---|---|---|
| **[@datarobot](https://github.com/datarobot)** | The company org. Officially released, customer-facing projects — [custom model boilerplate](https://github.com/datarobot/datarobot-user-models), the [Airflow provider](https://github.com/datarobot/airflow-provider-datarobot), the [R client](https://github.com/datarobot/rsdk), and research like [syftr](https://github.com/datarobot/syftr). The [Python client](https://pypi.org/project/datarobot/) ships from here too. | ✅ Officially supported |
| **[@datarobot-community](https://github.com/datarobot-community)** ← *you are here* | Templates, accelerators, App Framework components, and the Terraform/Pulumi providers. Built by DataRobot engineers, field data scientists, and users — designed as starting points you adapt. | 🛠️ Community-maintained |
| **[@datarobot-oss](https://github.com/datarobot-oss)** | First-party open source from DataRobot R&D — the [`dr` CLI](https://github.com/datarobot-oss/cli), the [`datarobot-genai`](https://github.com/datarobot-oss/datarobot-genai) agent runtime, [agent skills for coding assistants](https://github.com/datarobot-oss/datarobot-agent-skills), Terraform infra modules, and shared GitHub Actions. | 🔬 No official support |
| **[@datarobot-forks](https://github.com/datarobot-forks)** | Forks of third-party OSS we patch and contribute back upstream — LiteLLM, OpenLLMetry, Ory Hydra, and others. Nothing here is DataRobot-developed. | ↩️ Upstream projects |

---

## 🚀 Start here

| I want to… | Go to |
|---|---|
| Ship an AI app this afternoon | [Application templates](#-application-templates) |
| Build a custom agentic application | [The App Framework](#-the-app-framework) |
| Give an agent tools over DataRobot | [MCP servers](#-mcp--tools) |
| Manage DataRobot resources as code | [Declarative API](#-declarative-api--infrastructure) |
| Learn by reading real notebooks | [Accelerators & learning](#-accelerators--learning) |

---

## 📦 Application templates

Application templates are code-first, end-to-end pipelines that provision DataRobot resources for you. Each one ships with metadata, dependency auto-installation, and infrastructure-as-code, so you can go from `git clone` to a hosted, shareable app — then customize every layer.

Every template opens directly in a DataRobot Codespace (look for the badges in each repo) or runs locally.

| Template | What it builds |
|---|---|
| **[datarobot-agent-application](https://github.com/datarobot-community/datarobot-agent-application)** | The flagship agentic template — a multi-agent workflow, FastAPI backend, React frontend, and MCP server, deployable in one command. Pick your framework: CrewAI, LangGraph, LlamaIndex, or NVIDIA NeMo Agent Toolkit. |
| **[talk-to-my-data-agent](https://github.com/datarobot-community/talk-to-my-data-agent)** | Conversational analytics over your own datasets — ask questions in natural language, get charts and answers back. |
| **[talk-to-my-docs-agents](https://github.com/datarobot-community/talk-to-my-docs-agents)** | Multi-agent document Q&A across Google Drive, Box, and local files. |
| **[guarded-rag-assistant](https://github.com/datarobot-community/guarded-rag-assistant)** | A RAG chatbot with business-logic and LLM guardrails, plus a predictive secondary model that scores response quality. |
| **[forecast-assistant](https://github.com/datarobot-community/forecast-assistant)** | Time-series forecasting with a shareable UI and per-series explanations of what's driving the forecast. |
| **[predictive-content-generator](https://github.com/datarobot-community/predictive-content-generator)** | Turns predictive model output into drafted content — personalized offers, approval letters, and similar. |
| **[predictive-ai-starter](https://github.com/datarobot-community/predictive-ai-starter)** | A minimal predictive AI train-and-deploy pipeline. The best base for authoring a brand-new template. |
| **[datarobot-mcp-template](https://github.com/datarobot-community/datarobot-mcp-template)** | A production-ready [FastMCP](https://github.com/jlowin/fastmcp) server with DataRobot tools built in. |

📖 [Application template documentation](https://docs.datarobot.com/en/docs/workbench/wb-apps/app-templates/index.html)

> [!NOTE]
> Templates are **starting points**. Expect to adapt them to your data, your guardrails, and your business requirements before production.

---

## 🧱 The App Framework

The [**DataRobot App Framework**](https://af.datarobot.com) (AF) is the machinery behind those templates. Rather than one monolithic scaffold, an AF app is *composed* from small, independently versioned [copier](https://copier.readthedocs.io/) templates called **components**. You choose the pieces you need; the framework renders them into a single project that you own outright.

The lifecycle is the same for every app:

```
  dr start / dr component add          task dev              task deploy
        │                                 │                       │
   scaffold & compose  ──▶  build locally & iterate  ──▶  Pulumi provisions
   af-component-* modules      agent · MCP · API · UI      on DataRobot
```

Five tools do the work: [`dr`](https://cli.datarobot.com) (orchestration), `uv` (Python), `copier` (templating), `task` (go-task), and `pulumi` (infrastructure).

### The components

| Component | What it adds | Builds on |
|---|---|---|
| **[af-component-base](https://github.com/datarobot-community/af-component-base)** | The root scaffold every AF app starts from. Creates the project structure and the `.datarobot/answers/` state that all other components read and update. Applied first, exactly once. | — |
| **[af-component-agent](https://github.com/datarobot-community/af-component-agent)** | The agentic core. Scaffolds an `agent/` package for your chosen framework — CrewAI, LangGraph, LlamaIndex, NVIDIA NeMo Agent Toolkit, or a framework-neutral base — on top of the [`datarobot-genai`](https://github.com/datarobot-oss/datarobot-genai) runtime. | base, llm |
| **[af-component-llm](https://github.com/datarobot-community/af-component-llm)** | Model access. Wires the DataRobot LLM Gateway by default, or points at a specific deployed model / LLM blueprint. Infrastructure only — no application code. | base |
| **[af-component-datarobot-mcp](https://github.com/datarobot-community/af-component-datarobot-mcp)** | A FastMCP server deployed as its own DataRobot deployment, giving your agent a governed set of tools. | base |
| **[af-component-fastapi-backend](https://github.com/datarobot-community/af-component-fastapi-backend)** | A FastAPI server running as a DataRobot custom application — a deliberately minimal backend surface to build on. | base |
| **[af-component-react](https://github.com/datarobot-community/af-component-react)** | A React single-page frontend on top of the FastAPI backend. | base, fastapi-backend |
| **[scaffold-af-component](https://github.com/datarobot-community/scaffold-af-component)** | 🧩 A GitHub template for authoring **your own** component — `copier.yml`, template tree, Taskfile, and CI, ready to go. | — |

Additional components cover agent **memory**, **vector databases** for RAG, **evaluation**, and **user credentials**.

### How components become templates

The same component library composes into every template above — the difference is just which pieces are applied:

- `datarobot-agent-application` → **base + agent + llm + mcp** (the agent component brings the FastAPI and React app along with it)
- `datarobot-mcp-template` → **base + mcp**
- `talk-to-my-docs-agents` → the agent application, with CrewAI pre-selected
- `talk-to-my-data-agent` → **base + llm + fastapi + react** — no agent

Because each component is version-pinned in `.datarobot/answers/`, you can pull upstream improvements into a project you've already customized with `dr component update`.

**Supporting tooling:** [app-framework](https://github.com/datarobot-community/app-framework) — the CLI-adjacent tooling for applying and updating components across a project.

> [!TIP]
> Building with a coding agent? [`datarobot-agent-skills`](https://github.com/datarobot-oss/datarobot-agent-skills) teaches Claude Code, Cursor, and friends how to drive the `dr` CLI and the DataRobot platform directly.

---

## 🔌 MCP & tools

Model Context Protocol servers let agents — yours or off-the-shelf clients like Claude Desktop and Cursor — call DataRobot capabilities as governed tools.

- **[datarobot-mcp-template](https://github.com/datarobot-community/datarobot-mcp-template)** — the full standalone template, with pre-built DataRobot tools, OpenTelemetry tracing, dynamic tool registration, and deployment infrastructure.
- **[af-component-datarobot-mcp](https://github.com/datarobot-community/af-component-datarobot-mcp)** — the same capability as a component, when you want an MCP server *inside* a larger app.

---

## 🏗️ Declarative API & infrastructure

Provision DataRobot entities — models, deployments, applications, credentials — programmatically. Pick the tool that matches your stack; application templates default to Pulumi.

| Repository | Use it for |
|---|---|
| **[terraform-provider-datarobot](https://github.com/datarobot-community/terraform-provider-datarobot)** | Terraform-native resource management. Also the source the Pulumi provider is generated from. |
| **[pulumi-datarobot](https://github.com/datarobot-community/pulumi-datarobot)** | The Pulumi provider — manage DataRobot resources in Python. |
| **[datarobotx-idp](https://github.com/datarobot-community/datarobotx-idp)** | Idempotent DataRobot helpers (`get_or_create_*`) for orchestration tools that aren't Terraform or Pulumi. |

📖 [Declarative API docs](https://docs.datarobot.com/en/docs/api/reference/declarative-api.html) · [Pulumi registry](https://www.pulumi.com/registry/packages/datarobot/) · [Terraform registry](https://registry.terraform.io/providers/datarobot-community/datarobot/latest)

Related in [@datarobot-oss](https://github.com/datarobot-oss): [datarobot-pulumi-utils](https://github.com/datarobot-oss/datarobot-pulumi-utils) (higher-level Pulumi `ComponentResource`s) and the `terraform-{aws,azurerm,google}-dr-infra` modules for standing up the platform itself.

---

## 📚 Accelerators & learning

| Repository | What you'll find |
|---|---|
| **[ai-accelerators](https://github.com/datarobot-community/ai-accelerators)** ⭐ | Repeatable, code-first notebook workflows organized by use case, generative AI, ecosystem integrations (Snowflake, AWS, Azure, GCP), and advanced API techniques. The single best place to browse for "how do I…". |
| **[agent-build-clinic](https://github.com/datarobot-community/agent-build-clinic)** | Six modular "agentic blocks" that build up a production-ready agent step by step — adding predictive forecasting and structured data querying to a chat interface. |

📺 Also worth a look: the [DataRobot YouTube channel](https://www.youtube.com/@DataRobot/featured) and the [AI Accelerators playlist](https://www.youtube.com/playlist?list=PLe-6XGmzriIhoP4o8q_SapBTQJstLIRTY).

---

## 🧰 Libraries

- **[datarobot-opentelemetry-integration](https://github.com/datarobot-community/datarobot-opentelemetry-integration)** — OpenTelemetry semantic conventions and helpers used across DataRobot for consistent tracing of GenAI workloads.

---

## 💬 Get involved

- **Slack** — join [`#all-datarobot-community`](https://join.slack.com/t/datarobot-community/shared_invite/zt-3uzfp8k50-SUdMqeux25ok9_5wr4okrg); most template repos also point at `#applications`.
- **Issues and PRs** — open them on the individual repository. Each has its own contributing guide.
- **Docs** — [docs.datarobot.com](https://docs.datarobot.com) for the platform, [af.datarobot.com](https://af.datarobot.com) for the App Framework, [cli.datarobot.com](https://cli.datarobot.com) for the `dr` CLI.
- **Help** — [general support and troubleshooting](https://docs.datarobot.com/en/docs/get-started/troubleshooting/general-help.html).

<details>
<summary>Looking for something that isn't listed?</summary>

This page highlights actively maintained repositories. Older tutorials, sample apps, and workshop material still live in the org — browse the [full repository list](https://github.com/orgs/datarobot-community/repositories?type=source&sort=updated). Note that anything not listed above may target older versions of the DataRobot API.

One repository worth calling out: [**datarobot-agent-templates**](https://github.com/datarobot-community/datarobot-agent-templates) is **deprecated**. If you landed there from an older link, use [datarobot-agent-application](https://github.com/datarobot-community/datarobot-agent-application) instead.

</details>

---

**Please note:** The code in these repos is sourced from the DataRobot user community and is not owned or maintained by DataRobot, Inc. You may need to make edits or updates for this code to function properly in your environment.
