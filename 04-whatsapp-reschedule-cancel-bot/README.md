# WhatsApp AI Booking Bot: move and cancel by chat. Free n8n template (Bot Playbook, Episode 4)

A customer writes "Can I move it to 5 PM?" or "I need to cancel Thursday". The bot finds their booking, checks the calendar, asks them to confirm, then moves or cancels it. It can only find bookings made from the WhatsApp number it's talking to. This is the exact workflow built in the video.

| File | What it is |
|---|---|
| [`whatsapp-ai-booking-bot-move-cancel.json`](whatsapp-ai-booking-bot-move-cancel.json) | The Episode 3 booking bot, plus three new Google Calendar tools and the rules for changes. |

The AI Agent's five tools:

| Tool | Google Calendar | Filled in by |
|---|---|---|
| Check calendar | Calendar → Availability | the AI: start and end |
| Book appointment | Event → Create | the AI: start, end, service, reminder yes or no |
| **Find my bookings** | Event → Get Many, upcoming 60 days, Limit 10 | **nobody.** Its Query is the sender's WhatsApp number, straight from the WhatsApp Trigger |
| **Move booking** | Event → Update, Start and End | the AI: Event ID, new start and end |
| **Cancel booking** | Event → Delete | the AI: Event ID |

## Set it up in 20 minutes

1. **Import:** in n8n, open a new workflow, then **⋯** → **Import** → **From URL**:
   ```
   https://raw.githubusercontent.com/shafiqa123personal-do/bot-playbook-templates/main/04-whatsapp-reschedule-cancel-bot/whatsapp-ai-booking-bot-move-cancel.json
   ```
2. **Connect your accounts,** as in the [Episode 2 template](../02-whatsapp-ai-booking-bot/):
   - WhatsApp Trigger and Send reply: your WhatsApp app
   - Google Gemini Chat Model: your Gemini key
   - Save lead: your Google Sheet
   - the five calendar tools: your Google account and your bookings calendar
3. **Time zone:** **⋯** → **Settings** → **Timezone** → your business's time zone → **Save**. The template uses America/New_York. Change it in **Check calendar** and **Find my bookings** too.
4. **Your business:** in the **AI Agent**'s System Message, replace Bella's Hair Studio's hours, prices and services with yours. Keep the booking and change rules.
5. **Test** on your own phone. Book something, then ask to move it, then ask to cancel it.
6. **Publish.**

## The rules for changes, already in the System Message

- To move or cancel, first use Find my bookings, and only change bookings it returns. Never mention anyone else's.
- Nothing less than 24 hours away: the team replies. This is the example salon's policy, so change the number to yours.
- To move, check the calendar, then repeat the old and new day and time, and wait for yes.
- To cancel, repeat the service, day and time, and wait for yes.

## Before real customers use it

- **Keep the lock.** The Query in **Find my bookings** must stay an expression from the WhatsApp Trigger. Never let the AI fill it in, or a stranger could ask it to look up someone else's bookings.
- **Every change needs a yes.** Deleted bookings stay in Google Calendar's bin for 30 days, so mistakes can be undone.
- **Late changes go to people.** Fees and exceptions are for your team, not the bot.
- **Bookings made by hand.** The bot only finds bookings with the customer's WhatsApp number in the description. When your team books someone by phone, add their number there too.
- **Use a capable model.** In our tests, the lightest Gemini model sometimes named the wrong day or skipped the confirmation. Gemini Flash got it right.

## If something goes wrong

- **"I can't find a booking from this WhatsApp number" for a real customer:** their booking has no WhatsApp number in its description. It was probably made by hand, or before Episode 3.
- **A booking moves to the wrong time:** check the time zone in the workflow settings and in the calendar tools.

Not affiliated with WhatsApp, Meta, n8n or Google. Made by Bot Playbook (SystemSync AI).
