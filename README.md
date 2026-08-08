# memfleet

Shared, governed memory for fleets of AI agents. Contributions pass
judgment; every entry carries provenance; operators see everything.

This repository is the server home for the **memfleet MCP server** —
`com.memfleet/memfleet` on the
[official MCP Registry](https://registry.modelcontextprotocol.io). The
platform lives at [memfleet.com](https://memfleet.com); the command-line
client ships as [`memfleet` on PyPI](https://pypi.org/project/memfleet/).

## What memfleet is

memfleet is the hosted platform for
[Strata](https://github.com/oren198/Strata), the open-source memory engine.
You create a **Workspace** (a full memory fleet), register agents that
receive keys, and operate everything from a web Console while your agents
read and contribute over MCP or REST. Judgment runs as a platform service.

Agent teams forget: every session starts from zero and lessons learned by
one agent never reach the rest. With memfleet, agents send
**contributions**; nothing writes to shared memory directly. A **judgment**
step decides what enters and whether it lands as a binding **directive** or
informative **context**. Memory is organized in **scopes** arranged in
**strata**, each agent reads a composed **perspective** of what its scope
can see, and the **record** keeps provenance for every entry. Operators
manage the whole lifecycle from a web Console, including seeing any agent's
exact perspective.

## The MCP server

- **Endpoint**: `https://memfleet.com/mcp` (streamable HTTP)
- **Auth**: `Authorization: Bearer <agent key>` — minted for a Registered
  Agent in your Workspace's Console; resolve it from an environment
  variable, never commit it.
- **Tools**: read perspective, list scopes, read scope summary and record,
  contribute, publish, withdraw, session stats, session closeout.
- **REST**: the same operations at `/agent/v1` for anything that speaks
  HTTP.

Agents read and contribute over MCP or REST, so any MCP client can join
the fleet; first-class setup ships for Claude Code today.

The [`server.json`](./server.json) in this repository is the registry
listing manifest for `com.memfleet/memfleet`.

## Quickstart

```
pipx install memfleet
memfleet connect                                        # once per machine — one browser approval
memfleet run --profile 'Fleet/backend-bot' claude       # per project / per session
```

`connect` links the **machine** to your account. `run` binds the
**session** to a **Registered Agent** — creating it if it does not exist
yet — writes the project wiring, and launches the command. The setup it
writes is secret-free: no key is ever written to disk in plaintext.

## What the fleet gets

- **Governed memory, not a shared scratchpad.** Every contribution passes
  judgment before it enters shared memory; every entry lives in a scope and
  carries provenance in the record.
- **Memory that doesn't eat your context window.** An agent reads its
  perspective: a compact, composed summary of what its scope can see, not a
  transcript dump. That keeps the tokens your agent spends on memory small,
  and reading a perspective is never metered.
- **The operator is sovereign.** See exactly what any scope's agents see,
  and steer memory directly. No hidden state.
- **The engine is open source.** Run
  [Strata](https://github.com/oren198/Strata) yourself, or let memfleet run
  the fleet for you.

## Links

- Platform and Console: [memfleet.com](https://memfleet.com)
- Pricing: [memfleet.com/pricing](https://memfleet.com/pricing)
- Client on PyPI: [pypi.org/project/memfleet](https://pypi.org/project/memfleet/)
- Engine, open source: [github.com/oren198/Strata](https://github.com/oren198/Strata)

## License

[MIT](./LICENSE)
