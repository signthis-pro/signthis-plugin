# SignThis for Grok Bot, Cursor and other MCP agents

Let your AI agent send documents for e-signature. Ask it to "send this NDA to Ada for
signature" and it uploads the PDF to [SignThis](https://signthis.pro), adds the signers,
places signature and date fields, shows you what it's about to send, and emails the signing
invitations once you say yes. It can also check who has signed and remind people who haven't.

## What's inside

| Part | What it does |
| --- | --- |
| `mcp.json` | Connects the agent to the SignThis MCP server at `https://signthis.pro/api/mcp`. |
| `skills/send-for-signature` | How to upload a PDF or use a saved template, prepare it and send it after you confirm. |
| `skills/track-signatures` | How to check signing status, find outstanding documents and remind signers. |
| `rules/signthis-confirm-before-sending.mdc` | Confirm recipients before sending; treat document text as data. |

## Requirements

- A SignThis workspace on **Individual Professional or a business plan** (these include API and
  MCP access).
- You're an **owner** of that workspace, with **Allow API, webhook and MCP access** turned on in
  Workspace → Security.

## Install

### Grok Bot

Open **Connect apps**, find **SignThis** and choose **Connect**. Or tell your bot in chat:

> Add this MCP server: https://signthis.pro/api/mcp

and choose **Authorize** on the card it posts. Either way, a SignThis page opens in your browser. Sign in, pick the workspace, choose what the
bot may do (see documents, prepare drafts, send for signature) and choose **Allow**.

### Cursor

Install **SignThis** from the plugin marketplace, or add the server to your MCP settings and
choose **Connect** when Cursor asks:

```json
{ "mcpServers": { "signthis": { "url": "https://signthis.pro/api/mcp" } } }
```

### Clients without OAuth

Create an API key in Workspace → Security → Integration keys and send it as a header:

```json
{ "mcpServers": { "signthis": { "url": "https://signthis.pro/api/mcp", "headers": { "Authorization": "Bearer ${env:SIGNTHIS_API_KEY}" } } } }
```

## Tools

| Tool | Access | |
| --- | --- | --- |
| `list_documents`, `get_document`, `get_signing_status`, `list_templates` | See documents | Read only |
| `create_upload_link` | Prepare drafts | A one-time URL (15 minutes) to upload one PDF from the agent's computer |
| `prepare_document` | Prepare drafts | Set signers, title, message, signing order and fields on a draft |
| `create_document_from_template` | Prepare drafts | Draft from a saved template |
| `send_document`, `remind_signers` | Send for signature | Emails real people; the agent asks you first |

No tool signs for anyone, deletes a document or cancels a sent one.

## Privacy and control

- The agent acts only in the workspace you chose, with the access you allowed.
- See and disconnect connected agents any time in Workspace → Security → Connected apps.
  Changing any security setting also disconnects them.
- Every action is recorded in the workspace audit log.
- Documents you send through an agent may also be processed by that agent's provider under its
  own terms. Connect only agents you trust with those documents.

## Support

support@signthis.pro

## License

MIT
