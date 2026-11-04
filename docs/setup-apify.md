# Set up Apify for these workflows

1. Create an account at https://console.apify.com/sign-up.
2. Copy an API token from https://console.apify.com/settings/integrations.
3. In n8n, create a **Query Auth** credential named `Apify API Token`:
   - Name: `token`
   - Value: your Apify token
4. Select it in the **Run Apify Actor** node of each workflow you import.

Apify's free plan includes a monthly usage credit. Each Actor's Pricing tab shows what a run costs.

Never put the token in the workflow JSON. Keep it in the n8n credential.
