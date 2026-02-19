\# RB-001 — Redirect URI Mismatch (OIDC)



\## When to use

User clicks \*\*Sign in\*\* and authentication fails after redirect, often showing an AADSTS error page.



\## Symptoms

\- Browser error after Microsoft sign-in, commonly:

&nbsp; - \*\*AADSTS50011\*\* (reply URL / redirect URI mismatch)

\- App may show:

&nbsp; - “Token exchange failed (check redirect URI / secret).”

\- Entra \*\*Sign-in logs\*\* show failure for the app around the same timestamp.



\## Most likely cause

The app’s `REDIRECT\_URI` does not exactly match the Redirect URI configured in the Entra App Registration.

Even small differences break it: `localhost` vs `127.0.0.1`, wrong path, missing port, trailing slash.



\## Quick checks (2 minutes)

1\) Check the app config:

&nbsp;  - Open `.env`

&nbsp;  - Confirm:

&nbsp;    - `REDIRECT\_URI=http://localhost:3000/redirect`



2\) Check Entra App Registration:

&nbsp;  - Microsoft Entra ID → App registrations → \*\*IAM-OIDC-Onboarding-Demo-DEV\*\*

&nbsp;  - \*\*Authentication\*\* → Platform \*\*Web\*\*

&nbsp;  - Redirect URIs must include \*\*exactly\*\*:

&nbsp;    - `http://localhost:3000/redirect`



3\) Confirm in logs:

&nbsp;  - Entra ID → \*\*Sign-in logs\*\*

&nbsp;  - Filter: Application = IAM-OIDC-Onboarding-Demo-DEV

&nbsp;  - Open the failure event → verify AADSTS50011 or redirect mismatch details.



\## Fix (step-by-step)

1\) In Entra App Registration → Authentication:

&nbsp;  - Add or correct Redirect URI:

&nbsp;    - `http://localhost:3000/redirect`

&nbsp;  - Save.



2\) In `.env`:

&nbsp;  - Ensure `REDIRECT\_URI` matches exactly.

&nbsp;  - Save.



3\) Restart the app:

&nbsp;  - Stop node with `Ctrl + C`

&nbsp;  - Start: `node server.js`



4\) Retest:

&nbsp;  - Open `http://localhost:3000`

&nbsp;  - Click \*\*Sign in\*\*



\## Prevention

\- Keep redirect URIs minimal (only what you need).

\- Use environment-specific URIs (dev/test/prod).

\- Add a runbook note: “Always verify scheme/host/port/path match exactly.”

