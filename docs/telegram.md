---
sidebar_position: 2
title: Polycatch
---

Polycatch is a **Telegram bot for monitoring Polymarket activity** and helping you act on signals quickly. This page explains what the bot does, how to get started in Telegram, and what each command is for.

## What Polycatch does

- **Monitoring**: watches Polymarket-related on-chain activity and surfaces notable events (e.g., high-value deposits).
- **Trading UX**: lets you place trades from Telegram with structured, button-driven flows.
- **Position management**: shows your active positions and lets you sell via market or limit orders.

## Getting started (in Telegram)

Get started by visiting the bot: [https://t.me/polycatch_bot](https://t.me/polycatch_bot)

1) Open the Polycatch bot chat and run **`/start`**  
2) Create your encrypted account with **`/setup`**  
3) Unlock your session with **`/unlock`** (required for anything that uses your credentials)  
4) Start monitoring with **`/monitor`** (so the bot can surface signals and enable trading dashboards)

## Setup: what you’ll enter and why

### `/setup` (first-time account creation)

`/setup` creates your Polycatch account and stores your credentials **encrypted at rest**.

You’ll be prompted for:

- **Encryption password**
  - **What it’s for**: encrypts your sensitive credentials on disk.
  - **Important**: it is **never stored** and cannot be recovered. If you lose it, you must `/delete` and `/setup` again.

- **Signer private key**
  - **What it’s for**: signs Polymarket orders (this is how the bot proves you authorized an order).
  - **Recommendation**: use a dedicated wallet for trading (not your main wallet).

- **Funder address (Polymarket proxy wallet address)**
  - **What it’s for**: identifies the account that holds collateral and positions on Polymarket (used for balance/positions).
  - **Tip**: this is your Polymarket “proxy wallet/profile” address (not necessarily the same as your MetaMask EOA).

During setup, Polycatch also **generates Polymarket API credentials** for you (API key/secret/passphrase) based on your signer key. These are needed for authenticated Polymarket API calls (placing orders, listing/canceling orders, etc.).

## In-chat setup flow

### `/unlock` and `/lock` (sessions)

- **`/unlock`**: decrypts your credentials into memory and starts a session (default 30 minutes)
  - You can also provide the password inline: `/unlock <password>`
- **`/lock`**: immediately clears credentials from memory

Many actions (trading, monitoring, balance fetches) require an active session.

## Command reference

### Account & security

- **`/start`**: onboarding message and next steps
- **`/help`**: prints the command list
- **`/status`**: shows account info, session status, and **USDC balance**
  - Balance is fetched on-chain from the configured funder address (USDC `balanceOf`)
- **`/delete`**: deletes your Polycatch account (credentials + history + settings)
- **`/cancel`**: cancels the current operation (setup flows, prompts, etc.)

### Monitoring

- **`/monitor`**: starts background monitoring (deposits + insider signals)
  - Requires an unlocked session
  - Requires Polygon WS connectivity (`POLYGON_WSS_URL`)
- **`/stop`**: stops monitoring

### Trading dashboards

- **`/trade`** (alias: **`/positions`**): shows your **active positions** and lets you sell them
  - Shows your current **USDC balance**
  - For each position you can choose:
    - **Market Sell**: `FAK` or `FOK`
    - **Limit Sell**: `GTC` or `GTD`
      - `GTD` requires choosing an expiry
      - You’ll be prompted to enter a limit price in **cents** (e.g. `55` for 55¢)

- **`/trades`**: shows your **trading dashboard**
  - Active Positions (with sell buttons)
  - Active Orders (with cancel buttons)
  - Refresh button

### Crypto markets

- **`/crypto`**: opens the BTC 15-minute Up/Down market UI
  - You can place:
    - **Market buys** (immediate): `FAK` / `FOK`
    - **Limit buys**: `GTC` / `GTD`
  - The bot will guide you through outcome selection, amount selection, order type selection, and confirmation.

