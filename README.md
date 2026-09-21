# Meta Transform with AI — Phase 2

Official registration landing page and automation workflows for **Meta Transform with AI (Phase 2)** by **WYLDE International** in partnership with **Meta** and **SNDBX**.

---

## 🚀 Overview

- **Live Subdomain:** `meta.wyldeinternational.com`
- **Hosting Platform:** Vercel (Static Web Architecture)
- **Webinar ID:** `849 6724 7381` (Zoom Webinar)
- **Registration Database:** Google Sheets (`Registrations` tab)

---

## 📁 Repository Structure

```
├── index.html                           # Landing page with high-conversion registration form & testimonials
├── logo-meta.png                        # Official Meta logo
├── logo-sndbx.png                       # Official SNDBX logo
├── logo-wylde.png                       # Official WYLDE International logo
└── workflows/
    ├── WF-A-registration-workflow.json  # Real-time registration webhook -> Google Sheets & Zoom Webinar sync
    └── WF-B-sms-reminder-workflow.json  # Scheduled Monday 9:00 AM SMS reminder via Advanta API
```

---

## ⚡ Architecture & Automation Flow

### Workflow A: Real-Time Registration & Zoom Sync (`WF-A`)
1. Visitor fills the form on `meta.wyldeinternational.com` and clicks **"Complete Free Registration"**.
2. Form posts payload to n8n webhook (`/webhook/meta-transform-register`).
3. **Data Formatting & Validation:** Formats phone number into standard Kenyan international format (`2547XXXXXXXX`), captures timestamp, business sector, and training expectations.
4. **Google Sheets Sync:** Appends row to the primary Google Sheet tab (`Registrations`).
5. **Zoom Webinar Registration:** Calls Zoom API to register the participant into Webinar `849 6724 7381`.
6. **Sheet Update:** Writes back `Zoom Status: REGISTERED` and the participant's unique `Zoom Join URL`.

### Workflow B: Weekly SMS Session Reminders (`WF-B`)
1. Triggers every **Monday at 9:00 AM EAT**.
2. Reads confirmed registrants from Google Sheets.
3. Filters for valid phone numbers.
4. Dispatches personalized SMS reminder with Zoom access links via **Advanta SMS Gateway**.

---

## 🌐 Deployment Guide (Vercel)

1. Connect this repository to **Vercel**.
2. Framework Preset: **Other** (Static HTML).
3. Root Directory: `./`
4. Click **Deploy**.
5. In **Project Settings > Domains**, add:
   ```
   meta.wyldeinternational.com
   ```
6. In **SureServer DNS Manager** for `wyldeinternational.com`:
   - **Type:** `CNAME`
   - **Host:** `meta`
   - **Value:** `cname.vercel-dns.com`
