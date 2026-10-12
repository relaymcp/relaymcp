# RelayMCP: a WhatsApp MCP server for your AI assistant

RelayMCP is a hosted, per-user [Model Context Protocol](https://modelcontextprotocol.io) (MCP) server that connects **ChatGPT, Claude, Cursor** and other MCP clients to **your own personal WhatsApp**, with privacy and anti-spam safeguards.

> **Private pilot, invite only.** Join the waitlist at **https://relaymcp.app**.
> Setup guides: **https://relaymcp.app/guides/**

This repository holds documentation and directory metadata only. It contains no source code.

RelayMCP is an independent product. It is not affiliated with, endorsed by, or sponsored by WhatsApp or Meta.

## What you can ask your AI to do
- **Reminders:** "Remind me tomorrow at 10 to call Rahul back."
- **Follow-ups:** "If the supplier hasn't confirmed by Friday, draft a nudge."
- **Find what someone said:** "What time did Priya say the meeting was?"
- **Summarise chats:** decisions, questions for you, and anything waiting on your reply.
- **Draft and send replies** to your contacts, one person at a time.
- **Voice notes and media:** voice notes are transcribed (Hindi and English), and your AI can read images and documents people send you.

## How it works
1. **Link WhatsApp.** Scan a QR code under *Linked devices* on your phone. RelayMCP joins as a companion device, and your old chat history isn't imported.
2. **Connect your AI tool.** Add your personal RelayMCP URL as a remote MCP server.
3. **Set your privacy, then ask.** Block the chats you want kept private, choose how long messages are kept, and start asking.

## Connection details
| | |
|---|---|
| Endpoint | `https://<user>-mcp.relaymcp.app/mcp` (one per user, issued when you join the pilot) |
| Transport | Streamable HTTP |
| Auth | OAuth 2.1 with Dynamic Client Registration, **or** a bearer API key (`Authorization: Bearer rmcp_live_...`) |

Example client config (API key):
```json
{
  "mcpServers": {
    "relaymcp": {
      "url": "https://<user>-mcp.relaymcp.app/mcp",
      "headers": { "Authorization": "Bearer rmcp_live_..." }
    }
  }
}
```
Clients that support OAuth (ChatGPT, Claude) only need the URL. Step-by-step guides are at https://relaymcp.app/guides/.

## Tools (34)
**Contacts and chats:** `search_contacts`, `get_contact`, `list_chats`, `get_chat`, `get_direct_chat_by_contact`, `get_contact_chats`, `get_last_interaction`
**Messages:** `list_messages`, `get_message_context`, `mark_messages_read`, `list_waiting_on_me`
**Sending:** `send_message`, `send_reaction`, `send_file`, `send_audio_message`, `get_send_queue`, `cancel_queued_message`
**Media:** `download_media`, `view_media`, `get_media`, `transcribe_audio`
**Groups (read only):** `list_groups`, `list_group_members`
**Reminders and follow-ups:** `create_reminder`, `schedule_followup`, `list_followups`, `update_followup`, `cancel_followup`
**Privacy and account:** `block_chat`, `list_blocked_chats`, `request_unblock_chat`, `get_unblock_request_status`, `get_privacy_status`, `get_account_status`

## Privacy safeguards
- **Block any chat or group.** Its messages are dropped the moment they arrive: never stored, never shown to the AI, media never downloaded. Blocking also wipes anything already stored for that chat.
- **Only you can unblock.** Unblocking needs a code shown only on your own RelayMCP dashboard. Your AI never sees it.
- **Short memory.** Messages are deleted automatically after 72 hours (adjustable). Old chat history isn't imported when you link.
- **Encrypted at rest.** Message text is encrypted at rest, in storage on AWS in Mumbai, India. Logs never contain message text.
- **Delete anytime.** Unlink your device and all your data is wiped.
- **No selling.** Messages are used only to run the features you use, never sold or used for ads. Handled in line with India's DPDP Act, 2023.

## Anti-spam safeguards
RelayMCP is a reminder and follow-up tool, not a broadcast tool.
- Messages go out after a random 30 to 120 second delay, never in bursts.
- Each message goes to exactly one person. No groups, lists or broadcasts.
- Only people in your contacts or chats you already have.
- Quiet hours: no sends between 9 PM and 9 AM in the recipient's local time.
- About 30 unique recipients a day, and the same text can go to at most 3 people.
- Accounts used for spam or bulk messaging get paused or banned.

RelayMCP uses WhatsApp's linked-devices feature. Use it for your own conversations and in line with WhatsApp's terms.

## Pricing
Free for early users during the private pilot. Planned plans are listed at https://relaymcp.app.

## Contact
tushar@excelus.in · https://relaymcp.app/contact.html · Excelus Foodbev Pvt Ltd, Mumbai, India
