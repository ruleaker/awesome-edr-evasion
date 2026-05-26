# Awesome EDR Evasion [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of resources for EDR/AV evasion research and red team tradecraft.

Modern endpoint defenses move fast — kernel callbacks, ETW providers, ML telemetry, cloud-side correlation. The offensive side keeps pace through process tradecraft, syscall manipulation, sleep obfuscation, and userland API patching. This list collects the papers, PoCs, loaders, and operators worth following.

Intended for authorized red team work, malware research, and defensive evaluation. Treat every link as a primary source — read the code, not just the headline.

## Contents

- [Foundations & EDR Architecture](#foundations--edr-architecture)
- [Process & Memory Tradecraft](#process--memory-tradecraft)
- [Sleep Obfuscation & Syscalls](#sleep-obfuscation--syscalls)
- [Loader Development](#loader-development)
- [AMSI / ETW / WLDP Bypass](#amsi--etw--wldp-bypass)
- [Kernel-Level Evasion](#kernel-level-evasion)
- [Tooling & Frameworks](#tooling--frameworks)
- [Detection & Telemetry](#detection--telemetry)
- [Research Papers](#research-papers)
- [Blogs & Researchers](#blogs--researchers)
- [Training & Labs](#training--labs)
- [Related Awesome Lists](#related-awesome-lists)

## Foundations & EDR Architecture

- [ired.team](https://www.ired.team/) - Spotless Security's offensive notebook. Process injection, persistence, internals — the most-referenced free corpus.
- [Elastic Security Labs](https://www.elastic.co/security-labs) - In-depth posts on EDR internals, telemetry gaps, and emerging threat tradecraft.
- [modexp](https://modexp.wordpress.com/) - Odzhan's low-level Windows internals blog. Position-independent shellcode, indirect calls, API hashing.
- [0xPat — Malware Development series](https://0xpat.github.io/) - Multi-part walkthrough from string obfuscation to process hollowing.
- [Pavel Yosifovich — *Windows Kernel Programming, 2nd ed.*](https://leanpub.com/windowskernelprogrammingsecondedition) - The reference for understanding the surfaces EDRs hook.
- [Windows Internals, 7th ed. (Part 1 & 2)](https://learn.microsoft.com/en-us/sysinternals/resources/windows-internals) - Russinovich et al. Required reading for serious evasion work.
- [Microsoft Defender for Endpoint — Telemetry API](https://learn.microsoft.com/en-us/defender-endpoint/) - Vendor documentation worth reading to understand the blue side.
- [vxunderground](https://vx-underground.org/) - Malware archive and research library; samples, papers, source code.

## Process & Memory Tradecraft

- [Process Hollowing — original technique](https://attack.mitre.org/techniques/T1055/012/) - MITRE writeup with primary references.
- [Process Doppelgänging (MITRE T1055.013)](https://attack.mitre.org/techniques/T1055/013/) - NTFS transactions abused for image swap. Source paper linked in Research Papers section.
- [Process Herpaderping](https://github.com/jxy-s/herpaderping) - Johnny Shaw. Modify image on disk after section creation.
- [Process Ghosting](https://www.elastic.co/blog/process-ghosting-a-new-executable-image-tampering-attack) - Gabriel Landau. Delete-pending file mapped before deletion completes.
- [Module Stomping](https://0xpat.github.io/Malware_development_part_5/) - 0xPat. Hijack a legitimately loaded DLL's memory.
- [Phantom DLL Hollowing](https://github.com/forrest-orr/phantom-dll-hollower-poc) - Forrest Orr. Image-backed shellcode hosting without disk artifacts.
- [Transacted Hollowing](https://github.com/hasherezade/transacted_hollowing) - Combines Doppelgänging and Hollowing.
- [ThreadlessInject](https://github.com/CCob/ThreadlessInject) - CCob. Injection without `CreateRemoteThread`/`Queue*APC` — overwrites EAT pointers.
- [DarkLoadLibrary](https://github.com/bats3c/DarkLoadLibrary) - LoadLibrary replacement that loads from memory.
- [ProcessReflection (`PROCESS_VM_*`)](https://googleprojectzero.blogspot.com/2021/01/in-wild-series-windows-exploits.html) - James Forshaw / Project Zero references on lesser-known process primitives.
- [Reflective DLL Injection](https://github.com/stephenfewer/ReflectiveDLLInjection) - Stephen Fewer. The original technique; still foundational.
- [Hells Hall / Indirect Inject Patterns](https://github.com/Maldev-Academy/HellHall) - MalDev Academy. Modern injection-by-indirect-syscall walkthrough.

## Sleep Obfuscation & Syscalls

- [Ekko](https://github.com/Cracked5pider/Ekko) - C5pider. Sleep obfuscation via timer queue + RW/RX flip — the modern reference impl.
- [Foliage](https://github.com/SecIdiot/FOLIAGE) - Sec Idiot. Alternative sleep-mask using NtContinue.
- [DeepSleep](https://github.com/janoglezcampos/DeepSleep) - Encrypted sleep with CFG/ROP gadgets.
- [Cronos](https://github.com/Idov31/Cronos) - Idov31. Compact ROP-driven sleep encryption.
- [Hell's Gate](https://github.com/am0nsec/HellsGate) - am0nsec & smelly__vx. Original dynamic SSN resolution PoC.
- [Halo's Gate](https://blog.sektor7.net/#!res/2021/halosgate.md) - SEKTOR7 / Reenz0h. Hell's Gate fallback when ntdll is hooked.
- [Tartarus Gate](https://github.com/trickster0/TartarusGate) - Hell's Gate variant resilient to inline hooks.
- [SysWhispers](https://github.com/jthuraisamy/SysWhispers) - First-gen direct syscall stub generator.
- [SysWhispers2](https://github.com/jthuraisamy/SysWhispers2) - EDR-aware version; removes hard-coded SSNs.
- [SysWhispers3](https://github.com/klezVirus/SysWhispers3) - Adds indirect syscall + jumper randomization.
- [FreshyCalls](https://github.com/crummie5/FreshyCalls) - C++ direct syscall library with sorted-export SSN discovery.
- [RecycledGate](https://github.com/thefLink/RecycledGate) - Reuses syscall instructions inside ntdll.
- [Tampering with Direct System Calls — MDSec](https://www.mdsec.co.uk/2020/12/bypassing-user-mode-hooks-and-direct-invocation-of-system-calls-for-red-teams/) - Foundational walkthrough.
- [The Definitive Guide to Process Injection — Elastic](https://www.elastic.co/blog/ten-process-injection-techniques-technical-survey-common-and-trending-process) - Cross-technique survey from the defender's perspective.

## Loader Development

- [Stardust](https://github.com/Cracked5pider/Stardust) - C5pider. Modern PIC shellcode framework with build system.
- [Donut](https://github.com/TheWover/donut) - TheWover. Generates position-independent shellcode from PE/DLL/.NET/VBS/JS.
- [sRDI](https://github.com/monoxgas/sRDI) - Shellcode-form reflective DLL loader.
- [PEzor](https://github.com/phra/PEzor) - PE → shellcode packer with sandbox checks and AV evasion options.
- [ScareCrow](https://github.com/optiv/ScareCrow) - Loader generator with EDR userland-hook unhooking.
- [Nimcrypt2](https://github.com/icyguider/Nimcrypt2) - Nim-based PE/shellcode/raw payload crypter.
- [Inceptor](https://github.com/klezVirus/inceptor) - Templating engine for AV/EDR-evasive loaders.
- [DInvoke](https://github.com/TheWover/DInvoke) - TheWover & Flangvik. Dynamic invocation without PInvoke signatures.
- [BokuLoader](https://github.com/boku7/BokuLoader) - Cobalt Strike UDRL with manual mapping + sleep obfuscation.
- [CobaltStrike — UDRL Sample](https://github.com/Cobalt-Strike/UDRL-VS) - Official UDRL Visual Studio template.
- [pe2shc / sRDI / RDLL](https://github.com/hasherezade/pe_to_shellcode) - PE → shellcode converter.

## AMSI / ETW / WLDP Bypass

- [AMSI Bypass — Matt Graeber's original tweet](https://gist.github.com/mattifestation/9b3dde20a7da1b65adea1c5d3a64e0a8) - The historical reference; patched many times since but still cited.
- [Bypassing AMSI via COM Server Hijacking — modexp](https://modexp.wordpress.com/2019/06/03/disable-amsi-wldp-dotnet/) - AMSI + WLDP + .NET CLR bypass.
- [Hardware Breakpoints for AMSI Bypass — rad9800](https://github.com/rad9800/hwbp4mw) - Userland hardware breakpoint primitive for hookless patching.
- [AmsiScanBufferBypass](https://github.com/rasta-mouse/AmsiScanBufferBypass) - rasta-mouse. Classic patch-`AmsiScanBuffer` PoCs (C, C#, PowerShell).
- [AMSI.fail](https://amsi.fail/) - Flangvik. Rotating AMSI bypass one-liner generator.
- [Tampering with Windows Event Tracing — Palantir](https://blog.palantir.com/tampering-with-windows-event-tracing-background-offense-and-defense-4be7ac62ac63) - Survey of ETW disablement primitives.
- [ETW: Event Tracing for Killing — Outflank](https://outflank.nl/blog/2023/05/30/cobalt-strike-and-outflank-security-tooling-better-together/) - Patch ETW from CS.
- [Bypassing WLDP](https://googleprojectzero.blogspot.com/2018/04/windows-exploitation-tricks-exploiting.html) - James Forshaw / Project Zero. CLM and WLDP internals.
- [InvisiShell](https://github.com/OmerYa/Invisi-Shell) - OmerYa. PowerShell without ScriptBlock logging/AMSI.
- [Bypass-AMSI Cheat Sheet — S3cur3Th1sSh1t](https://s3cur3th1ssh1t.github.io/Bypass_AMSI_by_manual_modification/) - Manual ScanBuffer modification techniques.

## Kernel-Level Evasion

- [LOLDrivers](https://www.loldrivers.io/) - Reference catalog of vulnerable signed drivers (BYOVD candidates), maintained by magicsword-io.
- [EDRSandblast](https://github.com/wavestone-cdt/EDRSandblast) - Removes kernel notify callbacks via vulnerable driver; by wavestone-cdt.
- [Backstab](https://github.com/Yaxser/Backstab) - Yaxser. Kills PPL-protected EDR processes via signed driver.
- [KDU](https://github.com/hfiref0x/KDU) - Kernel Driver Utility — load unsigned drivers via vulnerable ones.
- [TDL — Turla Driver Loader](https://github.com/hfiref0x/TDL) - Loads unsigned drivers using Turla's technique.
- [DSEFix](https://github.com/hfiref0x/DSEFix) - Disables Driver Signature Enforcement at runtime.
- [PPLFault](https://github.com/gabriellandau/PPLFault) - Gabriel Landau. Exploits page-fault races to dump PPL processes.
- [PPLDump](https://github.com/itm4n/PPLdump) - Dumps LSASS (PPL) without a driver via known parser bugs.

## Tooling & Frameworks

- [Havoc](https://github.com/HavocFramework/Havoc) - C5pider. Modern Qt-based C2 with sleep obfuscation and indirect syscalls.
- [Sliver](https://github.com/BishopFox/sliver) - BishopFox. Go-based, cross-platform C2; widely adopted alternative to Cobalt Strike.
- [Mythic](https://github.com/its-a-feature/Mythic) - Pluggable C2 with rich agent ecosystem (Apollo, Athena, Poseidon).
- [PoshC2](https://github.com/nettitude/PoshC2) - PowerShell/.NET-focused C2 by Nettitude.
- [Empire (BC-Security fork)](https://github.com/BC-SECURITY/Empire) - Maintained successor to the original PowerShell Empire.
- [Merlin](https://github.com/Ne0nd0g/merlin) - HTTP/2-based cross-platform C2 in Go.
- [Covenant](https://github.com/cobbr/Covenant) - .NET-centric C2 framework.
- [Cobalt Strike](https://www.cobaltstrike.com/) - Industry-standard commercial C2 platform. *(paid)*
- [Brute Ratel](https://bruteratel.com/) - Commercial C2 framework focused on EDR evasion. *(paid)*

## Detection & Telemetry

- [Elastic Detection Rules](https://github.com/elastic/detection-rules) - Production rule corpus; useful for understanding what's actually being hunted.
- [SigmaHQ](https://github.com/SigmaHQ/sigma) - Vendor-neutral detection rule format and ruleset.
- [Sysmon-Modular](https://github.com/olafhartong/sysmon-modular) - Olaf Hartong. Modular Sysmon config — read it to know what gets logged.
- [SwiftOnSecurity Sysmon Config](https://github.com/SwiftOnSecurity/sysmon-config) - The widely-deployed starting-point config.
- [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team) - Red Canary. Atomic tests mapped to MITRE ATT&CK.
- [pe-sieve](https://github.com/hasherezade/pe-sieve) - Scans live processes for hollowing, injection, hooks.
- [Moneta](https://github.com/forrest-orr/moneta) - Forrest Orr. Memory IoC scanner for live processes.
- [Patriot](https://github.com/joe-desimone/patriot) - Joe Desimone. Detects unbacked execution, RWX, and module overlap.
- [Hollows Hunter](https://github.com/hasherezade/hollows_hunter) - Process scanner built on pe-sieve.
- [MITRE ATT&CK — Defense Evasion (TA0005)](https://attack.mitre.org/tactics/TA0005/) - Tactic page; pivot point into specific technique writeups.

## Research Papers

- [Tal Liberman & Eugene Kogan — *Lost in Transaction: Process Doppelgänging* (BH EU 2017)](https://www.blackhat.com/docs/eu-17/materials/eu-17-Liberman-Lost-In-Transaction-Process-Doppelganging.pdf) - The foundational paper on NTFS-transaction image swap.
- [Itzik Kotler & Amit Klein — *Process Reimaging* (BH USA 2019)](https://i.blackhat.com/USA-19/Thursday/us-19-Kotler-Process-Reimaging-A-Cybercrime-Defense-Technique.pdf)
- [Adam Chester — *Hijacking DLLs in Windows*](https://www.mdsec.co.uk/2020/10/exploring-token-privileges/) - MDSec primer; companion reading.
- [Yarden Shafir & Alex Ionescu — *Windows 10 and the WNF Subsystem*](https://blog.quarkslab.com/) - Background on WNF abuse for stealth IPC.
- [Microsoft — *Defender for Endpoint Architecture*](https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-endpoint) - Vendor-side primary source.
- [SANS — *EDR Bypass Techniques: A Survey*](https://www.sans.org/reading-room/) - Reading-room aggregator; search "EDR".
- [Black Hat / DEF CON Archives](https://www.blackhat.com/html/archives.html) - Search "EDR", "syscall", "process injection".

## Blogs & Researchers

- [MDSec](https://www.mdsec.co.uk/blog/) - Operator-grade red team research; the canonical industry blog.
- [SpecterOps Posts](https://posts.specterops.io/) - AD, EDR-aware tooling, BloodHound research.
- [Outflank Blog](https://outflank.nl/blog/) - Loaders, OST, and tradecraft notes.
- [F-Secure / WithSecure Labs](https://labs.withsecure.com/) - Strong on offensive engineering and red team posts.
- [s3cur3th1ssh1t](https://s3cur3th1ssh1t.github.io/) - AMSI/ETW bypass writeups, hands-on PoCs.
- [SEKTOR7 Blog](https://blog.sektor7.net/) - Compact, technique-focused entries by Reenz0h.
- [Connor McGarr's Blog](https://connormcgarr.github.io/) - Kernel exploitation, EDR internals.
- [hasherezade](https://hshrzd.wordpress.com/) - Malware analysis and tooling; author of pe-sieve and libpeconv.
- [XPN Security](https://blog.xpnsec.com/) - Adam Chester on C2, telemetry tampering, and AD.
- [Phantom Security Group](https://phantomsec.tools/blog) - Underrated; deep technique writeups.
- [winternl](https://winternl.com/) - Windows internals notes.
- [Trickster0 — RT Notes](https://trickster0.github.io/) - Concise PoCs and explainers.

## Training & Labs

- [SEKTOR7 — Malware Development Essentials / Intermediate / Advanced](https://institute.sektor7.net/) - Reenz0h. The respected progressive curriculum for offensive Windows tradecraft.
- [MalDev Academy](https://maldevacademy.com/) - Modern, well-paced; covers syscalls, injection, evasion end-to-end. *(paid)*
- [Zero-Point Security — Red Team Ops I & II](https://training.zeropointsecurity.co.uk/) - Daniel Duggan. Practical CRTO/CRTL certs. *(paid)*
- [Offensive Security — EXP-301 (OSED)](https://www.offsec.com/courses/exp-301/) - Windows exploit dev; covers shellcoding fundamentals. *(paid)*
- [AlteredSecurity — Red Team Operator paths](https://www.alteredsecurity.com/) - AD-focused, evasion-aware. *(paid)*
- [HackTricks](https://book.hacktricks.xyz/) - Free reference wiki; quick-recall for techniques and one-liners.
- [TryHackMe — Red Teaming Path](https://tryhackme.com/path/outline/redteamer) - Entry-level structured path.
- [Hack The Box — Pro Labs (Dante, Offshore, Cybernetics)](https://www.hackthebox.com/hacker/pro-labs) - Live multi-host environments. *(paid)*

## Related Awesome Lists

- [awesome-pentest](https://github.com/enaqx/awesome-pentest) - Penetration testing ecosystem.
- [awesome-malware-analysis](https://github.com/rshipp/awesome-malware-analysis) - Defender-side mirror; useful for understanding detection logic.
- [awesome-windows-kernel-exploitation](https://github.com/k0keoyo/Awesome-Windows-Kernel-Exploitation) - Kernel exploit dev resources.
- [awesome-red-teaming](https://github.com/yeyintminthuhtut/Awesome-Red-Teaming) - Broader red team operations.
- [awesome-active-directory-attack](https://github.com/Orange-Cyberdefense/awesome-active-directory) - AD attack surface and tooling.

## Contributing

Contributions welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for the quality bar — actively maintained, primary source preferred, substantively about EDR/AV evasion, with a one-line description that tells the reader *why it matters*.
