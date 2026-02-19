\# Compliance \& Audit Readiness Mapping (Demo)



\## Important note (scope)

ISO 27001 compliance is organisational, not something a single repo can claim.  

What this demo provides is \*\*control implementation + evidence\*\* that supports an ISO-style audit: secure configuration, secret hygiene, traceable changes via audit logs, and repeatable runbooks.



\## Audit readiness (what I do consistently)

My focus is audit readiness: every onboarding has a repeatable checklist, logs-based verification, and documented break/fix paths—so we can prove control and reduce repeat incidents.



\### Evidence produced by this demo

\- \*\*Microsoft Entra Sign-in logs\*\*: success/failure, error codes (AADSTS\*), Conditional Access/MFA status (if enabled)

\- \*\*Microsoft Entra Audit logs\*\*: consent events, redirect URI updates, secrets/certificates management (“who changed what, when”)

\- \*\*Runbooks\*\*: RB-001 (Redirect URI mismatch), RB-002 (Invalid/expired client secret)

\- \*\*Security hygiene\*\*: no secrets/tokens committed (local `.env` + `.gitignore`), secret rotation guidance



\## Framework alignment (practical mapping)



\### NIST CSF (high level)

\- \*\*Identify\*\*: document app registration settings (authority, redirect URI, scopes)

\- \*\*Protect\*\*: secret hygiene, least privilege scopes, secure configuration standards

\- \*\*Detect\*\*: monitor sign-in logs + failure codes and trends

\- \*\*Respond\*\*: runbooks for common onboarding failures

\- \*\*Recover\*\*: restore service (fix config/rotate secret), validate success in logs, record lessons learned



\### ITIL (operational alignment)

\- \*\*Incident Management\*\*: handle auth failures using runbooks + log-led triage

\- \*\*Problem Management\*\*: remove repeat causes (standard configs, checks, rotation process)

\- \*\*Change Management\*\*: controlled updates (redirect URI, secrets) with audit trail + validation



\## What is out of scope for this demo

\- Full identity lifecycle (Joiner/Mover/Leaver), SCIM provisioning, access reviews, privileged access governance

\- Organisation-level ISO 27001 certification / ISMS processes

