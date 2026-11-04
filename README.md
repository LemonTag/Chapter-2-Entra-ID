# [Title, outcome-flavored: "Investigating an Identity Attack in Entra ID"]

## Scenario
2 to 3 sentences. What was the situation and what question did the investigation answer? Frame it like a work ticket, not homework.
An employee at Madhat Labs was incorrectly granted owner-level permissions within the tenant. The employee was later targeted by a phishing attack, allowing the attacker to steal their session token and bypass MFA to gain unauthorized access. The investigation focused on determining how the attacker gained access, what permissions were compromised, and the potential impact on the tenant.

## Environment
One list: platform, services, tools, access level. Honest framing: "live multi-user Azure training tenant, Reader access."
Live multi-user Azure training tenant
Platform: Microsoft Azure
Environment: Live multi-user Azure training tenant
Service: Azure Portal
Tools: Azure Portal, Azure Active Directory (Microsoft Entra ID)
Access Level: Reader access

## Investigation
The core. Numbered steps IN YOUR OWN WORDS: what you looked at, what you found, what you concluded at each step. 6 to 12 screenshots of meaningful moments (portal views, query results, before/after).
Investigation
1. Reviewed App Registrations
- I opened App registrations in the Azure Portal and reviewed the registered applications. I located an application named Mad Hat Legacy Sync Service, which became the focus of my investigation.
<img width="939" height="354" alt="Screenshot 2026-11-04 150054" src="https://github.com/user-attachments/assets/853ae1c3-d88e-4f81-a587-98ff1bdf217d" />
<img width="362" height="348" alt="Screenshot 2026-11-04 150314" src="https://github.com/user-attachments/assets/395d65fa-41a9-44f1-94ea-1fe9bd741ebc" />

2. Inspected Certificates & Secrets
- I opened the Certificates & Secrets section of the Mad Hat Legacy Sync Service application. I found evidence left behind by the attacker in the form of a flag, suggesting that the application had been modified or used for unauthorized access.
<img width="490" height="278" alt="Screenshot 2026-11-04 151749" src="https://github.com/user-attachments/assets/6c245c3e-297b-4512-a918-626582c78643" />

3. Reviewed Application Owners and Permissions
- I returned to the Mad Hat Legacy Sync Service and investigated its owners and the permissions granted through Microsoft Graph admin consent. This helped me examine who had control over the application and what level of access had been approved.
<img width="573" height="301" alt="Screenshot 2026-11-04 153759" src="https://github.com/user-attachments/assets/ac0bb6a9-72a4-4e89-b9d6-74810f73f63b" />

4. Identified the Rogue Application
- After identifying the name of the rogue application created by the attacker, I opened its registration and examined its details. I found an internal note that provided additional evidence related to the attack.
<img width="600" height="324" alt="image" src="https://github.com/user-attachments/assets/dd2f0899-ce31-4171-a2bb-30cfdab5b152" />

5. Examined Exposed APIs
- I returned to the Mad Hat Legacy Sync Service and reviewed its Expose an API section. I discovered a custom scope that the attacker had injected, which appeared to be part of their persistence strategy and potential backup access method.
<img width="622" height="308" alt="Screenshot 2026-11-04 160954" src="https://github.com/user-attachments/assets/88b4cb22-dc8b-41e0-bcc8-85cf7c212097" />

6. Reviewed Authentication Settings
- Finally, I returned to the rogue application and opened its Authentication section. I examined the URL, decoded its contents, and used the decoded information to identify and submit the final flag.
<img width="820" height="300" alt="Screenshot 2026-11-04 162245" src="https://github.com/user-attachments/assets/b62cf147-d16d-4414-ab76-d7a4b5d518e2" />


## What broke / what surprised me
The most credible section in the document. Dead ends, wrong guesses, the thing that took an hour. Employers know real work is messy. This section separates you from certificate collectors.

## Findings and recommendations
What you determined, plus 2 or 3 recommendations as if you were reporting to the resource owner.

## What I learned
3 to 5 bullets. At least one technical, one "what I'd do differently."
