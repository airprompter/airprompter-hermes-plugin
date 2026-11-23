# AirPrompter for Hermes Agent

AirPrompter connects Hermes to your saved prompt and workflow library. Create,
run, and improve reusable multi-step AI workflows, and save them for repeatable
runs across your AI tools.

## Install

```bash
hermes plugins install airprompter
hermes plugins enable airprompter
```

The first command takes the pinned release from the Hermes plugin catalog. To
take this repository directly instead, run
`hermes plugins install airprompter/airprompter-hermes-plugin`. Hermes installs
a plugin switched off, so the second command turns it on.

## Sign in

This package's `mcp.json` names the AirPrompter server, but it cannot sign you
in. Add the server to `~/.hermes/config.yaml`:

```yaml
mcp_servers:
  airprompter:
    url: https://mcp.airprompter.com/mcp
    auth: oauth
    trust: untrusted
```

An entry in `config.yaml` replaces this package's entry for the same server,
so keep `trust: untrusted`: with it, Hermes asks you before every tool call
that is not marked read-only. Then sign in and check the connection:

```bash
hermes mcp login airprompter
hermes mcp test airprompter
```

Start a new session, or run `/reload-mcp`, so Hermes loads the AirPrompter
tools.

## What this package does

- It contains no local code: it adds one skill and one remote MCP server
  (https://mcp.airprompter.com/mcp).
- Hermes stores and refreshes the sign-in tokens; none are in the package.
- Every read, save, and run goes to AirPrompter, with what the call carries.
- What the tools return reaches your model provider through the session: your
  saved prompts and workflows, including the saved prompt text a run hands
  back for the assistant to follow.
- Write tools change your saved AirPrompter library, and Hermes asks before
  each one.
- The tool list comes from the AirPrompter server at run time, so a pinned
  commit does not fix it.
- There is no background process and no self-update, and the package itself
  sends no telemetry.

The files are `plugin.json`, `mcp.json`, `skills/airprompter/SKILL.md`, this
README, `LICENSE`, and `assets/logo.png` (the AirPrompter logo).

## What AirPrompter records when you run a workflow

Every workflow you run through this plugin is reported to AirPrompter and saved
as a run record on your account. This reporting cannot be turned off.

A run record can include:

- which saved workflow ran, when, and from which account, organization, or
  workspace
- the AI tool and connection used, and the plugin version
- the input values you give the run, and any page or file references passed to
  it
- each step's status and timing, and the token counts and model name when Hermes
  reports them

Hermes sends each step's output to AirPrompter so the next step can use it. By
default that output is not stored. It is stored only if your account has opted
in to storing run results. Stored output can be read back through AirPrompter
and, if you use workflow evaluation, sent to an AI model that grades it.

AirPrompter also records usage analytics, such as that a run happened and the
workflow's name. Usage totals, such as how many workflows you ran and when you
last connected, go to our email service provider so we can send you product
messages. Your inputs and step outputs are not part of these.

Run records expire after about 120 days. Usage analytics are kept for up to a
year, and summarized totals can be kept longer. AirPrompter runs on Amazon Web
Services. See the [privacy policy](https://airprompter.com/privacy) for more.

## What you need

An AirPrompter account. New users can create an AirPrompter account at no
charge; some features need a paid AirPrompter plan.

## Links

- Privacy policy: https://airprompter.com/privacy
- Terms: https://airprompter.com/terms
- Documentation: https://airprompter.com/docs
- Support: support@airprompter.com

## License

MIT. See `LICENSE`.
