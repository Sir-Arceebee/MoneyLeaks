---
name: money-leaks
description: Scans the student's email for free trials about to charge, forgotten subscriptions, duplicates, price hikes and missed student discounts, then reports the monthly leak total. Use whenever the student asks where their money is going, says "check my subscriptions", "money leaks", "am I wasting money", "what am I paying for", "why is my bank account empty", mentions a free trial, an unexpected charge, a renewal or a student discount, or a new trial or renewal email arrives. Also runs the 48 and 24 hour pre-charge warnings, the "saved so far" tracker and the Sunday money check-in it sets up.
---

# Money Leaks

Students lose money quietly: trials that auto-convert, subscriptions they forgot, two services doing the same job,
price increases and student discounts they never claimed. Money Leaks finds those leaks in the student's billing
emails, leads with one number ("You're leaking about $X/month"), warns before charges hit, helps the student cancel
or switch, and celebrates every dollar saved.

This Skill uses only Cubbie's built-in abilities. It has no scripts and no server. Cubbie never cancels, logs in,
pays or changes any account; the student does that themselves.

## When to use

- "where's my money going" / "am I wasting money" / "money leaks" / "check my subscriptions"
- "what am I even paying for" / "my bank account is empty again" / "I got charged $14.99 by something??"
- "is there a student discount for Spotify?" / "my Hulu trial is ending"
- "I cancelled Hulu" / "switched to the student plan" (log a win)
- "keep Netflix, I use it" (mark as kept)
- Proactively, only inside the check-ins the student agreed to (see Alerts and check-ins).

Do not use it for budgeting advice, investing, loans, taxes or splitting bills with friends. Never log in to bank
accounts or move money.

## Abilities used

- Email (connected Gmail, and the email events Cubbie extracts from it): search and read billing messages only.
- Google Calendar (connected): find free times for alerts.
- Reminders and scheduled check-ins: the pre-charge alerts and the Sunday summary.
- Memory: the student's leak list, kept items, alert settings and the "saved so far" total.
- Web search: verify student-plan prices and find official cancel and student-plan pages.
- Documents: a PDF or spreadsheet when the full list is long.

If Gmail is not connected, text: "I need your Gmail connected to find subscriptions. Want to connect it now?" and
stop. Offer the fallback: the student can forward or screenshot receipts and Cubbie reads those instead.
If Calendar is not connected, still offer alerts and send them at the default times below.

## Steps

### 1. Scan (first run, or when the student asks again)

1. Search the student's email from the last 13 months (so annual plans show up) for billing-type messages only:
   receipts, invoices, renewal notices, trial notices, price-change notices, cancellation and refund confirmations.
   Search with phrases like "receipt", "invoice", "your subscription", "free trial", "will be charged", "renews",
   "membership", "price change", "payment confirmation", "order confirmation", "cancelled", "refund".
2. Skip everything else. Do not open or quote personal, school, work or social email. If a message is not clearly
   about a charge, a plan or a trial, ignore it.
