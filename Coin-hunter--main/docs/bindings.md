1. What “binding” means (simple)

Binding = telling the bot WHERE to listen and WHAT to listen for

Your bot does not scan the whole Telegram universe.

It only reacts when:

- A specific group is bound

- AND optionally specific topics inside that group are bound

- AND the message matches a signal pattern

Think of it like this:

> “Only listen here, only for these types of messages”


2. Crypto binding – how it works

Step A — Bind the group (admin only)

You bind ONE group for crypto signals.

Example conceptually:

/bind crypto <group_id>

What the bot stores internally:

crypto_group_id = -100xxxxxxxx

From now on:

Bot ignores all other groups

Bot only monitors this group


Step B — Bind topics inside that group (optional but recommended)

Inside the bound crypto group, you bind topics:

Example:

/bind topic unfiltered
/bind topic low
/bind topic medium
/bind topic high
/bind topic cto

What the bot stores:

unfiltered_topic_id = 123
low_topic_id        = 124
medium_topic_id     = 125
high_topic_id       = 126
cto_topic_id        = 127

Now the bot knows:

Which risk bucket each signal belongs to

Users can toggle:

✅ Auto-buy High

❌ Auto-buy Low

❌ Auto-buy CTO


Step C — User settings decide what happens

Each user has settings like:

Auto-buy enabled? (yes/no)

Which risk levels allowed?

Buy amount (e.g. 0.01 SOL)

Slippage / speed / TP / SL


So when a signal appears:

1. Bot sees the message

2. Confirms it’s in the bound group

3. Confirms it’s in a bound topic

4. Checks which users:

   - Enabled auto-buy

   - Enabled that topic’s risk level


5. Executes (or skips)


3. Forex binding – how it works (separate but similar)

Forex is NOT Telegram-topic based like crypto.

Forex works via symbol + timeframe binding.


Step A — Enable forex signals globally

Admin enables forex engine:

/enable forex

Bot now starts:

Pulling data from yFinance + backups

On fixed timeframes:

1H

4H


Step B — Bind forex channels (optional)

You may still bind a forex signals group:

/bind forex <group_id>

This group is for:

Sending generated signals

Updates (TP hit, SL hit, trailing stop)


Step C — Forex signals are generated, not copied

Unlike crypto:

Forex signals are computed, not copied from Telegram calls


The bot:

1. Scans pairs (e.g. EURUSD, GBPJPY, XAUUSD)

2. Runs SMC logic:

   - Structure break

   - Liquidity sweep

   - HTF bias (1H / 4H)


3. Generates:

   - Entry

   - SL

   - TP levels


4. Sends signal to bound forex group


4. How users copy crypto vs forex (difference)

Crypto copy logic

User copies Telegram calls

Based on:

Topic

Risk category

Mint address


Forex copy logic

User copies bot-generated signals

Based on:

Pair

Timeframe

Risk profile


Users enable separately:

✅ Crypto auto-buy

✅ Forex copy trade


5. Manual trading (important distinction)

Manual trades:

Do NOT use bindings

They are user-initiated


Flow:

1. User sends mint address

2. Bot fetches:

   - Price

   - Liquidity

   - Supply

   - Authority


3. User clicks:

   - Buy

   - Cancel



Bindings are only for signals, not manual trades.


6. Safety rules baked in

Your bot already follows these rules:

❌ Ignores messages from unbound groups

❌ Ignores topics not bound

❌ Skips if user already holds token (if enabled)

❌ Skips if balance < minimum

✅ Supports Devnet (paper trading) with disclaimer


7. One-line summary

> Crypto binding = listen to one Telegram group + selected topics
Forex binding = bot generates signals → sends to bound forex group
Users decide whether to copy, auto-buy, or ignore


---

Notes:
- This document summarizes how bindings work conceptually and how the bot stores binding information.
- Add to README or admin help commands as needed.
