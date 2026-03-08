# v0 Frontend Prompt — AI Meeting Prep Assistant

Paste this prompt into v0.dev. Replace `[YOUR_WEBHOOK_URL]` with your n8n webhook URL before generating.

```
Build a clean, minimal AI Meeting Prep Assistant web app.

What it does:
- User uploads an Excel file (.xlsx) containing their prospect list
- App sends the file to an n8n webhook for processing
- When results come back, user can download the enriched Excel file with briefs added

Webhook:
POST to: [YOUR_WEBHOOK_URL]
Send the file as multipart/form-data with the field name "file"
Wait for the response which will be a downloadable Excel file

UI Layout:
- Centered, single page layout
- App title: "AI Meeting Prep Assistant"
- Subtitle: "Upload your prospect list and get AI-generated meeting briefs in seconds"
- A clean file upload zone (drag and drop + click to upload), accepts .xlsx only
- A "Generate Briefs" button — disabled until a file is uploaded
- A loading state while waiting: "Generating briefs for your prospects... this may take a moment"
- On success: a "Download Results" button that downloads the returned Excel file
- On error: a simple error message with a retry option

Design:
- Clean and professional, dark background with blue and purple colors
- Minimal — no sidebars, no complexity
- The upload zone should show the filename once a file is selected
```
