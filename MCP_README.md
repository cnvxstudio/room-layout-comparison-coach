# Room Layout Comparison Coach — local MCP companion

A read-only, open-source MCP server for comparing furniture arrangements from actual room measurements. It exposes an original planning guide and a reusable comparison prompt. The guide works without opening a website. Prepared by Ethan Lee for the 3D Room Maker team.

## Run locally

Requires Python 3.11+ and [uv](https://docs.astral.sh/uv/). Download `mcp_server.py` from this repository and run:

```sh
uv run /absolute/path/to/mcp_server.py
```

The script declares the pinned official Python MCP SDK dependency (`mcp==1.30.0`); uv installs it into its managed environment. First use needs internet to install dependencies. Standard MCP stdio transport is used; waiting for a client is normal.

For an MCP client that accepts a `mcpServers` configuration:

```json
{"mcpServers":{"room-layout-coach":{"command":"uv","args":["run","/absolute/path/to/mcp_server.py"]}}}
```

Replace the path with your downloaded file. Your client must support MCP prompts/resources; client-specific configuration may differ.

## Available capabilities

- Resource `room-layout://guide`: measurement worksheet, rectangle checks, two worked arrangements and optional manual 3D preview instructions.
- Prompt `compare_room_layouts`: accepts `measurements` (required text) and `priority` (optional). Example measurements: `Room 3 x 4 m; sofa 2 x 0.9 m; coffee table 0.9 x 0.5 m; door hinge unknown.` The prompt asks the assistant to compare two arrangements, preserve the same furniture inventory and flag unresolved measurements.
- No executable tools, network calls, telemetry, API keys or persistent room storage in this server. The host AI service receives the prompt/measurements you choose to share; do not send your address or sensitive personal information.

The server supplies guidance; the host model produces any comparison. It does not calculate or certify building-code compliance, generate room models, connect to a room-planning API, manipulate furniture in the browser or access private cloud saves.

## Optional 3D preview

Open [3D Room Maker](https://3droommaker.com/) to manually preview a layout with living-room, bedroom or blank-room templates. Move, rotate and resize available furniture, then inspect the arrangement from several 3D angles. Recheck the physical room with a tape measure. The preview is approximate.

## Verification and license

Local verification covers real stdio initialization, listing and reading the guide, listing and getting the prompt, and confirming there are no tools. It does not demonstrate host-model quality or certification for every MCP client. MIT license applies to this original companion resource; product source and third-party assets are not included.
