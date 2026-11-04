# Import a workflow

1. Open a workflow page in `docs/` and copy its raw JSON link (or download the file from `workflows/`).
2. In n8n, open a new workflow and choose **⋯ → Import from URL** (or **Import from file**).
3. Open **Run Apify Actor** and select the `Apify API Token` credential.
4. Edit **Configure input**.
5. Click **Execute workflow**.

The Google Sheets node is disabled by default. Enable it after adding a Google Sheets credential and sheet ID.
