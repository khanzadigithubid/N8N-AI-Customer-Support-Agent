# AI Customer Support Agent (n8n)

An n8n workflow that answers customer questions 24/7 using OpenAI.

## Features
- Replies in the customer's language (English, Urdu, Roman Urdu)
- Remembers the last 10 messages of each conversation
- Answers only from your company information
- Detects angry or unresolved cases and flags them for human handoff

## Setup
1. Import `ai-customer-support-agent.json` into n8n (Import from File).
2. Add your OpenAI credential to the OpenAI Chat Model node.
3. Edit the system message with your company details.
4. Activate the workflow and send a POST request to the webhook.

## Example request
{"sessionId": "u1", "message": "How long does delivery take?"}
