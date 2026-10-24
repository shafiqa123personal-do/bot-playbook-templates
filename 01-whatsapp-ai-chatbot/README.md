# WhatsApp AI Chatbot: free n8n template (Bot Playbook, Episode 1)

A WhatsApp bot that answers questions about your business day and night, remembers each customer's conversation, and saves every message to a Google Sheet. It's the exact workflow built in the video.

```
WhatsApp Trigger → Only text messages → AI Agent (Google Gemini + Simple Memory) → Send reply
                                      ↘ Save lead (Google Sheets)
```

## Set it up in 10 minutes

1. **Import:** in n8n, open a new workflow, then use the **⋯** menu → **Import from URL** and paste this link:
   ```
   https://raw.githubusercontent.com/shafiqa123personal-do/bot-playbook-templates/main/01-whatsapp-ai-chatbot/whatsapp-ai-chatbot.json
   ```
   Or download [`whatsapp-ai-chatbot.json`](whatsapp-ai-chatbot.json) and use **Import from File**.
2. **Meta app** (developers.facebook.com): create an app that connects with customers through WhatsApp. In **WhatsApp › API Setup**, add your own phone number under **To**. Copy the **WhatsApp Business Account ID** and the **access token**. In **App settings › Basic**, copy the **App ID** and **App Secret**, add your privacy policy and terms links, and switch the app to **Live**.
3. **WhatsApp Trigger:** create a credential with the App ID as **Client ID** and the App Secret as **Client Secret**.
4. **Google Gemini Chat Model:** create a credential with an API key from Google AI Studio (**Get API key**). Pick a Flash model.
5. **AI Agent → Options → System Message:** replace Bella's Hair Studio (an example business) with your own hours, prices and answers. Keep the two safety lines: *answer only using the information below*, and the *"I'll ask the team"* fallback.
6. **Send reply:** create a credential with the access token + WhatsApp Business Account ID, then choose your number in **Sender Phone Number**.
7. **Save lead:** connect Google, paste your sheet's link, and make sure the sheet has the columns **Date, Name, Phone, Message**.
8. Click **Publish**, then send your test number a message from your phone.

## If nothing happens

1. Is the workflow **Published**?
2. Is your Meta app **Live**, with privacy policy and terms links?
3. **Is your app subscribed to your WhatsApp Business Account?** Publishing registers the webhook but doesn't subscribe the app. Follow "Workflow doesn't run when WhatsApp messages arrive" in [n8n's WhatsApp Trigger docs](https://docs.n8n.io/integrations/builtin/trigger-nodes/n8n-nodes-base.whatsapptrigger/).
4. WhatsApp allows **one webhook per app**. If you tested with the test URL, publish again so the live URL is registered.

## Before real customers use it

- **Real number:** add your business number in WhatsApp Manager and verify it.
- **Permanent token:** the test token stops working after 24 hours. Create a System User token in Meta business settings and put it in both WhatsApp credentials.
- **Costs (October 2026):** replies within 24 hours of a customer's message are service messages. Each business number gets 1,000 free per month, then Meta charges per message ([Meta pricing](https://developers.facebook.com/docs/whatsapp/pricing)). After 24 hours, only approved templates can be sent.
- **Rules:** WhatsApp allows business assistants (questions, bookings, support), not general-purpose AI chatbots. Tell customers they're chatting with an AI, and give them a way to reach a person.
- **Memory:** Simple Memory lives inside n8n and is lost when n8n restarts. For a busy business, swap it for a database memory (Postgres or Redis).

Not affiliated with WhatsApp, Meta, n8n or Google. Made by Bot Playbook (SystemSync AI).
