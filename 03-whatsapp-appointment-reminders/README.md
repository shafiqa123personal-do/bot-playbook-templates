# WhatsApp Appointment Reminders: free n8n templates (Bot Playbook, Episode 3)

Every morning at 10, n8n reads tomorrow's bookings and sends each customer who said yes a WhatsApp reminder: "Hi Alex! This is Bella's Hair Studio with a reminder: your men's haircut is tomorrow at 4:00 PM." These are the exact workflows built in the video. There are two files:

| File | What it is |
|---|---|
| [`whatsapp-ai-booking-bot-with-reminders.json`](whatsapp-ai-booking-bot-with-reminders.json) | The Episode 2 booking bot, plus the reminder question. Before booking, it asks "Can Bella's Hair Studio send you a WhatsApp reminder the day before?" and saves the answer in the booking ("Reminder: yes" or "no"). |
| [`appointment-reminders.json`](appointment-reminders.json) | The new reminders workflow. |

```
Every day at 10 AM → Tomorrow's bookings (Google Calendar) → Said yes to reminders (Filter)
                   → Reminder details (Edit Fields) → Send reminder (WhatsApp template)
```

## Set it up in 20 minutes

1. **Booking bot:** import `whatsapp-ai-booking-bot-with-reminders.json` (or add the two sentences and the Reminder expression to your Episode 2 workflow). Set it up like the [Episode 2 template](../02-whatsapp-ai-booking-bot/).
2. **Template message:** in WhatsApp Manager, go to **Message templates** → **Create template**. Choose category **Utility**, name `appointment_reminder`, language **English**. Use this body:
   ```
   Hi {{1}}! This is Bella's Hair Studio with a reminder: your {{2}} is tomorrow at {{3}}. See you at 142 Maple Street. Need to change it? Just reply to this message.
   ```
   Change the business name and address to yours. Give the examples Alex, men's haircut and 4:00 PM, then submit it. It must be **Active** before n8n can send it.
3. **Import the reminders workflow:** **⋯** → **Import** → **From URL**:
   ```
   https://raw.githubusercontent.com/shafiqa123personal-do/bot-playbook-templates/main/03-whatsapp-appointment-reminders/appointment-reminders.json
   ```
4. **Workflow time zone:** **⋯** → **Settings** → **Timezone** → your business's time zone → **Save**. The template uses America/New_York. Change it in **Reminder details** too, in the `time` field, and in the calendar node's **Timezone** option.
5. **Tomorrow's bookings:** connect Google and pick your bookings calendar.
6. **Send reminder:** use your WhatsApp account from Episode 1. Set **Sender Phone Number** to your number, then pick **appointment_reminder** under **Template**. Keep the three Body parameters **in this order**: name, service, time.
7. **Test:** make a test booking for tomorrow and say yes to the reminder. Then click **Execute workflow**: the reminder arrives straight away.
8. **Publish:** from then on it runs every day at 10 AM.

## If something goes wrong

- **"Bad request" from WhatsApp:** the parameters don't match the template. Check that there are three, in the order name, service, time, and that the template is Active.
- **The wrong time in the reminder:** the workflow settings, the calendar node and the `time` field must all use your business's time zone.
- **Nobody gets a reminder:** open **Said yes to reminders**. Only bookings whose description contains `Reminder: yes` get through. Bookings made before you added the reminder question don't have it.

## Before real customers get reminders

- **It costs money.** Reminders are paid utility template messages, priced per message by the customer's country, from a fraction of a cent to a few cents. Check Meta's rate card: https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing
- **Permission comes first.** Only send to people who said yes. If customers also book by phone or on your website, mention reminders there too, and follow your local privacy rules. Meta's rules: https://developers.facebook.com/documentation/business-messaging/whatsapp/getting-opt-in
- **One plain reminder, no offers.** Offers can turn it into a marketing message, which costs more and needs different permission.
- **Moving and cancelling** aren't built in yet. The bot says the team will reply.

Not affiliated with WhatsApp, Meta, n8n or Google. Made by Bot Playbook (SystemSync AI).
