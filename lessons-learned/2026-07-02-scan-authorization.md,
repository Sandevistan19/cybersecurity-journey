# Lesson Learned: Always Verify Scan Target Authorization

**Date:** 2026-07-02
**Category:** Ethics & Methodology
**Tools:** Nmap

## What happened

While practicing Nmap flags, I copied an example command straight from a cheat sheet and ran it — including the IP range used in the example. The scan targeted 64 public-internet hosts. Partway through, I realized I had no idea whose network those IPs belonged to, or whether I had any right to be scanning them.

## Why it happened

The cheat sheet used real public IP addresses as example syntax rather than a placeholder private range (e.g. `192.168.1.0/24`) or a known-safe test target. I copied the command without stopping to check what the target actually was.

## What I did about it

- Killed the scan immediately (`Ctrl+C`) once I realized I couldn't confirm authorization.
- Did **not** re-run it or attempt to identify the range further via active means.
- Reviewed why this matters legally: in the UK, unauthorized scanning of systems you don't own or have written permission to test can fall under the **Computer Misuse Act 1990** — intent doesn't change that a port scan without authorization is the line, not just exploitation.

## The actual lesson

Before running *any* scan, the question isn't "what flags do I need" — it's **"how do I know I'm authorized to scan this target?"** A cheat sheet, tutorial, or blog post is never itself authorization. If I can't answer that question with certainty, I don't run the command, full stop.

## Going forward

Safe targets I'll use for practice instead of arbitrary example IPs:
- `scanme.nmap.org` — Nmap project's own sanctioned test target
- My own home network (`192.168.x.x`)
- TryHackMe deployed machines (`10.10.x.x`, over their OpenVPN)
- Local vulnerable VMs (e.g. Metasploitable2) run in isolation in VirtualBox

## WHOIS follow-up

Ran `whois` on both IPs afterward to confirm the risk was real, not theoretical:

- `178.27.10.13` → registered to **Vodafone Kabel Deutschland**, a residential broadband customer allocation block in Germany
- `136.244.41.196` → registered to **Tachus Infrastructure LLC**, a residential fiber ISP allocation block in Texas, US

Both were large ISP customer blocks — meaning the original command would have scanned random members of the public in two different countries, not a legitimate test target. This confirmed the decision to stop was correct, not overcautious.

## Verified-safe scan example (for comparison)

```bash
nmap -sV scanme.nmap.org
```

Run cleanly against an explicitly authorized target, with no rate-limiting pushback — a useful contrast to what a scan against an unknown/hostile-configured target looks like.

---
*This entry exists because catching and correcting this before acting on it matters more than pretending it didn't happen. Judgment like this is part of the job.*
