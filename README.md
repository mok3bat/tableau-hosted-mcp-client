# Tableau Hosted MCP Client Metadata

This repository hosts the **Client ID Metadata Document (CIMD)** required to authenticate with the **Tableau Hosted MCP Server** using OAuth 2.1.

The document is publicly available via GitHub Pages and serves as the OAuth Client Identifier for applications connecting to Tableau Hosted MCP.

## Why this repository exists

Unlike many OAuth implementations that support **Dynamic Client Registration (DCR)**, Tableau Hosted MCP currently uses the **Client ID Metadata Document (CIMD)** approach.

Instead of registering an OAuth client dynamically, the client publishes a static metadata document over HTTPS.

During authentication, Tableau validates this document and uses its URL as the OAuth Client ID.

This repository exists solely to host that metadata document.

---

## Client Metadata URL

```
https://mok3bat.github.io/tableau-hosted-mcp-client/client.json
```

---

## Repository Structure

```
.
├── client.json
└── README.md
```

---

## client.json

The `client.json` file follows the OAuth 2.0 Client Metadata specification and contains information such as:

- Client Name
- Redirect URIs
- Grant Types
- Response Types
- Token Endpoint Authentication Method
- Client URI
- Application Metadata

Example:

```json
{
  "client_name": "Mo Tableau MCP Test Client",
  "redirect_uris": [
    "http://localhost:*/callback"
  ],
  "grant_types": [
    "authorization_code",
    "refresh_token"
  ],
  "response_types": [
    "code"
  ],
  "token_endpoint_auth_method": "none",
  "client_uri": "https://github.com/mok3bat/tableau-hosted-mcp-client"
}
```

---

## Using with FastMCP

```python
from fastmcp import Client
from fastmcp.client.auth import OAuth

oauth = OAuth(
    client_metadata_url="https://mok3bat.github.io/tableau-hosted-mcp-client/client.json"
)

client = Client(
    "https://mcp.tableau.com",
    auth=oauth
)
```

---

## Related Projects

### Tableau Hosted MCP SDK

A higher-level Python SDK that simplifies authentication, token persistence, and interaction with Tableau Hosted MCP.

```
https://github.com/mok3bat/tableau-hosted-mcp
```

---

## References

- Tableau Hosted MCP
- OAuth 2.1
- OAuth 2.0 Client Metadata (RFC 7591)
- Model Context Protocol (MCP)

---

## License

MIT
