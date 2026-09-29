# blender-mcp-proxy

A policy-enforcing proxy that sits in front of a Blender MCP server.

Blender MCP servers let an AI client run arbitrary Python inside Blender.
This proxy runs on the Blender machine, hides the real MCP server behind a
single HTTP entry point, and decides for every request whether to allow it,
hold it for human approval, or reject it.

## Status

Design phase. There is no code yet.

## Planned design

- **Topology**: the MCP client and Blender run on separate machines. The
  proxy runs on the Blender machine and starts the real MCP server as a
  child process, so the server is never reachable from the network.
- **Default deny**: unknown tools, unknown MCP messages, and unknown Blender
  operators are rejected.
- **Two inspection layers**: the MCP message layer (which tool is called)
  and the code layer (the Python passed to the code execution tool).
- **No de-obfuscation**: code that cannot be resolved statically is
  rejected, and features that execute strings as code are closed off.
- **Three verdicts**: allow, needs approval, reject. Approval happens over
  a channel the model cannot operate.
- **Independent validator**: the code validator is written for this project
  and does not depend on any MCP server implementation.

## Conventions

- Documentation and code comments are written in English.
