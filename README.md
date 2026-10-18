# Quote Follow-Up (Lite): free n8n workflow for Australian businesses

Sent a quote and heard nothing? This sends the customer one polite check-in SMS a few days later, on a weekday, inside your hours.

- Webhook in (`/webhook/quote-lite/sent`) → one follow-up SMS via Twilio after `followUpAfterDays`
- Skips the follow-up if the customer has already replied to your number
- AU number normalisation (04xx → +614xx); only texts mobiles
- Weekday sending window in your timezone
- STOP/START opt-out handling (Spam Act 2003: business name + "Reply STOP to opt out" in every text)
- Daily SMS cap and optional webhook secret (`sharedSecret`)

Tested end-to-end in n8n with simulated APIs (a local mock of the Twilio API); no live SMS or email provider was used in testing.

## Setup (about 15 minutes)
1. n8n → **Import from file** → `workflow/quote-follow-up-lite.n8n.json`.
2. Open **Decide** and set `businessName`, `sms.from` (your Twilio AU mobile in +61 format) and `sms.twilioAccountSid`.
3. On **Send SMS (Twilio)**, add an HTTP Basic Auth credential: User = Account SID, Password = Auth Token.
4. Activate. Set your Twilio number's **Messaging** webhook to `https://<your-n8n>/webhook/quote-lite/sms-inbound`.
5. When you send a quote, POST `{"name":"Jo","phone":"0491 570 006","jobType":"fence"}` to `https://<your-n8n>/webhook/quote-lite/sent`.

Costs (Twilio, Oct 2026): about US$0.0515 (≈A$0.074) per SMS and US$8.25/month (≈A$11.90) for an AU mobile number.

## Want more?
The **Pro pack** adds:
- a 3-step chase (SMS → email → "valid until" SMS) counted in **business days**, skipping public holidays and the Christmas closedown
- "Reply YES" acceptance with an owner alert and customer thank-you
- other replies forwarded to your mobile with the quote reference
- email with one-click unsubscribe, A$ amounts with GST, quote links and validity dates
- won/lost updates from your system, a status page with win rate and open quote value
- ClickSend support and dry-run mode
- AU compliance notes, setup docs and test scripts

**Want the full Australian version?** The Quote Follow-Up Pack (Pro) adds the full business-day chase, YES acceptance, reply forwarding, email, ClickSend and full setup docs. Store link coming soon; questions to aussieflows@mail.grokbot.com.

[Notify me when Pro is out](mailto:aussieflows@mail.grokbot.com?subject=Notify%20me%20-%20Quote%20Follow-Up%20Pack).

Rather not set this up yourself? A done-for-you managed service (we set up, monitor and maintain these automations for your business; AU, from A$99/month) is being considered. [Join the waitlist](mailto:aussieflows@mail.grokbot.com?subject=Hosted%20waitlist%20-%20Quote%20Follow-Up%20Pack). One email if it goes ahead or doesn't, then your address is deleted.

## More free AU workflows
Other free n8n workflows for Australian small businesses (MIT, same setup style):
- [Missed-Call Text-Back](https://github.com/fletcheri/n8n-missed-call-textback): text back missed callers in seconds
- [Google Review Request](https://github.com/fletcheri/n8n-google-review-request): one honest Google review ask after each job
- [Booking Reminder](https://github.com/fletcheri/n8n-booking-reminder): a reminder SMS before each booking
- [Overdue Invoice Reminder](https://github.com/fletcheri/n8n-overdue-invoice-reminder): an overdue-invoice email a week after the due date

MIT licence. Not legal advice.
