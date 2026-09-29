# blender-mcp-secure-proxy

A pass-through proxy that sits in front of a Blender MCP server and stops
dangerous requests until the user allows them.

Blender MCP servers let an AI client run arbitrary Python inside Blender.
This proxy runs on the Blender machine and exposes a single HTTP entry
point. It forwards requests from the model to Blender unchanged. When it
detects a dangerous request, it holds that request, reports it to the user,
and asks for permission.

## Status

Design phase. There is no code yet.

## Planned design

- **Topology**: the MCP client and Blender run on separate machines. The
  proxy runs on the Blender machine and starts the real MCP server as a
  child process, so the server is never reachable from the network.
- **Pass-through by default**: requests are forwarded to Blender as they
  are. The proxy does not rewrite them.
- **Hold and ask**: a request detected as dangerous is held. The user sees
  what was requested and why it was flagged, then allows or denies it.
- **Two inspection layers**: the MCP message layer (which tool is called)
  and the code layer (the Python passed to the code execution tool).
- **Independent detector**: the detection logic is written for this project
  and does not depend on any MCP server implementation.

## Conventions

- Documentation and code comments are written in English.
