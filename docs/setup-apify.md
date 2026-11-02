# Setup Apify

1. Create an account at https://console.apify.com/sign-up.
2. Open https://console.apify.com/account#/integrations and copy an API token.
3. In n8n, create a **Query Auth** credential named `Apify API Token`:
   - Name: `token`
   - Value: your Apify token
4. The free Apify plan includes monthly usage credit. Check the actor page for pricing.

Never commit your token. Use n8n credentials, not workflow JSON.
