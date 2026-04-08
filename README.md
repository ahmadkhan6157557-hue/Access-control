# Access-control
vertical privilage escalation / horizontal privilage escalation / RBAC
# access-control

A hands-on research repository covering broken access control vulnerabilities — how they work,
\how they're found, and how they're exploited. Built from real-world testing experience and lab work.

---

## What's Inside

```
access-control/
├── idor/               # Insecure Direct Object Reference
├── privilege-escalation/   # Horizontal & vertical privesc
├── forced-browsing/    # Unprotected endpoints & hidden paths
├── jwt-misconfig/      # Token-based access control flaws
├── mass-assignment/    # Parameter binding vulnerabilities
└── notes/             # Research notes and methodology
```

---

## Why This Exists

Access control bugs are consistently ranked among the most critical web vulnerabilities — and also the most misunderstood. A lot of writeups out there skim the surface. This repo is built to go deeper: actual payloads, real testing methodology, and notes from hands-on work.

No fluff. No AI-generated explanations. Just raw findings.

---

## Topics Covered

**IDOR (Insecure Direct Object Reference)**
Manipulating references to access objects belonging to other users. See [`idor/`](./idor/) for a full breakdown.

**Privilege Escalation**
Both horizontal (accessing another user's data) and vertical (gaining higher-privilege actions). Covers role-based access control (RBAC) flaws and missing authorization checks.

**Forced Browsing**
Hitting endpoints that aren't linked in the UI but are still reachable. Admin panels, debug routes, backup files — things that shouldn't be exposed but are.

**JWT Misconfiguration**
Weak signing, `alg: none` bypass, key confusion attacks, and missing claims validation — all leading to broken access control at the token level.

**Mass Assignment**
Sending extra parameters in requests that the server accepts and applies without authorization checks. Common in REST APIs built with frameworks that auto-bind request bodies to models.

---

## Setup

Clone the repo and you're good. Most labs run locally with Docker or a simple Python server.

```bash
git clone https://github.com/yourhandle/access-control.git
cd access-control
```

Specific setup instructions live inside each folder's own `README.md`.

---

## Methodology

This is roughly the flow used when testing access control on any target:

1. Map out all user roles in the application
2. Capture requests for each role using a proxy (Burp, ZAP)
3. Replay requests across roles — look for missing enforcement
4. Fuzz object references (IDs, GUIDs, filenames) with other accounts' values
5. Test direct URL access to privileged paths without going through the normal flow
6. Check JWT claims, API keys, and session tokens for trust assumptions

---

## Tools Used

- [Burp Suite](https://portswigger.net/burp) — Proxy, repeater, intruder
- [ffuf](https://github.com/ffuf/ffuf) — Forced browsing / endpoint fuzzing
- [jwt_tool](https://github.com/ticarpi/jwt_tool) — JWT testing
- [Autorize](https://github.com/Quitten/Autorize) — Burp extension for automated access control testing
- [ParamMiner](https://github.com/PortSwigger/param-miner) — Undocumented parameter discovery

---

## Resources

- [OWASP Broken Access Control](https://owasp.org/Top10/A01_2021-Broken_Access_Control/)
- [PortSwigger Web Security Academy – Access Control](https://portswigger.net/web-security/access-control)
- [HackTricks – IDOR](https://book.hacktricks.xyz/pentesting-web/idor)

---

## Legal

This repo is for educational and authorized testing purposes only. Do not use any of this material against systems you don't own or have explicit permission to test. Always operate within scope.

---

## License

MIT
