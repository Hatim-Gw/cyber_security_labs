# DVWA — Session Security and Safe Evidence Handling

**Environment:** Damn Vulnerable Web Application (DVWA), virtual lab  
**Status:** In progress — documentation of discussed observations; testing evidence pending

## Objective

Understand how HTTP session cookies work, why an exposed authenticated session identifier can be sensitive, and how network configuration affects the risk of sharing lab evidence.

## Discussed observations

- DVWA was accessed in a virtual lab.
- The lab discussion referenced a private IPv4 address and port 8080.
- A PHP session cookie named `PHPSESSID` was visible in a screenshot.
- DVWA was configured with its intentionally vulnerable `low` security setting.
- Default DVWA demonstration credentials were discussed; real credential values are intentionally omitted here.

These are discussion-level observations, not independently reproduced tests. No successful session-hijacking attempt or network exposure test has been demonstrated in this record.

## Technical analysis

PHP commonly uses `PHPSESSID` to associate a browser request with server-side session state. If a valid authenticated session identifier is copied, an attacker who can reach the application may be able to reuse that session, depending on server-side controls and whether the session remains valid.

A private IPv4 address is not ordinarily routed over the public Internet, but it does **not** guarantee that a service is inaccessible from other devices. Virtual networking modes (NAT, bridged, host-only), port forwarding, and host firewall rules determine practical reachability.

## Evidence publishing checklist

- [ ] Remove or mask actual `PHPSESSID` values and other cookies
- [ ] Redact authorization headers, passwords, tokens, and secrets
- [ ] Review browser URLs and screenshots for identifying information
- [ ] Verify the VM network mode and any published/forwarded ports
- [ ] Invalidate or expire sessions before publishing evidence
- [ ] Upload only sanitized evidence

**Screenshots:** Not uploaded. Original images must be inspected and sanitized before publication.

## Next practical verification

1. Identify the DVWA VM/container networking mode.
2. Inspect local listening ports and port forwarding without changing configuration.
3. Determine whether DVWA is reachable only from the host or from other devices.
4. Document findings and add sanitized screenshots.

## Defensive takeaway

Treat authenticated session cookies as secrets, including in training environments. Prefer isolated networks, short session lifetimes, secure cookie attributes where applicable, and deliberate evidence sanitization.

> Educational use only: perform security testing exclusively on owned or explicitly authorized lab systems.
