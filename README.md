# TryHackMe | Verified Write-ups

Organized documentation for **TryHackMe** rooms that were solved and verified inside the authorized lab. Each write-up is a **single Markdown file per room**, designed to take the reader from scenario understanding to analysis, solution steps, final answers, and security lessons.

> **Scope:** Training inside authorized TryHackMe labs only.

## Quick overview

| Metric | Status |
|---|---|
| Documented rooms | **30 rooms** |
| Answer status | **Officially verified inside TryHackMe** |
| Room files | **One file per room** |
| Ratings | Not submitted as part of this workflow |
| Repository visibility | **Private** |

## Navigation

| Section | Description |
|---|---|
| [Completed rooms](#completed-rooms) | Full index ordered by completion sequence |
| [Rooms under verification](docs/unverified-rooms.md) | Rooms not listed as complete until verified |
| [Writing methodology](docs/workflow.md) | Rules for adding new rooms |

## Completed rooms

### 01–10 | SOC, defense, and monitoring

| # | Room | Focus | Write-up |
|---:|---|---|---|
| 01 | [Senior Security Analyst Intro](https://tryhackme.com/room/seniorsecanalystintro) | SOC analyst mindset, escalation, offensive thinking | [Open](rooms/01-senior-security-analyst-intro/README.md) |
| 02 | [SOC L2 Alert Triage](https://tryhackme.com/room/socl2alerttriage) | Alert triage, timeline building, containment | [Open](rooms/02-soc-l2-alert-triage/README.md) |
| 03 | [Report Writing for SOC L2](https://tryhackme.com/room/reportwritingsocl2) | Executive summaries and DFIR handoffs | [Open](rooms/03-report-writing-for-soc-l2/README.md) |
| 04 | [Defensive Security Trends](https://tryhackme.com/room/defensivesecuritytrends) | Defensive trends, supply chain, AI | [Open](rooms/04-defensive-security-trends/README.md) |
| 05 | [Splunk: Exploring SPL](https://tryhackme.com/room/splunkexploringspl) | Log search with SPL | [Open](rooms/05-splunk-exploring-spl/README.md) |
| 06 | [Monitoring Active Directory](https://tryhackme.com/room/monitoringactivedirectory) | Identity, authentication, and privilege change monitoring | [Open](rooms/06-monitoring-active-directory/README.md) |
| 07 | [M365 Monitoring Basics](https://tryhackme.com/room/m365monitoringbasics) | Microsoft 365 and identity log monitoring | [Open](rooms/07-m365-monitoring-basics/README.md) |
| 08 | [Entra ID Monitoring](https://tryhackme.com/room/entraidmonitoring) | Sign-in and Entra ID log monitoring | [Open](rooms/08-entra-id-monitoring/README.md) |
| 09 | [Cloud Security Pitfalls](https://tryhackme.com/room/cloudsecuritypitfalls) | Cloud protection and migration risks | [Open](rooms/09-cloud-security-pitfalls/README.md) |
| 10 | [Threat Hunting: Introduction](https://tryhackme.com/room/threathuntingintroduction) | Hypothesis-driven hunting and detection improvement | [Open](rooms/10-threat-hunting-introduction/README.md) |

### 11–30 | Threat intelligence, web, and incident response

| # | Room | Focus | Write-up |
|---:|---|---|---|
| 11 | [Volt Typhoon](https://tryhackme.com/room/volttyphoon) | Threat actor techniques against critical infrastructure | [Open](rooms/11-volt-typhoon/README.md) |
| 12 | [Fools Mate, Revenge](https://tryhackme.com/room/foolsm8v2) | Prototype pollution and chess app logic bypass | [Open](rooms/12-fools-mate-revenge/README.md) |
| 13 | [ContAInment](https://tryhackme.com/room/containment) | PCAP analysis and ransomware response | [Open](rooms/13-containment/README.md) |
| 14 | [Valenfind](https://tryhackme.com/room/lafb2026e10) | LFI, source disclosure, database extraction | [Open](rooms/14-valenfind/README.md) |
| 15 | [Fools Mate](https://tryhackme.com/room/foolsmate) | Client-side validation bypass and API manipulation | [Open](rooms/15-fools-mate/README.md) |
| 16 | [Corp Website](https://tryhackme.com/room/lafb2026e7) | React2Shell, RCE, then privilege escalation via sudo | [Open](rooms/16-corp-website/README.md) |
| 17 | [When Hearts Collide](https://tryhackme.com/room/lafb2026e1) | MD5 collision exploitation in a web app | [Open](rooms/17-when-hearts-collide/README.md) |
| 18 | [Signed Messages](https://tryhackme.com/room/lafb2026e8) | Predictable RSA key derivation and signature forgery | [Open](rooms/18-signed-messages/README.md) |
| 19 | [TryHack3M: Bricks Heist](https://tryhackme.com/room/tryhack3mbricksheist) | WordPress RCE, miner analysis, wallet linkage | [Open](rooms/19-bricks-heist/README.md) |
| 20 | [Extracted](https://tryhackme.com/room/extractedroom) | PCAP analysis, KeePass memory dump, stolen DB recovery | [Open](rooms/20-extracted/README.md) |
| 21 | [Cache Me Outside](https://tryhackme.com/room/cachemeoutside) | OSINT: identity, public data, geo clues | [Open](rooms/21-cache-me-outside/README.md) |
| 22 | [Digital Footprint](https://tryhackme.com/room/osintchallengeiv) | EXIF, WARC, reverse search, document metadata | [Open](rooms/22-digital-footprint/README.md) |
| 23 | [CupidBot](https://tryhackme.com/room/lafb2026e6) | Web, prompt injection, AI agent secret extraction | [Open](rooms/23-cupidbot/README.md) |
| 24 | [Water Bottle](https://tryhackme.com/room/waterbottle) | OSINT tracking of a historical water station | [Open](rooms/24-water-bottle/README.md) |
| 25 | [Missing Person](https://tryhackme.com/room/missingperson) | OSINT: image analysis, event, restaurant, DJ, cave | [Open](rooms/25-missing-person/README.md) |
| 26 | [Hidden Deep Into my Heart](https://tryhackme.com/room/lafb2026e9) | Web enumeration, robots.txt secrets, admin path | [Open](rooms/26-hidden-deep-into-my-heart/README.md) |
| 27 | [TryHeartMe](https://tryhackme.com/room/lafb2026e5) | JWT tampering, authorization bypass, hidden item purchase | [Open](rooms/27-tryheartme/README.md) |
| 28 | [Speed Chatting](https://tryhackme.com/room/lafb2026e4) | Unrestricted upload, Python reverse shell, RCE | [Open](rooms/28-speed-chatting/README.md) |
| 29 | [Cupid's Matchmaker](https://tryhackme.com/room/lafb2026e3) | Stored XSS, HeadlessChrome, reviewer cookie theft | [Open](rooms/29-cupids-matchmaker/README.md) |
| 30 | [Love Letter Locker](https://tryhackme.com/room/lafb2026e2) | IDOR, broken access control, reading other users' messages | [Open](rooms/30-love-letter-locker/README.md) |

## Room structure

```text
rooms/
└── NN-room-name/
    └── README.md
```

Each room file combines environment notes, objective, analysis, practical steps, answers, flags, official verification outcome, security takeaways, and references. There are no separate `solution.md` or `notes.md` files.

## Completion standard

A room is listed in the index only after answers are accepted inside TryHackMe and completion status (or equivalent proof) is confirmed. Room ratings are not submitted. Partial rooms are never presented as complete.

## Adding future rooms

Each new room gets a sequential number, its own folder, and a single `README.md`. Documentation starts with the objective, explains the observation that led to the next step, and ends with verified answers, security lessons, and appropriate references.

## Privacy

This repository is **Private**. Do not add account data, secrets, or personal information. Temporary lab IPs are mentioned only when they are part of the lab context. All work stays within authorized TryHackMe scope.
