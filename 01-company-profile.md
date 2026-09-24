# Northbridge Financial Partners: Company Profile

*Simulated organization for a cybersecurity home lab. Not a real company.*

## Overview

Northbridge Financial Partners is a wealth management and financial advisory firm headquartered in Dayton, Ohio. It serves about 3,000 individual and small-business clients with investment accounts, retirement planning, and insurance products.

## Workforce (50 employees)

- Executive Leadership: 4
- Human Resources: 6
- Finance & Operations: 10
- Sales & Advisory: 24
- IT: 6

About 40% of staff work remotely or hybrid, mostly advisors who meet clients off-site.

## Technology Environment

- Windows 11 laptops for all employees
- Active Directory domain: `corp.northbridge.lab`
- Microsoft 365 for email, Teams, and SharePoint, with MFA required
- Ubuntu Linux server `lnx01` for internal services
- Remote access over VPN

## Sensitive Data

- Client PII: names, SSNs, dates of birth, account numbers
- Client financial records: balances, transactions, investment holdings
- Employee HR records: payroll, benefits, performance reviews
- Internal financials and advisor compensation

## Regulatory Environment

- Gramm-Leach-Bliley Act (GLBA) Safeguards Rule, which requires a written information security program
- FINRA and SEC recordkeeping and cybersecurity expectations
- State data breach notification laws

## Known Security Gaps (starting point)

- IT staff share one administrator account
- No centralized logging or alerting
- Remote workers connect from unmanaged home networks
- No formal data classification policy
- No security awareness training program
