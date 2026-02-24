# Microsoft Entra ID OIDC Onboarding Demo
Built to demonstrate end-to-end IAM onboarding using modern identity protocols and to practice real-world enterprise troubleshooting scenarios.
## What This Does
A Node/Express application using MSAL that implements OIDC authentication via Microsoft Entra ID, including sign-in flow, audit log capture, and operational runbooks for common break/fix incidents.
## Authentication Flow
User → Express App → Microsoft Entra ID (OIDC) → ID Token validation → Authenticated session
## Key Features

OIDC sign-in flow using MSAL and Microsoft Entra ID
Sign-in and audit log evidence captured and documented
Operational runbooks for common enterprise IAM incidents
Security best practice — secrets stored in .env and excluded via .gitignore

## Runbooks Included

Redirect URI mismatch
Invalid client secret
Token expiry handling
Conditional Access policy failure

## Technology Stack

Node.js / Express
MSAL (Microsoft Authentication Library)
Microsoft Entra ID (Azure AD)
OIDC protocol

## Security Notice
Secrets are stored locally in .env and excluded via .gitignore. Never commit tokens or credentials. Rotate secrets regularly."
