\# RB-002 — Invalid Client Secret (OIDC token exchange failure)



\## When to use

User reaches Microsoft sign-in and consents successfully, but the app fails when exchanging the auth code for tokens.



\## Symptoms

\- App shows:

&nbsp; - “Token exchange failed (check redirect URI / secret).”

\- In the terminal where `node server.js` is running, you may see:

&nbsp; - `invalid\_client`

&nbsp; - \*\*AADSTS7000215\*\* (invalid client secret)

\- Entra \*\*Sign-in logs\*\* may show a failed token request / client auth failure.



\## Most likely cause

The app is using the wrong secret:

\- `.env` still has placeholder text

\- secret \*\*Value\*\* was not copied (only the secret ID)

\- secret expired

\- secret rotated in Entra but `.env` not updated



\## Quick checks (2 minutes)

1\) Check `.env`:

&nbsp;  - Confirm `CLIENT\_SECRET` is not a placeholder.

&nbsp;  - It must be the \*\*secret VALUE\*\*, not secret ID.



2\) Check expiry in Entra:

&nbsp;  - Entra ID → App registrations → your app

&nbsp;  - \*\*Certificates \& secrets\*\* → Client secrets

&nbsp;  - Confirm the secret is not expired.



3\) Confirm in logs:

&nbsp;  - Entra ID → \*\*Audit logs\*\*

&nbsp;  - Look for “Certificates and secrets management” events (new secret added / removed).



\## Fix (step-by-step)

1\) Create a new secret in Entra:

&nbsp;  - App registrations → your app → \*\*Certificates \& secrets\*\*

&nbsp;  - \*\*New client secret\*\*

&nbsp;  - Set a short expiry (3–6 months for demo hygiene)

&nbsp;  - Click \*\*Add\*\*

&nbsp;  - Copy the \*\*Value\*\* immediately (you cannot view it again later)



2\) Update `.env`:

&nbsp;  - Replace `CLIENT\_SECRET=...` with the new secret \*\*Value\*\*

&nbsp;  - Save the file



3\) Restart the app:

&nbsp;  - Stop with `Ctrl + C`

&nbsp;  - Start: `node server.js`



4\) Retest:

&nbsp;  - Open `http://localhost:3000`

&nbsp;  - Click \*\*Sign in\*\*

&nbsp;  - Confirm you return to `/` with \*\*Status: Signed in\*\*



5\) Cleanup (security hygiene):

&nbsp;  - Delete the old secret in Entra (if it’s no longer needed)

&nbsp;  - Record the change in notes (who/what/when)



\## Prevention

\- Never commit `.env` to GitHub (ensure `.gitignore` includes `.env`)

\- Rotate secrets with a controlled change plan (update app config + restart + validate)

\- Prefer short-lived secrets; rotate after exposure or sharing

