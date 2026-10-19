# del Trades

A lightweight web app for Deriv built to run on Vercel. It has a static front end and two small serverless functions.

## Features

- **Market:** live tick prices and a chart for any available symbol
- **Trade:** manual Rise/Fall contracts with live price quotes, plus early sell
- **Bot:** a simple automated trader with stop loss, take profit and a max-trade limit
- **Account:** balance, open positions and recent trade history

## Project structure

```
deriv-app/
├── index.html        # the whole front end
├── api/
│   ├── otp.js        # gets an authenticated WebSocket URL from Deriv
│   └── accounts.js   # lists your Deriv accounts
└── README.md
```

## Setup

1. Go to https://developers.deriv.com and register a **PAT-type** application. Legacy App IDs do not work with the new API.
2. Create a Personal Access Token (PAT) with the `trade` scope. Copy it somewhere safe, because it is shown only once.
3. Deploy to Vercel:
   - Push this repo to GitHub.
   - In Vercel, choose **Add New > Project**, select the repo, and click **Deploy**.
4. In Vercel, open **Settings > Environment Variables** and add:

   | Name | Value |
   |------|-------|
   | `DERIV_APP_ID` | your new App ID |

5. Go to **Deployments**, open the latest one, and click **Redeploy**.

## Usage

1. Open your Vercel URL. The status label (top right) should show "live (public)" and prices should stream in the Market tab.
2. Paste your PAT, click **Load accounts**, choose a **demo** account, and click **Log in**.
3. Use the Trade, Bot and Account tabs.

## Security notes

- Your PAT is held in browser memory only and is never saved.
- The PAT is sent only to this app's own `/api` routes, which call Deriv on your behalf. Your App ID stays on the server.
- Real-money trades ask for confirmation, and the bot needs an explicit checkbox before it runs on a real account.
- Always test on a demo account first.

## Troubleshooting

| Problem | Likely cause |
|---------|--------------|
| `401 Unauthorized` | Legacy App ID, wrong token type, or missing `DERIV_APP_ID` |
| `403 Forbidden` | Token created without the `trade` scope |
| No market data | The public WebSocket URL may differ. Update `PUBLIC_WS` in `index.html` using Deriv's "WebSocket public" docs page |
| Account dropdown empty | Type your account ID manually |

## Disclaimer

Trading involves risk of loss. This project is provided as is, with no guarantee of profit. The bot strategies are examples and have no proven edge. This project is not affiliated with Deriv.

## Resources

- Deriv API docs: https://developers.deriv.com
- Vercel docs: https://vercel.com/docs
