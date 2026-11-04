#  Module 2: Investigating an Identity Attack in Entra ID

## Scenario
An employee at Madhat Labs was incorrectly granted owner-level permissions within the tenant. The employee was later targeted by a phishing attack, allowing the attacker to steal their session token and bypass MFA to gain unauthorized access. The investigation focused on determining how the attacker gained access, what permissions were compromised, and the potential impact on the tenant.

## Environment
Live multi-user Azure training tenant
Platform: Microsoft Azure
Environment: Live multi-user Azure training tenant
Service: Azure Portal
Tools: Azure Portal, Azure Active Directory (Microsoft Entra ID)
Access Level: Reader access

## Investigation
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
Challenges and Dead Ends
The biggest challenge during this investigation was identifying the rogue application and understanding what Objectives 3, 4, and 5 were asking me to find. I spent a lot of time checking other registered applications because I initially thought one of them was the rogue app. I was searching for the internal notes and flags but wasn't sure which application I needed to investigate.

Objective 4: Persistence with Exposed API was particularly difficult. I had a hard time understanding what I was looking at in the Azure Portal and what the flag was hinting at regarding how the attacker could maintain access to the tenant.

Objective 5 was another challenge because I didn't fully understand the instructions for decoding the URL or where to find it within the rogue application's settings. I had to go back and reread the instructions to understand what information I needed and where to look.

What I Learned:

I need to slow down, read the objectives carefully, and understand what each step is asking before jumping into the Azure Portal. I also learned that investigations aren't always straightforward. Sometimes finding the right evidence means going back, reviewing what I've already looked at, and approaching the problem from a different perspective.

## Findings and recommendations
1.Review Application Ownership: Make sure you know who has ownership of each application and verify that everyone has a legitimate reason for having those permissions.
2.Follow Least Privilege: Avoid giving users unnecessary Owner or administrative permissions. Only grant the access they need to perform their jobs.

## What I learned
What I Learned
- I learned how rogue applications work and how attackers can make them blend in with legitimate applications to avoid detection.
- I learned how to use CyberChef to decode URLs and uncover information that might otherwise be difficult to understand.
- I learned how reviewing Expose an API and application owners can help identify suspicious changes and track down a rogue application.
- I learned the importance of reviewing ownership permissions before granting someone owner access. I wouldn't make Carl an owner without verifying that he needed those permissions, and I would make sure to review all application ownerships before calling it a day.