3. Group messages by service (the sender's company). For each service record only what the emails say: plan name,
   amount, currency, billing cycle, last charge date, next charge or trial end date, and whether it is cancelled.
4. Classify each service with the heuristics below. One service can match several; keep all its flags.
5. Check Memory first: drop services the student already marked "keep" (unless the price went up), already-logged
   wins, and services already cancelled.
6. For each "missed student discount", search the web for the provider's official student plan. Use a price only if
   the provider's own page shows it today; otherwise say "student plan available, check current price".
7. Do the math (see Money math), rank leaks by yearly cost, soonest charge first on ties.
8. Save the leak list to Memory with today's date.
9. Reply in the First reply format.
10. After the student has seen the list, offer alerts and the Sunday check-in (one question, default yes).

### 2. Help the student act

When the student picks a leak ("help me cancel Hulu", "switch me to student"):
1. Search the web for the provider's official cancel page or student-plan page. Link only to the provider's own
   domain (spotify.com, apple.com, amazon.com...). Never use a link from an email you are not sure is genuine.
2. Send the link on its own line plus 2 to 4 short steps. Mention the student-verification step (often through
   SheerID or UNiDAYS with the student's school email) when the provider uses one.
3. Say the student does it; Cubbie can't cancel or pay. Then ask them to text "done" when it's finished.

### 3. Log a win

When the student says they cancelled, switched or downgraded:
1. Saved amount: cancel = the yearly cost of that service; switch or downgrade = (old monthly − new monthly) × 12,
   using the new price only if the student or an email or the provider's page confirmed it. If the new price is
   unknown, log the win and ask "What's the new price? I'll add it to your total."
   A trial cancelled before it converted saves its first-year cost.
2. Add it to "saved so far" in Memory (keep a list: service, what changed, date, $/yr).
3. Celebrate in the Win reply format. Later, if a cancellation confirmation email shows up, note it quietly. If a new
   charge from that service shows up after the student said it was cancelled, flag it kindly and remove it from the
   total only after the student confirms.

### 4. Mark as kept

When the student says they still use something ("keep it", "I use that daily"): mark it "keep" in Memory, say so in
one line, and stop flagging it. Re-flag it only if its price goes up or a cheaper student plan is confirmed.

## Detection heuristics

Free trial converting
- "your free trial ends on", "trial ends in 3 days", "after your trial, you'll be charged", "you won't be charged
  until", "start your free trial", "your trial is about to end", "first payment on".
- Record the conversion date and amount. If the email gives "ends in 7 days" with no date, count from the email's
  date and say "around Nov 2".

Active subscription
- "thanks for subscribing", "your receipt from", "payment received", "your membership has renewed", "your plan
  renews on", "auto-renew", "billing period", "next billing date", "invoice for your subscription".
- Active = a charge in the last cycle and no cancellation since. Two or more charges at a steady interval give the
  billing cycle.

Price increase
- "your price is changing", "new price", "price update", "we're updating our pricing", "starting with your next
  bill", "your monthly price will be".
- Record old price, new price, start date. The leak is the difference.

Duplicate service
- Two or more active services in one group: music (Spotify, Apple Music, YouTube Music, Amazon Music Unlimited,
  Tidal), video (Netflix, Hulu, Disney+, Max, Peacock, Paramount+, Prime Video add-ons), cloud storage (iCloud+,
  Google One, Dropbox, OneDrive), AI chat tools, VPNs, password managers, food delivery memberships (DashPass,
  Uber One, Grubhub+), shipping memberships (Amazon Prime, Walmart+).
- Bundles are not duplicates: Spotify Premium Student includes Hulu (With Ads) in the US; Apple One includes Apple
  Music and iCloud+; Google One may come with YouTube or Pixel offers. If unsure whether it is a bundle, ask.

Possibly unused (always "possible", always ask)
- Renewal receipts arrive, but no other email from that service in 60+ days: no "new episodes", "your weekly
  playlist", "your order shipped", "someone shared a file", login alerts, activity digests.
- Never claim the student doesn't use it. Ask: "Do you still use Hulu? Last renewal was Oct 3."

Missed student discount
- The student pays a regular or individual price for a service with a known student offer, such as Spotify Premium
  Student, Apple Music student, YouTube Premium student, Amazon Prime Student, Adobe Creative Cloud for students,
  GitHub Student Developer Pack (free), Notion for education (free Plus plan), Microsoft 365 for students, Canva
  for Education, and student plans at news sites.
- Signals: the receipt says "Individual", "Premium", "Personal", "Monthly" and not "Student" or "Education".
- Check the offer on the provider's page before claiming it. Offers change and differ by country.

Not a leak (exclude, or note in one line)
- "your subscription has been cancelled", "you've cancelled", "your plan will end on" → note it ends and when.
- "refund issued", "we've refunded" → exclude that charge; if the whole subscription was refunded, drop it.
- One-time purchases (a single order, a ticket, a textbook) are not subscriptions.
- Family or shared plans where the student is a member and receives no receipts: not their cost, skip.
- Suspicious emails ("payment failed, update your card", a sender domain that doesn't match the company, urgent
  threats): never count them, never send their links. Tell the student it looks like possible phishing.

## Money math

- Use only amounts found in emails, on the provider's page, or given by the student. Never guess a price.
- Monthly cost: monthly = amount; yearly plan = amount ÷ 12; quarterly = amount ÷ 3; weekly = amount × 52 ÷ 12.
  Yearly cost = monthly × 12 (or the yearly amount itself). Show cents for items.
- Leak amount per item (count each service once, using its largest leak):
  - trial about to convert, possibly unused, or recommended to cancel: its full monthly cost
  - duplicate: the cost of the one suggested to drop (the cheaper one, unless the student says otherwise)
  - price increase only: new price − old price
  - missed student discount: full price − verified student price; $0 in the total if the student price isn't verified
- Headline total: sum of leak amounts, monthly, rounded to whole dollars, with "about". Yearly = monthly total × 12.
- Different currencies: never convert silently. Keep the main total in the student's most common currency and add
  the rest on the same line in their own currency ("about $41/month, plus €9.99"). Convert only with a rate from a
  web search today, and say "approx".
- Taxes: use the charged total from the receipt when shown.

## Leak report format

All replies are plain text, short lines, no Markdown symbols (no #, **, tables or code blocks).

First reply: three short texts.

Text 1, the hook:
You're leaking about $X/month ($Y/year) 💸

Text 2, the top 3 leaks, one per line:
1. Name: $A/mo, reason, next charge Date
2. ...
3. ...

Text 3, the next step:
Want the full list?

Full list (when the student says yes): one block per leak.
Name (possible)  ← "possible" only when uncertain
$amount/cycle, next charge Date
$monthly/mo · $yearly/yr
Action: cancel / switch to student plan / keep / you decide

Up to 6 leaks go in texts. More than 6: make a short PDF or spreadsheet with the full report (name, amount, cycle,
next charge, monthly, yearly, flag, suggested action), send it, and text only the top 3 plus the total.
End the full list with one question, for example "Want help with Hulu first?"

Win reply:
Hulu cancelled ✅
+$95.88/year saved
Saved so far: $239.76/year 🎉

Keep the "Saved so far" line on every win. On round milestones ($100, $250, $500, $1,000 a year) add one fun line
("That's a flight home." / "That's a semester of textbooks.").

## Alerts and check-ins

Offer, then wait for a yes. Never create a check-in the student didn't agree to. Ask once, with a default:
"Want me to watch for new trials and text you 48h and 24h before any trial or big renewal charges? Plus a quick Sunday 6pm recap?"

Pre-charge alerts
- Create two reminders for each trial conversion and each large renewal: 48 hours and 24 hours before the charge.
- Large renewal = $20 or more per charge, or any annual plan. The student can change this ("only over $50").
- When the email gives no time, assume the charge happens at the start of that day, so alerts land early enough.
- Alerts go out between 8 am and 10 pm in the student's time zone. If an alert time falls inside a Calendar event
  (class, exam, meeting), move it to the nearest free time before it. If the 48h and 24h alerts would end up within
  12 hours of each other, send only the 24h one. If the charge is less than 24 hours away when found, tell the
  student right away instead.
- Word each reminder so it makes sense days later, for example:
  "Money Leaks alert: the student's Paramount+ free trial converts to $12.99/month on Fri Nov 7. Check the email for
  a cancellation first; if it is already cancelled, say nothing. Otherwise text: Paramount+ trial charges $12.99
  tomorrow. Keep it or cancel?"

Sunday check-in (weekly, default Sunday 6 pm, student picks)
- Word it as: "Money Leaks weekly check: search the student's billing emails from the last 7 days for new trials,
  subscriptions, price changes, cancellations and refunds; compare with the saved leak list; add alerts for any new
  trial (if alerts are on); then text the summary."
- Summary: at most 4 short lines: new leaks (with amounts), charges coming this week, saved so far.
- If nothing changed and nothing is due, send one line: "Quiet week, no new leaks. Saved so far: $X/year 💰"
- Offer once to stop or move it; "stop money check-ins" removes it.

Daily trial watch (part of alerts, so short trials don't slip past the weekly check)
- When the student turns alerts on, also create a daily check-in at 9 am, worded as: "Money Leaks trial watch:
  search the student's billing emails from the last 24 hours for new free trials, renewal notices and price changes
  not in the saved leak list. If none, send nothing. If found, add 48h and 24h alerts and text one line with the
  service, amount and charge date."
- It stays silent on days with nothing new.

## Replies and tone

- Short. Lead with the number. One idea per text. Links on their own line.
- Friendly, a little playful, never judgmental. Subscriptions are allowed; the goal is "only pay for what you use".
  Say "Want to keep it?" not "You're wasting money on this."
- Ask before assuming, one question at a time, with a default the student can answer with "yes".
- Say "possible" whenever something is a guess, and ask the student to confirm.
- Use emoji sparingly: 💸 for the hook, ✅ and 🎉 for wins.

## Example conversations

1. First scan

Student: where's my money going
Cubbie: You're leaking about $46/month ($552/year) 💸
Cubbie: Top 3:
1. Paramount+ trial: turns into $12.99/mo on Nov 7
2. Spotify: $11.99/mo at full price, student plan available, check current price
3. Hulu (possible): $9.99/mo, no activity emails since July
Cubbie: Want the full list?
Student: yes
Cubbie: Paramount+ (trial)
$12.99/mo, first charge Nov 7
$12.99/mo · $155.88/yr
Action: cancel before Nov 7 if you won't watch it
Cubbie: Hulu (possible)
$9.99/mo, next charge Nov 3
$9.99/mo · $119.88/yr
Do you still use it?
Cubbie: (…3 more…) Want help with the Paramount+ trial first?

2. "I still use that, keep it"

Cubbie: Do you still use Hulu? Last renewal was Oct 3.
Student: yeah i watch it every night lol keep it
Cubbie: Got it, Hulu stays ✅ I won't flag it again unless the price goes up.

3. 24-hour trial warning

Cubbie: Heads up: your Paramount+ trial turns into $12.99/month tomorrow (Nov 7).
Keep it or cancel?
Student: cancel how
Cubbie: Cancel here:
https://www.paramountplus.com/account/
Account > Subscription > Cancel. Text me "done" after.
Student: done
Cubbie: Paramount+ cancelled before it charged ✅
+$155.88/year saved
Saved so far: $155.88/year 🎉

4. Student discount switch

Student: is there a student discount for spotify
Cubbie: Yes. You're on Premium Individual at $11.99/mo.
Spotify's student page shows Premium Student at $5.99/mo right now, and it includes Hulu (With Ads) in the US.
Cubbie: Switch here (you verify with your school email):
https://www.spotify.com/us/student/
Student: switched!!
Cubbie: Spotify switched to Student ✅
+$72.00/year saved
Saved so far: $227.88/year 🎉
Cubbie: Your Hulu might be covered by Spotify Student now. Want to check before Hulu renews Nov 3?

(Prices in this example are illustrations; always use the amounts found in the student's emails and on the
provider's page that day.)

5. Weekly summary (Sunday 6 pm)

Cubbie: Sunday money check 💰
- New: Notion Plus $10/mo, and Notion is free for students with your .edu email
- Coming up: iCloud+ $2.99 on Tue
Saved so far: $227.88/year
Want the Notion link?

6. No leaks found

Student: am i wasting money
Cubbie: Good news: no leaks found 🙌 I found 2 subscriptions (Spotify Student, iCloud+), both look in use.
Want a heads-up before any new free trial charges you?

## Safety rules

- Only report amounts, dates and plans found in emails, on the provider's own page, or told by the student.
  Never invent a price, a date or a student discount.
- Unconfirmed student price: "student plan available, check current price".
- Uncertain items are "possible" and need the student's confirmation.
- Read only billing, receipt, trial and subscription emails. Never open, quote or summarize personal email.
- Never share email contents or the leak list outside this conversation, and never send them to any server.
- Cubbie never cancels, logs in, signs up, pays or changes an account. It gives links and steps; the student acts.
- No financial advice beyond naming charges and options (cancel, switch, keep). No investing, credit, loan or budget
  plans.
- Link only to the provider's official domain. Never forward links from suspicious emails.

## Edge cases

- No billing emails at all: "I couldn't find any subscription emails. If your receipts go to another inbox, forward
  one to this Gmail or send a screenshot."
- Annual plans: show the real amount and date ("$99/yr, renews Mar 12") plus the monthly equivalent; always alert
  48h and 24h before an annual renewal.
- Foreign currency: keep the original currency; see Money math.
- Family or shared plans: if the student pays, say so and suggest checking who else uses it; if they're a member,
  skip. Ask when unclear: "Are you paying for the Spotify Family plan, or on someone else's?"
- Already cancelled: don't count it; mention when access ends, only if it ends within 14 days.
- Refunds: don't count the refunded charge; a full refund plus a cancellation means it's gone.
- Same service from two senders (Apple receipts for several apps, Google Play): split by the app or plan named on
  the receipt.
- Charges bought through Apple or Google: the cancel steps are in the phone's subscription settings, not the app's
  website. Say so.
- Student asks about a charge with no email: say "I don't see an email for that one" and ask for a screenshot.
- Student wants to stop: "stop money leaks" removes its check-ins and alerts; ask before deleting the saved list.
