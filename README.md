# Hybrid_MCPServer_Rust
We build a stateful Hybrid MCP Server( with both HTTP JSON-RPC and GraphQL endpoints) with in Depth Security and Post‑Quantum Resilience, using open-source tools utilising the Meson build System.

## Requirements for a  Hybrid MCP Server with In-Depth Security and Post-Quantum Resilience
MCP is the standard protocol created by Anthropic for connecting AI agents to external tools and data sources. This server implements the MCP protocol to provide AI applications with a standardized interface for tool invocation and data access.
This document defines the complete requirements for a stateful hybrid Model Context Protocol (MCP) Server that exposes both an HTTP JSON-RPC 2.0 endpoint and a GraphQL endpoint, while incorporating in-depth security protections and Post-Quantum Cryptography (PQC) resilience.

## Why Stateful Design
According to the major architectural changes in the (MCP 2026-07-28 specification)[https://mcp.directory/blog/mcp-2026-07-28-release-candidate], long-lived protocol-level sessions (via the Mcp-Session-Id header) have been removed. Therefore, this server's "statefulness" is achieved through the following mechanisms:
Explicit State Handles: The server generates and returns state identifiers (e.g., basket_id, workflow_id), which the client sends back in subsequent calls.
Session Affinity: At the deployment level, all interactions from the same user are bound to the same upstream server instance.
Client-Side State Storage: The server is allowed to store state information on the client side (similar to HTTP Cookie mechanisms).
Critical Constraint: The server MUST NOT use protocol-level sessions for authentication. All authentication MUST be based on per-request token validation.
