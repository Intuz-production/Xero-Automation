*Intuz — Your automation partner, one workflow at a time.*

<p align="center">
  <picture>
    <img alt="Banner Image" src="https://github.com/user-attachments/assets/210f97fc-0fce-404a-b647-7dfe1302cd37" />
  </picture>
</p>

[Intuz](https://www.intuz.com) helps organizations orchestrate AI, automation, and enterprise systems through scalable workflows. Our repository showcases proven implementations across healthcare, operations, customer support, document processing, sales, and back-office functions, enabling teams to accelerate automation initiatives without starting from scratch.

[N8N Creator](https://n8n.io/creators/intuz/) · [Workflow Automation](https://www.intuz.com/workflow-automation-services/) · [AI Consulting Company](https://www.intuz.com/company/) · [For Custom Workflow Automation](https://www.intuz.com/get-started/)

# Answer finance questions from Xero via WhatsApp, Telegram, Slack, and OpenAI

## Quick overview

This workflow answers finance questions received on WhatsApp (via WAHA) or Telegram by fetching data from Xero, drafting a validated response with OpenAI, optionally posting the result to Slack, and persisting conversation state in an n8n Data Table.

## How it works

1. Receives an incoming message from WhatsApp via a WAHA webhook (with HMAC verification) or from a Telegram bot trigger.
2. Normalizes the incoming message into a consistent format, applies workflow configuration, and blocks unauthorized senders based on an allowed-users list.
3. Loads the prior conversation state from an n8n Data Table and decides whether the message is a Slack-share follow-up (Yes/No/post) or a new finance request.
4. For new requests, uses OpenAI to classify the intent (accounts receivable, cash position, or bills due this week) and replies with help text if the intent is unknown.
5. Retrieves the connected Xero organisations, selects the correct Xero tenant, and queries the relevant Xero endpoints to build a canonical text summary for the requested report.
6. Uses OpenAI to rewrite the canonical Xero summary as a concise chat response and validates it against the canonical numbers before asking whether to post the update to Slack.
7. Saves the updated conversation state and sends the reply back to the originating channel (WhatsApp via WAHA or Telegram), posting the previous answer to Slack if the user confirms.

## Setup

1. Connect credentials for Xero OAuth2, OpenAI, Slack, and Telegram, and add HTTP Header Auth credentials for the WAHA send API.
2. Configure WAHA to send message events to the workflow’s webhook URL and set the matching HMAC SHA-512 secret and WAHA base URL.
3. Create an n8n Data Table named “Finance Bot Conversation State” with columns for stateKey, userId, channel, chatId, lastIntent, lastResponse, and pendingSlackConfirmation.
4. Update the workflow configuration values for allowed users, the Slack channel ID, and (if you have multiple Xero organisations) the Xero tenant ID.

## FAQ

**Which messaging platforms does this workflow support?**  
It supports WhatsApp via WAHA, Telegram, and optionally posts results to Slack.

**How does the workflow handle finance questions?**  
It classifies the intent using OpenAI, fetches relevant data from Xero, drafts a validated response, and sends it back to the user.

**What is required to set up this workflow?**  
You need to connect credentials for Xero OAuth2, OpenAI, Slack, Telegram, configure WAHA webhook and HMAC secret, create an n8n Data Table for conversation state, and update workflow configuration values.

## Related n8n templates from Intuz

- [Material TextField for iOS](https://github.com/Intuz-production/MaterialTextField-iOS)
- [Permission Manager for Android](https://github.com/Intuz-production/PermissionManager-Android)
- [AudioTrimmer iOS](https://github.com/Intuz-production/AudioTrimmer-iOS)

[See all of Intuz's free n8n templates](https://www.intuz.com/n8n-workflow-automation-templates/)

## Connect with us

Intuz is a USA-based AI & workflow automation company with 16+ years of experience building custom AI-enabled workflow automations for SMBs and Enterprises, specializing in agentic AI, LLM integrations, and CRM/ERP sync across Healthcare, FinTech, eCommerce, Manufacturing, and Real Estate.

* **Website:** [https://www.intuz.com](https://www.intuz.com)
* **Email:** [getstarted@intuz.com](mailto:getstarted@intuz.com)
* **LinkedIn:** https://www.linkedin.com/company/intuz/
* **Get Started:** https://n8n.partnerlinks.io/intuz

## For Custom Workflow Automation

[Click here - Get Started](https://www.intuz.com/get-started/)
