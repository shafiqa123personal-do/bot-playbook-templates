# WhatsApp AI Booking Bot: free n8n template (Bot Playbook, Episode 2)

The Episode 1 WhatsApp chatbot, now with two tools: it checks your Google Calendar, offers free times, asks the customer to confirm, and books the appointment by itself. It's the exact workflow built in the video.

```
WhatsApp Trigger → Only text messages → AI Agent → Send reply
                                      ↘ Save lead (Google Sheets)
AI Agent uses: Google Gemini · Simple Memory · Check calendar · Book appointment
```

## Set it up in 15 minutes

1. **Import:** in n8n, open a new workflow, then use the **⋯** menu → **Import** → **From URL** and paste this link:
   ```
   https://raw.githubusercontent.com/shafiqa123personal-do/bot-playbook-templates/main/02-whatsapp-ai-booking-bot/whatsapp-ai-booking-bot.json
   ```
   Or download [`whatsapp-ai-booking-bot.json`](whatsapp-ai-booking-bot.json) and use **Import from File**.
2. **WhatsApp, Gemini and Google Sheets:** set them up exactly like Episode 1. The steps are in the [Episode 1 template](../01-whatsapp-ai-chatbot/).
3. **Bookings calendar:** in Google Calendar, create a new calendar for bookings and set its **time zone to where your business is**.
4. **Workflow time zone:** **⋯** → **Settings** → **Timezone** → the same time zone → **Save**. The template uses America/New_York.
5. **Check calendar** and **Book appointment:** open each one, connect Google (on n8n Cloud: **Sign in with Google**), and pick your bookings calendar. The fields marked **Defined by agent** are filled in by the AI. Leave them.
6. **AI Agent → Options → System Message:** replace Bella's Hair Studio (an example business) with your own hours, prices, services and how long each one takes. Keep the first line (today's date and time zone) and the booking rules.
7. Click **Publish**, then message your test number: "Can I book a haircut tomorrow at 3?"

## If a booking lands at the wrong time

Three things must use the same time zone: the **calendar**, the **workflow settings**, and the **first line of the system message**. In our first test, before that line existed, the AI booked noon instead of 4 PM.

## If nothing happens

See "If nothing happens" in the [Episode 1 template](../01-whatsapp-ai-chatbot/). Usually the workflow isn't Published, or the Meta app isn't subscribed to your WhatsApp Business Account.

## Before real customers use it

- **Watch the first bookings** on day one, and tweak the rules if needed.
- **Double bookings:** if two customers grab the same slot at the same second, both could get it. It's rare for a small business. The rule "check the calendar right before booking" makes it rarer.
- **Tell customers it's an AI**, and give them a way to reach a person. WhatsApp allows business assistants for bookings.
- **Cancelling and moving bookings** aren't built in. The bot says the team will reply.
- **Self-hosted n8n:** "Sign in with Google" is n8n Cloud only. Self-hosted n8n needs its own Google OAuth app.

Not affiliated with WhatsApp, Meta, n8n or Google. Made by Bot Playbook (SystemSync AI).
