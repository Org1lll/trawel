# Deploying You & Me Travel to Cloudflare

This is a static website: one HTML page, no server code, no build step.
Cloudflare hosts it for free on **your own** Cloudflare account.

```
public/index.html   <- the website (edit this file to change the site)
wrangler.jsonc      <- tells Cloudflare to serve the public/ folder
```

You only need to pick **one** of the three options below.

---

## Option 1 — Drag and drop (easiest, no tools)

1. Go to <https://cloudflare.com/drop>.
2. Drag the **`public`** folder onto the page (or zip it and upload the zip).
3. You get a temporary preview link. It only lives for **1 hour**.
4. Click **Claim**, then sign in to your Cloudflare account (or create one and
   verify your email). The site is now permanently yours.

To update the site later, use Option 2 or 3. Drag-and-drop is best for a
first try.

---

## Option 2 — Connect GitHub (updates automatically on every push)

1. Put this project in **your own** GitHub account (fork it, or create a new
   repository and upload these files).
2. Log in at <https://dash.cloudflare.com> and open **Workers & Pages**.
3. Click **Create application**, then **Get started** next to
   **Import a repository**.
4. Connect your GitHub account when asked, then pick your repository.
5. Check the settings:
   - **Project name:** `you-me-travel`
     (it must match `"name"` in `wrangler.jsonc`, or the build fails)
   - **Build command:** leave empty
   - **Deploy command:** `npx wrangler deploy` (the default)
6. Click **Save and Deploy**.

Your site will be at `https://you-me-travel.<your-subdomain>.workers.dev`.
Every time you push a change to GitHub, Cloudflare redeploys it.

---

## Option 3 — Command line

Requires [Node.js](https://nodejs.org) (version 22 or newer).
Open a terminal in this project folder and run:

```sh
npx wrangler login     # opens the browser - log in to YOUR Cloudflare account
npx wrangler deploy    # uploads the site and prints its URL
```

To preview locally before deploying: `npx wrangler dev`, then open
<http://localhost:8787>.

---

## Good to know

- **The booking form does not send anything.** When a visitor submits it, the
  page only shows a "Захиалга Хүлээн Авлаа!" message — no name or phone number
  is saved or emailed. Connect it to a form service (or remove the success
  message) before using the site for real customers.
- **Changing the address:** rename `"name"` in `wrangler.jsonc` (and the
  Worker name in the dashboard, if you used Option 2). A custom domain can be
  added later: **Workers & Pages** → select the Worker → **Domains** tab.
- **Browser console warning about Tailwind:** the page loads Tailwind CSS from
  `cdn.tailwindcss.com`, which prints a "should not be used in production"
  warning. The site still works; it is just a heads-up.
