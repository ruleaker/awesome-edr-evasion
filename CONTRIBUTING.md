# Contributing

Thanks for considering a contribution. This list aims for **signal, not coverage** — every entry should earn its place.

## Suggesting a resource

Open a Pull Request that adds the resource to the appropriate section. Each entry must follow the format:

```markdown
- [Name](URL) — One-line description explaining *why it matters* for EDR/AV evasion or defender-side telemetry research.
```

## Quality bar

Resources should meet **all** of the following:

- **Actively maintained or historically foundational.** Tools updated in the last 18 months, or papers/PoCs that remain referenced as primary sources.
- **Substantively about EDR/AV evasion** or directly-supporting tradecraft (syscalls, loaders, telemetry tampering, kernel callbacks, BYOVD). Generic offensive security content is out of scope — that's what [awesome-pentest](https://github.com/enaqx/awesome-pentest) is for.
- **Primary source.** Link to the repo / paper / vendor doc, not to a blog post that summarizes it. The one exception is technique walkthroughs that *are* the primary explainer (e.g. Outflank, MDSec, modexp posts).
- **Stable home.** Personal blogs, GitHub repos, vendor labs — yes. Threads on Twitter/X or Discord-only resources — no.
- **Original.** Not a re-aggregation of resources already on this list.

## What gets rejected

- Generic pentest / red team content with no evasion angle
- Twitter-only / Discord-only resources
- Repos with no README, no commits in 3+ years, and no historical citation value
- Affiliate-linked product pages or course mills
- Duplicates of existing entries with weaker framing

## Scope

In scope:
- Process and memory tradecraft (injection, hollowing, doppelgänging)
- Syscall manipulation (direct, indirect, gate techniques)
- Sleep obfuscation, ROP-based encryption
- Loader development and PIC shellcode
- AMSI / ETW / WLDP / CLM bypass
- Kernel-level evasion (BYOVD, callback removal, DSE bypass)
- C2 frameworks with non-trivial evasion features
- Detection tooling (read as: "know thy enemy")
- Training programs with substantive evasion content

Out of scope:
- Initial-access social engineering (phishing kits, lures, payload delivery via mail)
- Web exploitation
- Network-level red team (lateral movement, AD enumeration — except where evasion-relevant)
- Defensive blue team content unless it informs evasion design

## Format

- Keep description **under 30 words**.
- Use `*(paid)*` suffix for paywalled resources.
- Sort entries within a section by relevance, not alphabetically.
- Use the author's preferred capitalization for tool names (`SysWhispers3`, not `syswhispers3`).

## PR title

Use the format: `add: <Resource Name>` or `update: <Resource Name>` or `remove: <Resource Name> — <reason>`.

## Ethics

This list is for authorized red team work, malware research, and defensive evaluation. Don't submit resources whose primary documented use is criminal operations against targets without authorization.
