# Awesome Red Team Operations

### PenTest and Red Team Tools by Joas A Santos and S3cur3Th1sSh1t

A curated, battle-tested collection of offensive security tooling, modern tradecraft, defense evasion, cloud red teaming, adversary emulation, LLM/AI red teaming, training providers, labs, blogs and research. It is intended for authorized penetration tests, red team engagements, purple team exercises and security research only.

> **Last reviewed:** November 2026
> Maintained by [Joas A Santos](https://www.linkedin.com/in/joas-antonio-dos-santos) and the community.
> Issues and pull requests are welcome: [Awesome-Red-Team-Operations issues](https://github.com/JoasASantos/Awesome-Red-Team-Operations/issues)

> **Legal disclaimer:** Every technique and tool listed here must only be used against systems you own or have explicit written authorization to test. Unauthorized access, persistence, data exfiltration or disruption is illegal in most jurisdictions. The maintainers accept no liability for misuse.

---

## Table of Contents

1. [Methodology, Frameworks and Mindmaps](#1-methodology-frameworks-and-mindmaps)
2. [Reconnaissance and OSINT](#2-reconnaissance-and-osint)
3. [Initial Access and Phishing](#3-initial-access-and-phishing)
4. [Payload Development and Malware Tradecraft](#4-payload-development-and-malware-tradecraft)
5. [Defense Evasion](#5-defense-evasion)
6. [PowerShell Offensive Tooling](#6-powershell-offensive-tooling)
7. [Command and Control (C2) Frameworks](#7-command-and-control-c2-frameworks)
8. [C2 Infrastructure, Redirectors and OPSEC](#8-c2-infrastructure-redirectors-and-opsec)
9. [Credential Access and Exfiltration](#9-credential-access-and-exfiltration)
10. [Active Directory Attacks](#10-active-directory-attacks)
11. [Entra ID, Microsoft 365 and Hybrid Identity](#11-entra-id-microsoft-365-and-hybrid-identity)
12. [Lateral Movement](#12-lateral-movement)
13. [Windows Privilege Escalation](#13-windows-privilege-escalation)
14. [Linux Privilege Escalation](#14-linux-privilege-escalation)
15. [macOS and Apple Tradecraft](#15-macos-and-apple-tradecraft)
16. [Pivoting and Tunneling](#16-pivoting-and-tunneling)
17. [Persistence](#17-persistence)
18. [Cloud Red Team Operations](#18-cloud-red-team-operations)
19. [Containers and Kubernetes](#19-containers-and-kubernetes)
20. [Web Application Pentesting](#20-web-application-pentesting)
21. [API, GraphQL and Mobile](#21-api-graphql-and-mobile)
22. [Network, Wireless, Hardware and OT/ICS](#22-network-wireless-hardware-and-otics)
23. [Exploit Development and Buffer Overflow](#23-exploit-development-and-buffer-overflow)
24. [Malware Analysis and Reverse Engineering](#24-malware-analysis-and-reverse-engineering)
25. [Adversary Emulation and Purple Teaming](#25-adversary-emulation-and-purple-teaming)
26. [LLM, AI and Agentic Red Teaming](#26-llm-ai-and-agentic-red-teaming)
27. [Reporting and Collaboration](#27-reporting-and-collaboration)
28. [Wordlists, Cheatsheets and Awesome Lists](#28-wordlists-cheatsheets-and-awesome-lists)
29. [Blogs, Articles, Research and Newsletters](#29-blogs-articles-research-and-newsletters)
30. [Conferences and Talks](#30-conferences-and-talks)
31. [Books](#31-books)
32. [Training, Labs and Certifications](#32-training-labs-and-certifications)
33. [Contributing](#33-contributing)

---

## Modern Tradecraft Highlights (2024-2026)

A quick map of what changed recently and where to look in this document.

- **C2:** AdaptixC2 went from a quiet open-source project to a framework observed in real intrusions (Unit 42, 2025). Sliver, Havoc and Mythic remain the default open-source choices for many teams. Brute Ratel and Nighthawk remain the commercial evasion-first options.
- **Active Directory:** ADCS abuse matured into ESC1-ESC15. Certipy, BloodHound CE, Locksmith and PassTheCert are now standard. BadSuccessor (dMSA abuse, CVE-2025-53779) introduced a new privilege-escalation primitive in Windows Server 2025 domains, and dMSA abuse survived the patch in modified form.
- **Evasion:** indirect syscalls, call-stack spoofing, sleep obfuscation (Ekko/Foliage/Cronos), hardware-breakpoint AMSI/ETW patching, BYOVD and bring-your-own-vulnerable-driver EDR killers.
- **Identity:** device-code phishing, primary refresh token (PRT) abuse, Evilginx-style adversary-in-the-middle, OAuth consent abuse, Entra Connect abuse, TokenTactics/GraphRunner/ROADtools/AADInternals.
- **Cloud:** identity-graph attack paths (BloodHound CE, CloudFox, PMapper, AzureHound), IMDS/SSRF credential theft, CI/CD and artifact poisoning, Kubernetes RBAC and container escape, serverless abuse.
- **AI/LLM:** prompt injection and jailbreaks are now a red team discipline of their own. garak, PyRIT, Promptfoo, DeepTeam and Giskard are the main open-source tools. Agentic and MCP tool-poisoning attacks are the fastest-moving area (OWASP LLM Top 10 2025, OWASP Agentic Top 10, MITRE ATLAS).
- **Detection pressure:** EDR/XDR memory scanning, ETW-TI, AMSI, WDAC, Credential Guard, LSASS PPL, kernel callbacks and cloud identity analytics have forced a shift toward in-process execution, BOFs, living-off-the-land and clean call stacks.

---

## 1. Methodology, Frameworks and Mindmaps

### Frameworks

- [MITRE ATT&CK](https://attack.mitre.org/) - The canonical adversary tactics and techniques knowledge base (Enterprise, Mobile, ICS, Cloud).
- [MITRE ATLAS](https://atlas.mitre.org/) - Adversarial threat landscape for AI systems; the ATT&CK equivalent for ML/LLM.
- [MITRE D3FEND](https://d3fend.mitre.org/) - Defensive countermeasures mapped to ATT&CK.
- [MITRE CALDERA](https://github.com/mitre/caldera) - Automated adversary emulation and autonomous response.
- [MITRE Engenuity ATT&CK Evaluations](https://attackevals.mitre-engenuity.org/) - Vendor detection evaluations and public emulation plans.
- [OWASP Top 10](https://owasp.org/www-project-top-ten/) - Web application risk baseline.
- [OWASP API Security Top 10](https://owasp.org/API-Security/editions/2023/en/0x00-header/) - API-specific risk baseline.
- [OWASP LLM Top 10 (2025)](https://genai.owasp.org/llm-top-10/) - LLM application risks: prompt injection, sensitive disclosure, supply chain, data poisoning, improper output handling, excessive agency and more.
- [OWASP Agentic Security Initiative](https://genai.owasp.org/) - Threat modeling and Top 10 for autonomous agents.
- [OWASP MCP Top 10](https://genai.owasp.org/) - Security risks for Model Context Protocol deployments.
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) - Govern, map, measure, manage.
- [Google SAIF](https://saif.google/) - Secure AI Framework risk map.
- [Cloud Security Alliance MAESTRO](https://cloudsecurityalliance.org/) - Agentic AI threat modeling framework.
- [PTES](http://www.pentest-standard.org/) - Penetration Testing Execution Standard.
- [OSSTMM](https://www.isecom.org/OSSTMM.3.pdf) - Open Source Security Testing Methodology Manual.
- [TIBER-EU](https://www.ecb.europa.eu/pub/pdf/other/ecb.tiber_eu_framework.en.pdf) - Threat intelligence-based ethical red teaming.
- [CBEST](https://www.bankofengland.co.uk/financial-stability) - UK financial-sector intelligence-led testing.
- AADAPT - Azure AD Attack Paths and Techniques.
- [Red Team Development and Operations](https://redteam.guide/) - Joe Vest and James Tubberville's methodology guide.

### Mindmaps by Joas

- [Web Attacks, Bug Bounty and AppSec](https://www.mindmeister.com/pt/1746180947/web-attacks-bug-bounty-and-appsec-by-joas-antonio)
- [Information Security Certifications](https://www.mindmeister.com/pt/1760781948/information-security-certifications-by-joas-antonio)
- [Best Labs and CTF for Red Team and Pentest](https://www.mindmeister.com/pt/1781013629/the-best-labs-and-ctf-red-team-and-pentest)
- [Cyber Security Career Knowledge](https://www.mindmeister.com/pt/1746187693/cyber-security-career-knowledge-by-joas-antonio)

### Engagement Workflow

1. **Scoping and rules of engagement** - targets, exclusions, time windows, escalation contacts, data handling, emergency stop.
2. **Threat modeling** - emulate the adversaries that matter to the client (ransomware, espionage, insider, hacktivist).
3. **Reconnaissance** - external OSINT, infrastructure enumeration, internal discovery.
4. **Initial access** - phishing, valid accounts, exposed services, supply chain.
5. **Foothold and host situational awareness** - who am I, where am I, what is protected.
6. **Privilege escalation and credential access** - local admin, domain identity, cloud identity.
7. **Lateral movement and persistence** - reach the objective without burning the operation.
8. **Collection and exfiltration** - prove impact with controlled, approved data.
9. **Impact demonstration** - domain/tenant/cloud takeover, business disruption scenarios (safely).
10. **Cleanup, reporting and debrief** - remove artifacts, document TTPs, map to ATT&CK, remediation.

---

## 2. Reconnaissance and OSINT

### Attack Surface and Asset Discovery

- [Amass](https://github.com/owasp-amass/amass) - Attack surface mapping and DNS enumeration.
- [Subfinder](https://github.com/projectdiscovery/subfinder) - Passive subdomain enumeration.
- [Assetfinder](https://github.com/tomnomnom/assetfinder) - Find related domains and subdomains.
- [Findomain](https://github.com/Findomain/Findomain) - Cross-platform subdomain monitor.
- [dnsx](https://github.com/projectdiscovery/dnsx) - DNS toolkit and resolver.
- [httpx](https://github.com/projectdiscovery/httpx) - HTTP probing at scale.
- [naabu](https://github.com/projectdiscovery/naabu) - Port scanning for recon pipelines.
- [nuclei](https://github.com/projectdiscovery/nuclei) - Template-based vulnerability scanning.
- [katana](https://github.com/projectdiscovery/katana) - Next-generation crawling and spidering.
- [gau](https://github.com/lc/gau) - Fetch known URLs from AlienVault OTX, Wayback Machine and Common Crawl.
- [waybackurls](https://github.com/tomnomnom/waybackurls) - URLs from the Wayback Machine.
- [hakrawler](https://github.com/hakluke/hakrawler) - Fast web crawler for links and endpoints.
- [gospider](https://github.com/jaeles-project/gospider) - Fast web spider.
- [ParamSpider](https://github.com/devanshbatham/ParamSpider) - Mining parameters from web archives.
- [Arjun](https://github.com/s0md3v/Arjun) - HTTP parameter discovery.
- [x8](https://github.com/Sh1Yo/x8) - Hidden parameter discovery.
- [Kiterunner](https://github.com/assetnote/kiterunner) - API route and endpoint discovery.
- [gowitness](https://github.com/sensepost/gowitness) - Web screenshot reconnaissance.
- [aquatone](https://github.com/michenriksen/aquatone) - Visual inspection of many hosts.
- [EyeWitness](https://github.com/RedSiege/EyeWitness) - Website screenshot and server header inventory.
- [theHarvester](https://github.com/laramies/theHarvester) - Emails, names, hosts and open sources.
- [Photon](https://github.com/s0md3v/Photon) - Fast OSINT web crawler.
- [recon-ng](https://github.com/lanmaster53/recon-ng) - Modular OSINT reconnaissance framework.
- [SpiderFoot](https://github.com/smicallef/spiderfoot) - Automated OSINT correlation.
- [Maltego](https://www.maltego.com/) - Link analysis and graph OSINT (community edition available).
- [Shodan](https://www.shodan.io/) - Internet-connected device search.
- [Censys](https://search.censys.io/) - Internet-wide asset and certificate search.
- [FOFA](https://fofa.info/) - Cyberspace asset search.
- [ZoomEye](https://www.zoomeye.org/) - Cyberspace mapping.
- BinaryEdge - Internet scanning and threat intelligence (now part of Coalition).
- [Netlas](https://netlas.io/) - Internet intelligence and scanning.
- [urlscan.io](https://urlscan.io/) - Website scanning and DOM/network evidence.
- [SecurityTrails](https://securitytrails.com/) - DNS and domain intelligence.
- [crt.sh](https://crt.sh/) - Certificate transparency search.
- [Cert Spotter](https://sslmate.com/certspotter/) - Certificate transparency monitoring.
- [CloudEnum](https://github.com/initstring/cloud_enum) - Multi-cloud public asset enumeration.
- [S3Scanner](https://github.com/sa7mon/S3Scanner) - Find open S3 buckets.
- [GCPBucketBrute](https://github.com/RhinoSecurityLabs/GCPBucketBrute) - GCS bucket enumeration and permission checks.
- [TruffleHog](https://github.com/trufflesecurity/trufflehog) - Secrets discovery in repos, files and pipelines.
- [Gitleaks](https://github.com/gitleaks/gitleaks) - Secrets detection in git history.
- [gitrecon](https://github.com/GONZOsint/gitrecon) - GitHub OSINT.
- [GitHub Dorking](https://github.com/techgaun/github-dorks) - GitHub search dorks for secrets and sensitive files.

### People, Identity and Breach Intelligence

- [Have I Been Pwned](https://haveibeenpwned.com/) - Breach exposure.
- [DeHashed](https://www.dehashed.com/) - Breach and credential search (paid).
- [Intelligence X](https://intelx.io/) - OSINT and leak search.
- [Hunter.io](https://hunter.io/) - Corporate email discovery.
- [Phonebook](https://phonebook.cz/) - Domains, emails and URLs.
- [Sherlock](https://github.com/sherlock-project/sherlock) - Username enumeration across platforms.
- [WhatsMyName](https://github.com/WebBreacher/WhatsMyName) - Username enumeration.
- [LinkedIn Sales Navigator](https://business.linkedin.com/sales-solutions/sales-navigator) - Org chart and employee mapping.
- [CrossLinked](https://github.com/m8sec/CrossLinked) - LinkedIn employee enumeration.
- [TeamsEnum](https://github.com/sse-secure-systems/TeamsEnum) - Microsoft Teams user enumeration.
- [AADInternals](https://github.com/Gerenios/AADInternals) - Tenant reconnaissance from outside.

### Network Reconnaissance

- [Nmap](https://nmap.org/) - The reference port scanner.
- [Masscan](https://github.com/robertdavidgraham/masscan) - Internet-scale port scanning.
- [RustScan](https://github.com/RustScan/RustScan) - Fast port scanner with Nmap integration.
- [Zmap](https://github.com/zmap/zmap) - Fast single-packet network scanning.
- [enum4linux-ng](https://github.com/cddmp/enum4linux-ng) - SMB/NetBIOS enumeration.
- [smbmap](https://github.com/ShawnDEvans/smbmap) - SMB share enumeration and access testing.
- [smbclient](https://www.samba.org/samba/docs/current/man-html/smbclient.1.html) - SMB client.
- [rpcclient](https://www.samba.org/samba/docs/current/man-html/rpcclient.1.html) - RPC enumeration.
- [NetExec](https://github.com/Pennyw0rth/NetExec) - Successor to CrackMapExec; SMB/WinRM/LDAP/MSSQL/SSH protocols and modules.
- [ldapdomaindump](https://github.com/dirkjanm/ldapdomaindump) - Domain dump over LDAP.
- [BloodHound CE](https://github.com/SpecterOps/BloodHound) - Graph-based AD and cloud attack path analysis.
- [adalanche](https://github.com/lkarlslund/adalanche) - AD ACL analysis and visualization.
- [PingCastle](https://github.com/vletoux/pingcastle) - AD security posture assessment.
- [Purple Knight](https://www.semperis.com/purple-knight/) - AD and Entra ID security assessment.
- [ADRecon](https://github.com/sense-of-security/ADRecon) - AD reconnaissance and reporting.
- [ADRecon (adrecon)](https://github.com/adrecon/ADRecon) - Actively maintained fork.
- [ADExplorerSnapshot.py](https://github.com/c3c/ADExplorerSnapshot.py) - Offline AD snapshot analysis.
- [windapsearch](https://github.com/ropnop/windapsearch) - Python LDAP enumeration.
- [ldeep](https://github.com/franc-pentest/ldeep) - LDAP enumeration and dumping.

### DNS, Email and Brand Intelligence

- [DNSRecon](https://github.com/darkoperator/dnsrecon) - DNS enumeration.
- [dnsenum](https://github.com/fwaeytens/dnsenum) - DNS enumeration and zone transfer testing.
- [Fierce](https://github.com/mschwager/fierce) - DNS reconnaissance.
- [Subjack](https://github.com/haccer/subjack) - Subdomain takeover detection.
- [nuclei-templates](https://github.com/projectdiscovery/nuclei-templates) - Takeover and CVE checks.
- [Can-I-Take-Over-XYZ](https://github.com/EdOverflow/can-i-take-over-xyz) - Subdomain takeover fingerprints.
- [dnstwist](https://github.com/elceef/dnstwist) - Typosquatting and phishing domain detection.
- [EvilURL](https://github.com/UndeadSec/EvilURL) - IDN homograph domain generation and detection.
- [DomainHunter](https://github.com/threatexpress/domainhunter) - Expired-domain candidate hunting for red team infrastructure.
- [CatMyFish](https://github.com/Mr-Un1k0d3r/CatMyFish) - Categorized-domain search for whitelisted C2 fronting.
- [FindFrontableDomains](https://github.com/rvrsh3ll/FindFrontableDomains) - Candidate frontable domains.
- [DomainFrontingLists](https://github.com/vysec/DomainFrontingLists) - CDN frontable domain lists.
- [urlcrazy](https://github.com/urbanadventurer/urlcrazy) - Domain typo and variant generation.
- [mailspoof](https://github.com/serain/mailspoof) - SPF/DMARC spoofing checks.
- [spoofcheck](https://github.com/BishopFox/SpoofcheckSelfTest) - SPF/DMARC/DKIM misconfiguration checks.

---

## 3. Initial Access and Phishing

### Phishing Frameworks and Credential Capture

- [GoPhish](https://github.com/gophish/gophish) - Open-source phishing framework.
- [Evilginx3](https://github.com/kgretzky/evilginx2) - Adversary-in-the-middle phishing and session cookie theft.
- [Modlishka](https://github.com/drk1wi/Modlishka) - Reverse-proxy phishing.
- [CredSniper](https://github.com/ustayready/CredSniper) - Phishing framework with 2FA capture.
- [King Phisher](https://github.com/rsmusllp/king-phisher) - Phishing campaign toolkit.
- [Social-Engineer Toolkit (SET)](https://github.com/trustedsec/social-engineer-toolkit) - Classic social engineering framework.
- [ThePhish](https://github.com/emalderson/ThePhish) - Phishing analysis and reporting.
- [Gophish Templates](https://github.com/FreeZeroDays/GoPhish-Templates) - Ready-made campaign templates.
- [Muraena](https://github.com/muraenateam/muraena) - Reverse-proxy phishing with automated session hijacking.
- [NecroBrowser](https://github.com/muraenateam/necrobrowser) - Headless browser for session cookie theft and post-phish automation.
- [PhishCatch](https://github.com/palantir/phishcatch) - Phishing detection browser extension and API server.
- [SquarePhish](https://github.com/secureworks/SquarePhish) - QR-code phishing with device-code flow.
- [QRGen](https://github.com/1r0dm480/QRGen) - QR phishing page generation.
- [TeamsPhisher](https://github.com/Octoberfest7/TeamsPhisher) - Microsoft Teams external phishing.
- [pickl3](https://github.com/hlldz/pickl3) - Microsoft Teams phishing via external access.
- [TokenTactics](https://github.com/rvrsh3ll/TokenTactics) - Azure token abuse for M365.
- [TokenTacticsV2](https://github.com/f-bader/TokenTacticsV2) - Updated token abuse.
- [GraphRunner](https://github.com/dafthack/GraphRunner) - Microsoft Graph post-exploitation toolkit.
- [MFASweep](https://github.com/dafthack/MFASweep) - MFA enforcement probing.
- [TeamFiltration](https://github.com/Flangvik/TeamFiltration) - Teams/O365 enumeration, spraying and exfiltration.
- [o365spray](https://github.com/0xZDH/o365spray) - Microsoft 365 user enumeration and password spraying.
- [CredsLeaker](https://github.com/Dviros/CredsLeaker) - Fake credential prompt.
- [SharpLoginPrompt](https://github.com/shantanu561993/SharpLoginPrompt) - Fake Windows logon prompt.
- [fakelogonscreen](https://github.com/bitsadmin/fakelogonscreen) - Fake logon screen.
- [PinSwipe](https://github.com/CCob/PinSwipe) - Windows Hello PIN capture research.

### Payload Delivery and Container Files

- [Donut](https://github.com/TheWover/donut) - Position-independent shellcode from .NET assemblies, PE files and scripts.
- [CACTUSTORCH](https://github.com/xillwillx/CACTUSTORCH_DDEAUTO) - Shellcode injection via VBScript/JScript and DDEAUTO.
- SharpShooter - Payload generation framework (historical MDSec tool; see archived writeups).
- [DotNetToJScript](https://github.com/tyranid/DotNetToJScript) - .NET execution from JScript/VBScript.
- [VBA-RunPE](https://github.com/itm4n/VBA-RunPE) - Run PE from VBA.
- [MacroPack](https://github.com/sevagas/macro_pack) - Office macro obfuscation and payload generation.
- [LuckyStrike](https://github.com/curi0usJack/luckystrike) - Macro-based payload generator.
- Chameleon - Proxy categorization evasion.
- [RedFile](https://github.com/outflanknl/RedFile) - Conditional payload delivery.
- [keyserver](https://github.com/leoloobeek/keyserver) - HTTP/DNS key delivery for payload protection.
- [pwndrop](https://github.com/kgretzky/pwndrop) - Self-deployable file hosting for payloads.
- [updog](https://github.com/sc0tfree/updog) - Simple HTTP/S file server with upload.
- [mkhtaccess_red](https://github.com/violentlydave/mkhtaccess_red) - Sandbox-aware .htaccess generation.
- [Serving Random Payloads with NGINX](https://gist.github.com/jivoi/a33ace2e25515a31aa2ffbae246d98c9) - Conditional payload serving.
- WSFunnel - Windows Script File payload delivery (historical).
- [ClickOnce](https://learn.microsoft.com/en-us/visualstudio/deployment/clickonce-security-and-deployment) - Signed .application deployment abuse.

### Password Spraying and Credential Attacks

- [DomainPasswordSpray](https://github.com/dafthack/DomainPasswordSpray) - Domain password spraying.
- [DomainPasswordSpray (mdavis332)](https://github.com/mdavis332/DomainPasswordSpray) - Maintained fork.
- [SharpSpray](https://github.com/jnqpblc/SharpSpray) - C# domain password spraying.
- [Spray](https://github.com/Greenwolf/Spray) - Password spraying with lockout awareness.
- [TREVORspray](https://github.com/blacklanternsecurity/TREVORspray) - Password spraying with proxy support.
- [MSOLSpray](https://github.com/dafthack/MSOLSpray) - Microsoft Online spraying.
- [CredMaster](https://github.com/knavesec/CredMaster) - Password spraying via rotating proxies.
- [MailSniper](https://github.com/dafthack/MailSniper) - Exchange and OWA reconnaissance.
- [mimikittenz](https://github.com/putterpanda/mimikittenz) - Extract credentials from process memory.

---

## 4. Payload Development and Malware Tradecraft

### Shellcode, Loaders and Execution

- [Donut](https://github.com/TheWover/donut) - Shellcode generation from .NET, PE and scripts.
- [sRDI](https://github.com/monoxgas/sRDI) - Reflective DLL injection to shellcode.
- [PE2SHC](https://github.com/hasherezade/pe_to_shellcode) - PE to shellcode converter.
- [amber](https://github.com/EgeBalci/amber) - Reflective PE packer.
- [Shhhloader](https://github.com/icyguider/Shhhloader) - Shellcode loader generator with evasion.
- [Nimcrypt2](https://github.com/icyguider/Nimcrypt2) - Nim PE/shellcode packer.
- [Inceptor](https://github.com/klezVirus/inceptor) - Template-based shellcode loader.
- [Freeze](https://github.com/optiv/Freeze) - Payload evasion using suspend and fork.
- [PEzor](https://github.com/phra/PEzor) - Open-source PE packer.
- [ThreadlessInject](https://github.com/CCob/ThreadlessInject) - Threadless process injection.
- [PoolParty](https://github.com/SafeBreach-Labs/PoolParty) - Thread pool injection techniques.
- [Mockingjay](https://github.com/ewby/Mockingjay_BOF) - DLL hollowing into known-good modules (BOF conversion).
- [Process Herpaderping](https://github.com/jxy-s/herpaderping) - Image manipulation to evade scanners.
- [Process Ghosting](https://github.com/hasherezade/process_ghosting) - Execute from a deleted file.
- [Process Doppelganging](https://github.com/hasherezade/process_doppelganging) - Transactional NTFS execution.
- [DInvoke](https://github.com/TheWover/DInvoke) - Dynamic API invocation to avoid static imports.
- [SysWhispers2](https://github.com/jthuraisamy/SysWhispers2) - Direct syscall generation.
- [SysWhispers3](https://github.com/klezvirus/SysWhispers3) - Direct/indirect syscalls with evasion improvements.
- [Hell's Gate](https://github.com/am0nsec/HellsGate) - Syscall number resolution from PEB.
- [FreshyCalls](https://github.com/crummie5/FreshyCalls) - Syscall stub parsing.
- [TartarusGate](https://github.com/trickster0/TartarusGate) - Indirect syscall technique.
- [SilentMoonwalk](https://github.com/klezvirus/SilentMoonwalk) - Call stack spoofing.
- Vulcan - Call stack spoofing research (community implementation).
- [Ekko](https://github.com/Cracked5pider/Ekko) - Sleep obfuscation.
- [Foliage](https://github.com/y11en/FOLIAGE) - Sleep obfuscation.
- [Cronos](https://github.com/Idov31/Cronos) - Sleep obfuscation.
- [DeathSleep](https://github.com/janoglezcampos/DeathSleep) - Sleep obfuscation research.
- [NimPlant](https://github.com/chvancooten/NimPlant) - Nim implant and C2.
- [Nimcrypt](https://github.com/icyguider/Nimcrypt) - Nim crypter.
- [RustSoliloquy](https://github.com/safedv/RustSoliloquy) - Rust implementation of Internal-Monologue.
- [MalDev Academy](https://github.com/MalDev-Academy) - Practical malware development examples.

### BOFs, .NET and In-Memory Execution

- [TrustedSec COFFLoader](https://github.com/trustedsec/COFFLoader) - Standalone BOF loader.
- [CS-Situational-Awareness-BOF](https://github.com/trustedsec/CS-Situational-Awareness-BOF) - Situational awareness BOFs.
- [BOF Collection (rvrsh3ll)](https://github.com/rvrsh3ll/BOF_Collection) - Community BOF collection.
- [InlineExecute-Assembly](https://github.com/anthemtotheego/InlineExecute-Assembly) - In-memory .NET execution.
- [SharpCollection](https://github.com/Flangvik/SharpCollection) - Nightly builds of common C# offensive tools.
- [GhostPack](https://github.com/GhostPack) - Classic C# offensive toolkit (Seatbelt, SharpUp, Rubeus, Certify, SafetyKatz, SharpDPAPI, Lockless and more).
- [SharpSploit](https://github.com/cobbr/SharpSploit) - .NET offensive library.
- [Seatbelt](https://github.com/GhostPack/Seatbelt) - Host situational awareness.
- [SharpUp](https://github.com/GhostPack/SharpUp) - Privilege escalation checks.
- [SharpWMI](https://github.com/GhostPack/SharpWMI) - WMI execution and queries.
- [SharpRDP](https://github.com/0xthirteen/SharpRDP) - RDP command execution.
- [SharpMove](https://github.com/0xthirteen/SharpMove) - Lateral movement toolkit.
- [MoveKit](https://github.com/0xthirteen/MoveKit) - Lateral movement BOFs.
- [SharpCOM](https://github.com/rvrsh3ll/SharpCOM) - COM execution.
- [GhostBuild](https://github.com/bohops/GhostBuild) - MSBuild-based execution.
- [PowerSharpPack](https://github.com/S3cur3Th1sSh1t/PowerSharpPack) - Many C# tools wrapped for PowerShell.
- [Rubeus-Rundll32](https://github.com/rvrsh3ll/Rubeus-Rundll32) - Rubeus via rundll32.
- [Zolom](https://github.com/checkymander/Zolom) - .NET tool wrapper.
- [CSExec](https://github.com/malcomvetter/CSExec) - Service-based execution.

### Reverse Shells and Post-Exploitation Toolkits

- [xc](https://github.com/xct/xc) - Reverse shell generator and listener.
- [pwncat](https://github.com/cytopia/pwncat) - Netcat with advanced features.
- [pwncat-cs](https://github.com/calebstewart/pwncat) - Post-exploitation platform over reverse shells.
- [LOLBITS](https://github.com/Kudaes/LOLBITS) - C2 over BITS.
- [mubix post-exploitation](https://github.com/mubix/post-exploitation) - Post-exploitation scripts.
- [Windows-Post-Exploitation](https://github.com/emilyanncr/Windows-Post-Exploitation) - Windows post-exploitation notes and scripts.
- [Invoke-PowerThIEf](https://github.com/nettitude/Invoke-PowerThIEf) - Outlook and Exchange post-exploitation.
- [BADministration](https://github.com/ThunderGunExpress/BADministration) - Post-exploitation tooling.
- [RunasCs](https://github.com/antonioCoco/RunasCs) - Run as another user with explicit credentials.
- [Invoke-Vnc](https://github.com/klsecservices/Invoke-Vnc) - VNC deployment.
- [Reverse shell generator](https://www.revshells.com/) - Quick reverse shell payloads.
- [PayloadsAllTheThings - Reverse Shell](https://github.com/swisskyrepo/PayloadsAllTheThings) - Reverse shell cheatsheet.

### Packers, Obfuscation and Signing

- [ConfuserEx](https://github.com/mkaring/ConfuserEx) - .NET obfuscator.
- [Obfuscar](https://github.com/obfuscar/obfuscar) - Open-source .NET obfuscator.
- [de4dot](https://github.com/de4dot/de4dot) - .NET deobfuscator (analysis/defense).
- [UPX](https://github.com/upx/upx) - Executable packer.
- [SigThief](https://github.com/secretsquirrel/SigThief) - Signature theft.
- [LimeLighter](https://github.com/Tylous/Limelighter) - Code signing abuse.
- [SigFlip](https://github.com/med0x2e/SigFlip) - Authenticode hash manipulation.
- [Mangle](https://github.com/optiv/Mangle) - PE manipulation and signature preservation.

---

## 5. Defense Evasion

> The most important rule: know what telemetry your action generates before you run it. Modern EDRs detect behavior, call stacks, memory patterns and cloud identity anomalies, not just static strings.

### AMSI, ETW and Script Controls

- [Amsi-Bypass-Powershell](https://github.com/S3cur3Th1sSh1t/Amsi-Bypass-Powershell) - Collected AMSI bypass techniques.
- [AMSI.fail](https://github.com/Flangvik/AMSI.fail) - Obfuscated AMSI bypass generator.
- [AmsiScanBufferBypass](https://github.com/rasta-mouse/AmsiScanBufferBypass) - Classic patch research.
- [AMSI_Ordinal_Bypass](https://github.com/rmdavy/AMSI_Ordinal_Bypass) - Ordinal-based bypass.
- [AMSITrigger](https://github.com/RythmStick/AMSITrigger) - Find AMSI-triggering strings.
- [Stracciatella](https://github.com/mgeeky/Stracciatella) - PowerShell AMSI bypass obfuscation.
- [NoAmci](https://github.com/med0x2e/NoAmci) - AMSI patching via hardware breakpoints.
- [SharpBlock](https://github.com/CCob/SharpBlock) - Block AMSI/ETW in child processes.
- [Invisi-Shell](https://github.com/OmerYa/Invisi-Shell) - Hide PowerShell from logging.
- [InsecurePowerShell](https://github.com/cobbr/InsecurePowerShell) - PowerShell without security features.
- [PowerShdll](https://github.com/p3nt4/PowerShdll) - PowerShell without powershell.exe.
- PSAttack - Offensive PowerShell environment.
- [p0wnedShell](https://github.com/Cn33liz/p0wnedShell) - PowerShell runspace and offensive shell.
- [nopowershell](https://github.com/bitsadmin/nopowershell) - PowerShell rebuilt in C#.
- [PowerLessShell](https://github.com/Mr-Un1k0d3r/PowerLessShell) - Run PowerShell without powershell.exe.
- [MSBuildShell](https://github.com/Cn33liz/MSBuildShell) - PowerShell via MSBuild.
- [NoMSBuild](https://github.com/rvrsh3ll/NoMSBuild) - MSBuild evasion.
- [PowerShellArmoury](https://github.com/cfalta/PowerShellArmoury) - Offensive PowerShell toolkit.
- [Salsa-tools](https://github.com/Hackplayers/Salsa-tools) - PowerShell tooling.
- [PSByPassCLM](https://github.com/padovah4ck/PSByPassCLM) - Constrained Language Mode bypass.
- [SpaceRunner](https://github.com/Mr-B0b/SpaceRunner) - AppLocker/WDAC execution research.
- [UltimateWDACBypassList](https://github.com/bohops/UltimateWDACBypassList) - WDAC bypass collection.
- [LOLBAS](https://lolbas-project.github.io/) - Living Off The Land Binaries, Scripts and Libraries.
- [GTFOBins](https://gtfobins.github.io/) - Unix binaries for privilege escalation and evasion.
- [LOLDrivers](https://www.loldrivers.io/) - Vulnerable and malicious drivers.
- [Living Off Trusted Sites](https://lots-project.com/) - Trusted-domain C2 and delivery.

### Syscalls, Unhooking and Memory Evasion

- [Hell's Gate](https://github.com/am0nsec/HellsGate) - Syscall number extraction.
- [SysWhispers2](https://github.com/jthuraisamy/SysWhispers2) - Syscall stub generation.
- [SysWhispers3](https://github.com/klezvirus/SysWhispers3) - Indirect syscalls and evasion.
- [FreshyCalls](https://github.com/crummie5/FreshyCalls) - Syscall stub parsing.
- [TartarusGate](https://github.com/trickster0/TartarusGate) - Indirect syscall research.
- [SilentMoonwalk](https://github.com/klezvirus/SilentMoonwalk) - Stack spoofing.
- Vulcan - Stack spoofing research (community implementation).
- [Ekko](https://github.com/Cracked5pider/Ekko) - Sleep obfuscation with ROP.
- [Foliage](https://github.com/y11en/FOLIAGE) - Sleep obfuscation.
- [Cronos](https://github.com/Idov31/Cronos) - Sleep obfuscation.
- [DeathSleep](https://github.com/janoglezcampos/DeathSleep) - Sleep obfuscation.
- [Mockingjay](https://github.com/ewby/Mockingjay_BOF) - DLL hollowing research (BOF conversion).
- [ThreadlessInject](https://github.com/CCob/ThreadlessInject) - Threadless injection.
- [PoolParty](https://github.com/SafeBreach-Labs/PoolParty) - Thread pool injection.

### EDR Enumeration, BYOVD and Tampering

- [EDRSilencer](https://github.com/netero1010/EDRSilencer) - Block EDR telemetry using Windows Filtering Platform.
- [Terminator](https://github.com/ZeroMemoryEx/Terminator) - BYOVD EDR termination.
- [Krueger](https://github.com/logangoins/Krueger) - BYOVD and WDAC-based EDR termination.
- [EDRaser](https://github.com/SafeBreach-Labs/EDRaser) - EDR telemetry tampering research.
- [Backstab](https://github.com/Yaxser/Backstab) - Kill protected processes via driver.
- [PPLdump](https://github.com/itm4n/PPLdump) - Dump PPL processes.
- [PPLmedic](https://github.com/itm4n/PPLmedic) - PPL bypass research.
- [Microsoft driver blocklist](https://learn.microsoft.com/en-us/windows/security/application-security/application-control/app-control-for-business/design/microsoft-recommended-driver-block-rules) - Driver blocklist (defense awareness).
- [Windows Defender exclusions](https://learn.microsoft.com/en-us/defender-endpoint/configure-exclusions-microsoft-defender-antivirus) - Abuse of exclusion paths (detectable).

### Process Injection and Execution

- [Process Doppelganging](https://github.com/hasherezade/process_doppelganging) - Transactional NTFS.
- [Process Ghosting](https://github.com/hasherezade/process_ghosting) - Deleted-file execution.
- [Process Herpaderping](https://github.com/jxy-s/herpaderping) - Image tampering.
- [Mockingjay](https://github.com/ewby/Mockingjay_BOF) - Module hollowing (BOF conversion).
- [PoolParty](https://github.com/SafeBreach-Labs/PoolParty) - Thread pool injection.
- [ThreadlessInject](https://github.com/CCob/ThreadlessInject) - Threadless injection.
- [EarlyBird injection](https://www.ired.team/offensive-security/code-injection-process-injection/early-bird-apc-queue-code-injection) - APC injection before thread start.
- [Fiber execution](https://www.ired.team/offensive-security/code-injection-process-injection/executing-shellcode-with-createfiber) - Fiber-based execution.
- [Callback execution](https://attack.mitre.org/techniques/T1055/) - Enum/console/event callbacks.

### Application Control and Sandbox Evasion

- [UltimateAppLockerByPassList](https://github.com/api0cradle/UltimateAppLockerByPassList) - AppLocker bypasses.
- [UltimateWDACBypassList](https://github.com/bohops/UltimateWDACBypassList) - WDAC bypasses.
- [PSByPassCLM](https://github.com/padovah4ck/PSByPassCLM) - Constrained Language Mode.
- [al-khaser](https://github.com/LordNoteworthy/al-khaser) - Anti-analysis and sandbox checks.
- [pafish](https://github.com/a0rtega/pafish) - Paranoid fish sandbox detection.

### Logging and Telemetry Evasion

- [SwiftOnSecurity sysmon-config](https://github.com/SwiftOnSecurity/sysmon-config) - Understand what defenders collect.
- [Invoke-Phant0m](https://github.com/hlldz/Invoke-Phant0m) - Kill event log threads.
- [NoAmci](https://github.com/med0x2e/NoAmci) - Hardware-breakpoint AMSI/ETW patching.
- [ETW research](https://www.ired.team/miscellaneous-reversing-forensics/windows-kernel-internals/etw-event-tracing-for-windows-101) - ETW internals and suppression.

---

## 6. PowerShell Offensive Tooling

- [PowerSploit](https://github.com/PowerShellMafia/PowerSploit) - The foundational offensive PowerShell suite.
- [PowerTools](https://github.com/PowerShellEmpire/PowerTools) - Original Empire-era PowerShell tools.
- [nishang](https://github.com/samratashok/nishang) - PowerShell for penetration testing.
- PowerOPS - PowerShell runspace offensive tool (archived).
- [PowerMemory](https://github.com/giMini/PowerMemory) - Credential and memory operations.
- [PowerShell-Suite](https://github.com/FuzzySecurity/PowerShell-Suite) - FuzzySecurity tooling.
- [PowerShellArmoury](https://github.com/cfalta/PowerShellArmoury) - Modular offensive PowerShell.
- [WinPwn](https://github.com/S3cur3Th1sSh1t/WinPwn) - Recon and privilege escalation automation.
- [Inveigh](https://github.com/Kevin-Robertson/Inveigh) - LLMNR/NBT-NS/mDNS/DHCPv6 spoofing and relay.
- [Powermad](https://github.com/Kevin-Robertson/Powermad) - Machine account and Kerberos abuse.
- [DSInternals](https://github.com/MichaelGrafnetter/DSInternals) - AD database and crypto tooling.
- [LAPSToolkit](https://github.com/leoloobeek/LAPSToolkit) - LAPS enumeration and abuse.
- [LAPSDumper](https://github.com/n00py/LAPSDumper) - LAPS password extraction.
- [Grouper](https://github.com/S3cur3Th1sSh1t/Grouper) - Group Policy password mining.
- [Grouper2](https://github.com/l0ss/Grouper2) - GPO misconfiguration analysis.
- [ADRecon](https://github.com/sense-of-security/ADRecon) - AD recon and reporting.
- [PowerUpSQL](https://github.com/NetSPI/PowerUpSQL) - SQL Server attack toolkit.
- [NetSPI PowerShell](https://github.com/NetSPI/PowerShell) - NetSPI offensive modules.
- [Invoke-Phant0m](https://github.com/hlldz/Invoke-Phant0m) - Event log thread termination.
- [MailSniper](https://github.com/dafthack/MailSniper) - Exchange/OWA recon.
- [SessionGopher](https://github.com/Arvanaghi/SessionGopher) - Extract saved sessions and credentials.
- [mimikittenz](https://github.com/putterpanda/mimikittenz) - Process memory credential extraction.
- [PowerSharpPack](https://github.com/S3cur3Th1sSh1t/PowerSharpPack) - C# tools in PowerShell.
- [SharpCollection](https://github.com/Flangvik/SharpCollection) - Compiled .NET offensive tools.

---

## 7. Command and Control (C2) Frameworks

### Framework Comparison

| Framework | Type | Transports | Notes |
|---|---|---|---|
| [AdaptixC2](https://github.com/Adaptix-Framework/AdaptixC2) | Open source, Go server + Qt client | HTTP/S, DNS/DoH, SMB, TCP, mTLS Gopher | Highly modular, plugin listeners/agents, BOF support, seen in real intrusions in 2025 |
| [Sliver](https://github.com/BishopFox/sliver) | Open source, Go | mTLS, WireGuard, HTTP/S, DNS | Cross-platform implants, armory packages, BOFs, per-binary obfuscation |
| [Havoc](https://github.com/HavocFramework/Havoc) | Open source, Go server + C/C++ agent | HTTP/S, SMB, TCP | Demon agent with sleep obfuscation, indirect syscalls, stack spoofing |
| [Mythic](https://github.com/its-a-feature/Mythic) | Open source platform | HTTP, WebSocket, DNS, SMB, custom | Agent-agnostic: Apollo (.NET), Poseidon (Go) and community agents |
| [Cobalt Strike](https://www.cobaltstrike.com/) | Commercial | HTTP/S, DNS, SMB, TCP, custom | Beacon, malleable profiles, BOFs, mature ecosystem |
| [Brute Ratel C4](https://bruteratel.com/) | Commercial | HTTP/S, DNS, SMB, TCP | Evasion-focused, badger agent |
| [Nighthawk](https://nighthawkc2.io/) | Commercial | HTTP/S, SMB, custom | MDSec evasion-first C2 |
| [PoshC2](https://github.com/nettitude/PoshC2) | Open source | HTTP/S, DNS, SMB | Proxy-aware, PowerShell/Python/C# implants |
| [Empire](https://github.com/BC-SECURITY/Empire) | Open source | HTTP/S, custom | PowerShell, Python and C# agents |
| [Covenant](https://github.com/cobbr/Covenant) | Open source | HTTP/S, SMB, custom | .NET C2, Grunt and Elite agents |
| [Merlin](https://github.com/Ne0nd0g/merlin) | Open source, Go | HTTP/2, HTTP/3, DNS | Cross-platform agent |
| [NimPlant](https://github.com/chvancooten/NimPlant) | Open source, Nim | HTTP/S | Lightweight Nim implant |
| [Deimos C2](https://github.com/DeimosC2/DeimosC2) | Open source, Go | HTTP/S, TCP | Modular C2 with agents |
| [SharpC2](https://github.com/rasta-mouse/SharpC2) | Open source, .NET | HTTP/S, SMB, TCP | .NET C2 with teamserver |
| [Villain](https://github.com/t3l3machus/Villain) | Open source | HTTP/S, TCP | C2 with payload generation |
| [Metasploit](https://github.com/rapid7/metasploit-framework) | Open source | TCP, HTTP/S, custom | Meterpreter and exploit modules |
| [SILENTTRINITY](https://github.com/byt3bl33d3r/SILENTTRINITY) | Open source | HTTP/S | Python/IronPython/.NET agent |
| [Pupy](https://github.com/n1nj4sec/pupy) | Open source | HTTP/S, custom | Cross-platform RAT and post-exploitation |
| Koadic | Open source | HTTP/S | COM-based Windows post-exploitation (archived) |
| [TrevorC2](https://github.com/trustedsec/trevorc2) | Open source | HTTP/S | Legitimate-website tunneling |
| [Gcat](https://github.com/byt3bl33d3r/gcat) | Open source | Gmail | Gmail-based covert C2 |
| [EvilOSX](https://github.com/Marten4n6/EvilOSX) | Open source | HTTP/S | macOS RAT |
| [EggShell](https://github.com/neoneggplant/EggShell) | Open source | HTTP/S | macOS/Linux surveillance |
| [DNScat2](https://github.com/iagox86/dnscat2) | Open source | DNS | Encrypted DNS C2 |
| [FactionC2](https://github.com/FactionC2/) | Open source | WebSocket | WebSocket-based C2 |
| [QuasarRAT](https://github.com/quasar/QuasarRAT) | Open source | TCP | .NET RAT (authorized testing) |
| [C3](https://github.com/FSecureLABS/C3) | Open source | Custom | Custom command and control framework |

### Framework Deep Dives

- [AdaptixC2](https://github.com/Adaptix-Framework/AdaptixC2) - Go teamserver, C++/Qt client, plugin listeners and agents, BOF and async BOF, SOCKS4/5, port forwarding, kill date and working time. Unit 42 documented real-world use in 2025.
- [Adaptix documentation](https://adaptix-framework.gitbook.io/adaptix-framework) - Install, extenders and usage.
- [Adaptix Extension-Kit](https://github.com/Adaptix-Framework/Extension-Kit) - Official extension kit.
- [Sliver](https://github.com/BishopFox/sliver) - Bishop Fox's cross-platform adversary emulation framework.
- [Sliver documentation](https://sliver.sh/) - Official docs.
- [Sliver Armory](https://github.com/sliverarmory) - BOFs, extensions and packages.
- [Havoc](https://github.com/HavocFramework/Havoc) - Demon agent with Ekko/Zilean/FOLIAGE sleep obfuscation, indirect syscalls, stack spoofing, SMB and token vault.
- [Mythic](https://github.com/its-a-feature/Mythic) - Agent-agnostic C2 platform.
- [Mythic docs](https://docs.mythic-c2.net/) - Official docs.
- [Apollo](https://github.com/MythicAgents/Apollo) - .NET Windows agent.
- [Poseidon](https://github.com/MythicAgents/poseidon) - Go Linux/macOS agent.
- [Cobalt Strike](https://www.cobaltstrike.com/) - Beacon and malleable C2.
- [Malleable C2 Profiles](https://github.com/rsmudge/Malleable-C2-Profiles) - Profile collection.
- [Malleable-C2-Randomizer](https://github.com/bluscreenofjeff/Malleable-C2-Randomizer) - Randomize profiles.
- [Malleable C2 Profiles (xx0hcd)](https://github.com/xx0hcd/Malleable-C2-Profiles) - Additional profiles.
- [cs2modrewrite](https://github.com/threatexpress/cs2modrewrite) - Cobalt Strike to mod_rewrite.
- [e2modrewrite](https://github.com/infosecn1nja/e2modrewrite) - Empire to mod_rewrite.
- [CobaltStrike-ToolKit](https://github.com/killswitch-GUI/CobaltStrike-ToolKit) - Useful scripts.
- [ExternalC2](https://github.com/ryhanson/ExternalC2) - Cobalt Strike External C2 library.
- [external_c2_framework](https://github.com/Und3rf10w/external_c2_framework) - External C2 framework.
- [DoHC2](https://github.com/SpiderLabs/DoHC2) - ExternalC2 over DNS over HTTPS.
- [PoshC2](https://github.com/nettitude/PoshC2) - Proxy-aware C2.
- [Empire](https://github.com/BC-SECURITY/Empire) - BC Security Empire.
- [Covenant](https://github.com/cobbr/Covenant) - .NET C2.
- [Merlin](https://github.com/Ne0nd0g/merlin) - HTTP/2 C2.
- [NimPlant](https://github.com/chvancooten/NimPlant) - Nim C2.
- [Deimos C2](https://github.com/DeimosC2/DeimosC2) - Modular C2.
- [SharpC2](https://github.com/rasta-mouse/SharpC2) - .NET C2.
- [Villain](https://github.com/t3l3machus/Villain) - C2 and payload generator.
- [C3](https://github.com/FSecureLABS/C3) - Custom C2.
- [Mythic C2 Profiles](https://github.com/MythicC2Profiles) - Transport profiles.
- [Havoc profiles](https://github.com/HavocFramework/Havoc/tree/main/profiles) - Example profiles.

### Legacy and Archived C2 References

- [Cobalt Strike](https://cobaltstrike.com/) - Official site (also https://www.cobaltstrike.com).
- [EmpireProject/Empire](https://github.com/EmpireProject/Empire) - Original Empire repository (legacy; use BC-SECURITY/Empire).
- [PoshC2_Python](https://github.com/nettitude/PoshC2_Python) - Original PoshC2 Python repository (legacy).
- [Covenant](https://github.com/cobbr/Covenant) - Development largely stalled; still useful for .NET research.

### C2 Selection Notes

- **AdaptixC2** is the newest open-source framework to gain real-world attention. It is plugin-driven, supports BOFs and async BOFs, and has a clean Qt client. Its defaults are fingerprinted (`Server: AdaptixC2`, `Adaptix-Version`), so profile and error-page customization is mandatory.
- **Sliver** is the pragmatic cross-platform default. Use mTLS or WireGuard, customize the HTTP profile, avoid default JARM/JA3, and use `garble` symbol obfuscation.
- **Havoc** is strong when memory-scanning EDR is the obstacle: sleep obfuscation, indirect syscalls and return-address spoofing are built in.
- **Mythic** is the best choice for multi-operator, multi-agent campaigns where you want to swap agent and transport independently.
- **Cobalt Strike** remains the most mature ecosystem, but default profiles and teamserver fingerprints are heavily detected. Treat every default as burned.
- **Brute Ratel and Nighthawk** are commercial and evasion-first, but they are also increasingly fingerprinted. Validate against the target's actual EDR.

### BOFs and Post-Exploitation Extensions

- [TrustedSec COFFLoader](https://github.com/trustedsec/COFFLoader) - Standalone BOF loader.
- [CS-Situational-Awareness-BOF](https://github.com/trustedsec/CS-Situational-Awareness-BOF) - Situational awareness BOFs.
- [BOF Collection](https://github.com/rvrsh3ll/BOF_Collection) - Community BOFs.
- [Sliver Armory](https://github.com/sliverarmory) - Sliver packages.
- [Adaptix Extension-Kit](https://github.com/Adaptix-Framework/Extension-Kit) - Adaptix plugins.
- [InlineExecute-Assembly](https://github.com/anthemtotheego/InlineExecute-Assembly) - In-memory .NET execution.

---

## 8. C2 Infrastructure, Redirectors and OPSEC

### Infrastructure Automation

- [RAI (Rapid Attack Infrastructure)](https://github.com/obscuritylabs/RAI) - Teamserver, domains, redirectors and phishing infrastructure.
- Red-Baron - Terraform-based resilient infrastructure (archived).
- RedTeam-Automation - Automated Empire infrastructure (archived).
- [redi](https://github.com/taherio/redi) - Cobalt Strike redirectors with nginx and Let's Encrypt.
- [ycsm](https://github.com/infosecn1nja/ycsm) - Resilient nginx redirector for Cobalt Strike, Empire, Metasploit and PoshC2.
- [Apache2-Mod-Rewrite-Setup](https://github.com/n0pe-sled/Apache2-Mod-Rewrite-Setup) - Quick mod_rewrite setup.
- [Postfix-Server-Setup](https://github.com/n0pe-sled/Postfix-Server-Setup) - Phishing mail server setup.
- [cat-sites](https://github.com/audrummer15/cat-sites) - Site categorization library.
- [DomainHunter](https://github.com/threatexpress/domainhunter) - Aged and categorized domain hunting.
- Chameleon - Proxy categorization evasion.
- [EvilURL](https://github.com/UndeadSec/EvilURL) - IDN homograph domains.
- PowerDNS - PowerShell over DNS (archived MDSec research).
- [meek](https://github.com/arlolra/meek) - Blocking-resistant Tor pluggable transport.
- [HTran](https://github.com/HiwinCN/HTran) - Connection bouncer and proxy.
- [Google Domain Fronting](https://github.com/redteam-cyberark/Google-Domain-fronting) - Historical domain-fronting research.
- [DomainFrontDiscover](https://github.com/peewpw/DomainFrontDiscover) - CloudFront frontable-domain discovery.

### Redirectors, Proxies and Filtering

- [nginx](https://nginx.org/) - Reverse proxy and redirector workhorse.
- [Caddy](https://caddyserver.com/) - Automatic TLS reverse proxy.
- [Traefik](https://traefik.io/) - Cloud-native reverse proxy.
- [HAProxy](https://www.haproxy.org/) - High-availability proxy.
- [Socat](https://linux.die.net/man/1/socat) - Multipurpose relay.
- [Stunnel](https://www.stunnel.org/) - TLS wrapper.
- [mod_rewrite sandbox evasion](https://gist.github.com/curi0usJack/971385e8334e189d93a6cb4671238b10) - Sandbox-aware redirects.
- [mkhtaccess_red](https://github.com/violentlydave/mkhtaccess_red) - Automated sandbox blocking.
- [RedFile](https://github.com/outflanknl/RedFile) - Conditional file delivery.
- [keyserver](https://github.com/leoloobeek/keyserver) - Key delivery for payload protection.
- [C2-Tracker](https://github.com/montysecurity/C2-Tracker) - C2 infrastructure intelligence (defense awareness).

### OPSEC Checklist

- Separate long-haul and short-haul infrastructure; never touch both from the same host.
- Use aged, categorized domains; avoid lookalikes that trigger brand monitoring.
- Customize TLS, HTTP headers, error pages, JARM/JA3 and beacon metadata.
- Use redirectors with allow-lists; never expose the teamserver directly.
- Keep per-target payloads, certificates and keys unique.
- Respect kill dates and working hours; avoid noisy actions during incident response windows.
- Never reuse credentials, implants or domains across engagements.
- Assume every artifact is collected: timestamps, user agents, DNS, TLS, file hashes, command lines and cloud audit logs.
- Log operator actions for the report and for deconfliction with the blue team.

---

## 9. Credential Access and Exfiltration

### Windows Credential Access

- [mimikatz](https://github.com/gentilkiwi/mimikatz) - The reference Windows credential extraction toolkit.
- [SafetyKatz](https://github.com/GhostPack/SafetyKatz) - Safer mimikatz execution.
- [BetterSafetyKatz](https://github.com/Flangvik/BetterSafetyKatz) - Fetches and patches mimikatz in memory.
- [Rubeus](https://github.com/GhostPack/Rubeus) - Kerberos abuse (AS-REP, Kerberoast, S4U, tickets, relays).
- [SharpKatz](https://github.com/b4rtik/SharpKatz) - C# port of key mimikatz modules.
- [Dumpert](https://github.com/outflanknl/Dumpert) - LSASS dump via direct syscalls and API unhooking.
- [SharpMiniDump](https://github.com/b4rtik/SharpMiniDump) - Minidump LSASS using Dumpert.
- [ATPMiniDump](https://github.com/b4rtik/ATPMiniDump) - Evade Defender ATP credential theft.
- [Nanodump](https://github.com/helpsystems/nanodump) - Flexible LSASS dumping.
- [lsassy](https://github.com/Hackndo/lsassy) - Remote LSASS parsing.
- [spraykatz](https://github.com/aas-n/spraykatz) - Remote procdump and pypykatz analysis.
- [pypykatz](https://github.com/skelsec/pypykatz) - Python mimikatz implementation.
- [SharpDPAPI](https://github.com/GhostPack/SharpDPAPI) - DPAPI credential and blob decryption.
- [SharpChromium](https://github.com/djhohnstein/SharpChromium) - Chromium cookies, history and logins.
- [SharpWeb](https://github.com/djhohnstein/SharpWeb) - Browser credential gathering.
- [HackBrowserData](https://github.com/moonD4rk/HackBrowserData) - Browser data extraction.
- [SharpClipHistory](https://github.com/mwrlabs/SharpClipHistory) - Clipboard history extraction.
- [SharpHandler](https://github.com/jfmaes/SharpHandler) - Reuse open LSASS handles.
- [SharpSecDump](https://github.com/G0ldenGunSec/SharpSecDump) - Remote SAM/LSA secrets.
- [DecryptAutoLogon](https://github.com/securesean/DecryptAutoLogon) - Decrypt Sysinternals AutoLogon passwords.
- [Internal-Monologue](https://github.com/eladshamir/Internal-Monologue) - Internal NTLM challenge without network traffic.
- [RdpThief](https://github.com/0x09AL/RdpThief) - Extract live RDP credentials.
- [Invoke-WCMDump](https://github.com/peewpw/Invoke-WCMDump) - Credential Manager dump.
- [SessionGopher](https://github.com/Arvanaghi/SessionGopher) - Session and saved-credential extraction.
- [LaZagneForensic](https://github.com/AlessandroZ/LaZagneForensic) - Remote LaZagne.
- [LaZagne](https://github.com/AlessandroZ/LaZagne) - Multi-application credential recovery.
- [Gopher](https://github.com/EncodeGroup/Gopher) - Low-hanging credential discovery.
- [SharpCloud](https://github.com/chrismaddalena/SharpCloud) - AWS/Azure/GCP credential file discovery.
- [SharpScribbles](https://github.com/V1V1/SharpScribbles) - Firefox credentials and sticky notes.
- [sAINT](https://github.com/tiagorlampert/sAINT) - Credential collection.
- [KeeThief](https://github.com/GhostPack/KeeThief) - KeePass credential extraction.
- [SharpSCCM](https://github.com/Mayyhem/SharpSCCM) - SCCM attack toolkit.
- [SCCMHunter](https://github.com/garrettfoster13/sccmhunter) - SCCM reconnaissance and exploitation.
- [Certipy](https://github.com/ly4k/Certipy) - ADCS enumeration, request and abuse.
- [Certify](https://github.com/GhostPack/Certify) - ADCS enumeration.
- [ForgeCert](https://github.com/GhostPack/ForgeCert) - Forge certificates.
- [PassTheCert](https://github.com/AlmondOffSec/PassTheCert) - Authenticate with certificates.

### Linux and macOS Credential Access

- [mimipenguin](https://github.com/huntergregal/mimipenguin) - Linux credential extraction.
- [mimipy](https://github.com/n1nj4sec/mimipy) - Linux credential extraction.
- [3snake](https://github.com/blendin/3snake) - SSH/sudo/su credential capture.
- [sshLooterC](https://github.com/mthbernardes/sshLooterC) - SSH credential loot.
- [gimmecredz](https://github.com/0xmitsurugi/gimmecredz) - Credential harvesting.
- [tickey](https://github.com/TarlogicSecurity/tickey) - Extract Kerberos tickets from Linux kernel keyrings.
- [KeyTabExtract](https://github.com/sosdave/KeyTabExtract) - Keytab analysis.
- [Linikatz](https://github.com/CiscoCXSecurity/linikatz) - Linux AD credential extraction.
- [dirtycow](https://github.com/dirtycow/dirtycow.github.io) - Historical Linux privilege escalation.

### Cloud Credential Access

- [HackTricks Cloud](https://cloud.hacktricks.wiki/) - Cloud attack techniques.
- [AADInternals](https://github.com/Gerenios/AADInternals) - Token and identity abuse.
- [ROADtools](https://github.com/dirkjanm/ROADtools) - Entra ID enumeration and token use.
- [TokenTactics](https://github.com/rvrsh3ll/TokenTactics) - Token acquisition and abuse.
- [GraphRunner](https://github.com/dafthack/GraphRunner) - Microsoft Graph post-exploitation.
- [TeamFiltration](https://github.com/Flangvik/TeamFiltration) - M365 exfiltration.

### Data Exfiltration

- [Egress-Assess](https://github.com/FortyNorthSecurity/Egress-Assess) - Egress testing and data exfiltration.
- [Invoke-TmpDavFS](https://github.com/p3nt4/Invoke-TmpDavFS) - Temporary WebDAV file system.
- [icmptunnel](https://github.com/DhavalKapil/icmptunnel) - ICMP tunneling.
- [dnscat2](https://github.com/iagox86/dnscat2) - DNS C2 and exfiltration.
- [DNSExfiltrator](https://github.com/Arno0x/DNSExfiltrator) - DNS exfiltration.
- [DNSlivery](https://github.com/no0be/DNSlivery) - File and payload delivery over DNS.
- [FlyingCarpet](https://github.com/spieglt/FlyingCarpet) - Wi-Fi exfiltration.
- [Tunna](https://github.com/SECFORCE/Tunna) - TCP over HTTP tunneling.
- [chashell](https://github.com/sysdream/chashell) - HTTP(S) shell.
- [PowerLessShell](https://github.com/Mr-Un1k0d3r/PowerLessShell) - Payload execution without PowerShell.
- [rclone](https://rclone.org/) - Cloud storage exfiltration.
- [PacketWhisper](https://github.com/TryCatchHCF/PacketWhisper) - DNS exfiltration.
- [DET](https://github.com/sensepost/DET) - Data exfiltration toolkit.
- [Sliver](https://github.com/BishopFox/sliver) - Built-in upload/download.

---

## 10. Active Directory Attacks

### Enumeration and Attack Paths

- [BloodHound CE](https://github.com/SpecterOps/BloodHound) - Graph analysis of AD and Entra ID attack paths.
- [SharpHound](https://github.com/SpecterOps/SharpHound) - C# collector for BloodHound.
- [AzureHound](https://github.com/SpecterOps/AzureHound) - Entra ID collector.
- [BloodHoundQueries](https://github.com/CompassSecurity/BloodHoundQueries) - Query packs.
- [awesome-bloodhound](https://github.com/chryzsh/awesome-bloodhound) - BloodHound resources.
- [Bloodhound-Custom-Queries](https://github.com/hausec/Bloodhound-Custom-Queries) - Custom queries.
- [ADACLScanner](https://github.com/canix1/ADACLScanner) - ACL enumeration and reporting.
- [ACLight](https://github.com/cyberark/ACLight) - Privileged account discovery.
- [Invoke-ACLPwn](https://github.com/fox-it/Invoke-ACLPwn) - ACL abuse.
- [dacledit.py](https://github.com/fortra/impacket) - DACL editing via Impacket.
- [ADCollector](https://github.com/dev-2null/ADCollector) - AD recon.
- [ADAPE-Script](https://github.com/hausec/ADAPE-Script) - Automated AD assessment.
- [PingCastle](https://github.com/vletoux/pingcastle) - AD risk assessment.
- [Purple Knight](https://www.semperis.com/purple-knight/) - AD/Entra assessment.
- [Locksmith](https://github.com/TrimarcJake/Locksmith) - ADCS misconfiguration scanner and fixer.
- [ADCSKiller](https://github.com/grimlockx/ADCSKiller) - ADCS exploitation automation.
- [Certipy](https://github.com/ly4k/Certipy) - The standard ADCS attack tool.
- [Certify](https://github.com/GhostPack/Certify) - ADCS enumeration.
- [PSPKIAudit](https://github.com/GhostPack/PSPKIAudit) - ADCS audit.
- [Certified Pre-Owned](https://posts.specterops.io/certified-pre-owned-d95910965cd2) - The ADCS whitepaper.

### Legacy AD Tooling (Historical Reference)

- [BloodHound (legacy)](https://github.com/BloodHoundAD/BloodHound) - Original BloodHound repository.
- [SharpHound3 (legacy)](https://github.com/BloodHoundAD/SharpHound3) - Original SharpHound collector.
- [SharpGPOAbuse (mwrlabs)](https://github.com/mwrlabs/SharpGPOAbuse) - Original GPO abuse tool.

### Kerberos Abuse

- [Rubeus](https://github.com/GhostPack/Rubeus) - Kerberos request, roast, relay and ticket abuse.
- [Kerbrute](https://github.com/ropnop/kerbrute) - User enumeration and password spraying over Kerberos.
- [GetNPUsers.py](https://github.com/fortra/impacket) - AS-REP roasting.
- [GetUserSPNs.py](https://github.com/fortra/impacket) - Kerberoasting.
- [ticketer.py](https://github.com/fortra/impacket) - Golden and silver tickets.
- [Kekeo](https://github.com/gentilkiwi/kekeo) - Kerberos toolkit.
- [KrbRelayUp](https://github.com/Dec0ne/KrbRelayUp) - Local privilege escalation via Kerberos relay.
- [KrbRelay](https://github.com/cube0x0/KrbRelay) - Kerberos relay framework.
- [RemotePotato0](https://github.com/antonioCoco/RemotePotato0) - Cross-session relay.
- [PetitPotam](https://github.com/topotam/PetitPotam) - Coerce authentication via EFSRPC.
- [Coercer](https://github.com/p0dalirius/Coercer) - Automated authentication coercion.
- [DFSCoerce](https://github.com/Wh04m1001/DFSCoerce) - DFS coercion.
- [ShadowCoerce](https://github.com/ShutdownRepo/ShadowCoerce) - Shadow coercion.
- MSEven - MS-EVEN coercion (community PoC).
- [PrinterBug](https://github.com/dirkjanm/krbrelayx) - Spooler coercion.
- [SpoolSample](https://github.com/leechristensen/SpoolSample) - Spooler coercion.
- [SpoolSamplerNET](https://github.com/leftp/SpoolSamplerNET) - .NET spooler coercion.
- [noPac](https://github.com/Ridter/noPac) - CVE-2021-42278/42287.
- [Zerologon](https://github.com/dirkjanm/CVE-2020-1472) - CVE-2020-1472 (historical, still seen in legacy networks).
- [PrintNightmare](https://github.com/cube0x0/CVE-2021-1675) - Historical print spooler abuse.

### Delegation, ACLs and Account Abuse

- [rbcd_permissions](https://github.com/NinjaStyle82/rbcd_permissions) - RBCD permission checks.
- [GMSAPasswordReader](https://github.com/rvazarkar/GMSAPasswordReader) - Read gMSA passwords.
- [NetNTLMtoSilverTicket](https://github.com/NotMedic/NetNTLMtoSilverTicket) - Silver ticket from NetNTLM.
- [Whisker](https://github.com/eladshamir/Whisker) - Shadow credentials.
- [pyWhisker](https://github.com/ShutdownRepo/pyWhisker) - Shadow credentials in Python.
- [BadSuccessor](https://github.com/akamai/BadSuccessor) - dMSA privilege escalation (CVE-2025-53779).
- [SharpSuccessor](https://github.com/logangoins/SharpSuccessor) - C# BadSuccessor implementation.
- [BadSuccessor research](https://www.akamai.com/blog/security-research/abusing-dmsa-for-privilege-escalation-in-active-directory) - Akamai original disclosure.
- [BadSuccessor after the patch](https://specterops.io/blog/2025/10/20/the-near-return-of-the-king-account-takeover-using-the-badsuccessor-technique/) - SpecterOps follow-up and BadTakeover BOF.
- [SharpGPOAbuse](https://github.com/FSecureLABS/SharpGPOAbuse) - GPO abuse.
- [pyGPOAbuse](https://github.com/Hackndo/pyGPOAbuse) - GPO abuse in Python.
- [Group3r](https://github.com/Group3r/Group3r) - GPO misconfiguration analysis.
- [Grouper2](https://github.com/l0ss/Grouper2) - GPO password and setting mining.
- [ADACLScanner](https://github.com/canix1/ADACLScanner) - ACL analysis.
- [BloodyAD](https://github.com/CravateRouge/bloodyAD) - AD privilege escalation framework.
- [ldeep](https://github.com/franc-pentest/ldeep) - LDAP enumeration and dumping.

### Domain and Forest Compromise

- [Impacket](https://github.com/fortra/impacket) - Python protocol toolkit: secretsdump, smbexec, wmiexec, psexec, ntlmrelayx, ticketer, getTGT and more.
- [secretsdump.py](https://github.com/fortra/impacket) - DCSync and remote SAM/LSA/NTDS extraction.
- [Mimikatz DCSync](https://github.com/gentilkiwi/mimikatz) - DCSync.
- [Golden Ticket](https://www.ired.team/offensive-security-experiments/active-directory-kerberos-abuse/kerberos-golden-tickets) - krbtgt forgery.
- Diamond Ticket - Modify legitimate TGTs (see TrustedSec research).
- Sapphire Ticket - TGT forgery research (see Charlie Clark and community writeups).
- [Golden SAML](https://www.cyberark.com/resources/threat-research-blog/golden-saml-newly-discovered-attack-technique-offers-attackers-every-enterprise-as-a-target) - Federation token forgery.
- [ADFSDump](https://github.com/mandiant/ADFSDump) - AD FS configuration and secrets.
- [raiseChild.py](https://github.com/fortra/impacket) - Child-to-parent domain escalation.
- [Certipy](https://github.com/ly4k/Certipy) - Golden certificate and ADCS abuse.
- [PassTheCert](https://github.com/AlmondOffSec/PassTheCert) - LDAP/S channel authentication with certificates.

### ADCS (ESC1-ESC15)

- **ESC1** - Enrollee supplies subject and SAN; client authentication EKU.
- **ESC2** - Any Purpose EKU or no EKU.
- **ESC3** - Enrollment agent abuse.
- **ESC4** - Write access to a template.
- **ESC5** - Write access to CA-related AD objects.
- **ESC6** - `EDITF_ATTRIBUTESUBJECTALTNAME2` enabled.
- **ESC7** - CA officer rights abuse.
- **ESC8** - NTLM relay to ADCS HTTP enrollment endpoints.
- **ESC9** - No security extension / UPN mapping abuse.
- **ESC10** - Weak certificate mapping.
- **ESC11** - NTLM relay to ICPR.
- **ESC12** - Shell access to CA.
- **ESC13** - Issuance policy OID linked to a group.
- **ESC14** - Explicit certificate mapping abuse.
- **ESC15** - EKUwu / schema v1 template abuse.
- Tooling: [Certipy](https://github.com/ly4k/Certipy), [Certify](https://github.com/GhostPack/Certify), [Locksmith](https://github.com/TrimarcJake/Locksmith), [PSPKIAudit](https://github.com/GhostPack/PSPKIAudit), [PassTheCert](https://github.com/AlmondOffSec/PassTheCert).

---

## 11. Entra ID, Microsoft 365 and Hybrid Identity

- [ROADtools](https://github.com/dirkjanm/ROADtools) - Entra ID recon and token analysis.
- [AADInternals](https://github.com/Gerenios/AADInternals) - Deep Entra ID and AD FS abuse.
- [AzureHound](https://github.com/SpecterOps/AzureHound) - BloodHound collector for Entra ID.
- [BloodHound CE](https://github.com/SpecterOps/BloodHound) - Azure/Entra attack paths.
- [MicroBurst](https://github.com/NetSPI/MicroBurst) - Azure offensive PowerShell.
- [PowerZure](https://github.com/hausec/PowerZure) - Azure exploitation and assessment.
- [Stormspotter](https://github.com/Azure/Stormspotter) - Azure resource graph.
- [GraphRunner](https://github.com/dafthack/GraphRunner) - Microsoft Graph post-exploitation.
- [TokenTactics](https://github.com/rvrsh3ll/TokenTactics) - Token abuse.
- [TokenTacticsV2](https://github.com/f-bader/TokenTacticsV2) - Updated token abuse.
- [TeamFiltration](https://github.com/Flangvik/TeamFiltration) - Teams/O365 enumeration and exfiltration.
- [MFASweep](https://github.com/dafthack/MFASweep) - MFA coverage checks.
- [o365spray](https://github.com/0xZDH/o365spray) - User enumeration and spraying.
- [MSOLSpray](https://github.com/dafthack/MSOLSpray) - Microsoft Online spraying.
- [TeamsPhisher](https://github.com/Octoberfest7/TeamsPhisher) - Teams external phishing.
- [Evilginx3](https://github.com/kgretzky/evilginx2) - AiTM phishing and token theft.
- [Muraena](https://github.com/muraenateam/muraena) - AiTM session hijacking.
- [NecroBrowser](https://github.com/muraenateam/necrobrowser) - Session cookie theft automation.
- AADAPT - Azure AD attack paths.
- [Monkey365](https://github.com/silverhack/monkey365) - Microsoft 365 and Azure scanner.
- [ScubaGear](https://github.com/cisagov/ScubaGear) - M365 configuration assessment.
- [ScoutSuite](https://github.com/nccgroup/ScoutSuite) - Multi-cloud audit.
- [Prowler](https://github.com/prowler-cloud/prowler) - Cloud security assessment.
- [Graph API permissions reference](https://learn.microsoft.com/en-us/graph/permissions-reference) - Permission mapping.

### Hybrid Identity Attack Paths

- Password hash sync and seamless SSO abuse.
- AD FS token signing key theft (Golden SAML).
- Entra Connect service account privilege.
- On-premises AD to Entra ID privilege mapping.
- Conditional Access gaps and legacy authentication.
- Guest account and B2B trust abuse.
- Service principal and app registration credential abuse.
- Managed identity assignment abuse.
- Privileged Identity Management (PIM) activation gaps.
- Break-glass account discovery.
- Primary Refresh Token (PRT) theft and reuse.
- Device code flow phishing.
- OAuth illicit consent grant.
- Token protection gaps and session cookie replay.

---

## 12. Lateral Movement

- [Impacket](https://github.com/fortra/impacket) - SMB, WMI, DCOM, Kerberos and RPC.
- [NetExec](https://github.com/Pennyw0rth/NetExec) - Modern CrackMapExec successor.
- [CrackMapExec](https://github.com/byt3bl33d3r/CrackMapExec) - Original swiss army knife (legacy).
- [SharpMapExec](https://github.com/cube0x0/SharpMapExec) - C# lateral movement.
- [evil-winrm](https://github.com/Hackplayers/evil-winrm) - WinRM shell.
- [WSMan-WinRM](https://github.com/bohops/WSMan-WinRM) - WinRM tradecraft.
- [WMIcmd](https://github.com/nccgroup/WMIcmd) - WMI execution.
- [WMIHACKER](https://github.com/360-Linton-Lab/WMIHACKER) - WMI lateral movement.
- [SharpWMI](https://github.com/GhostPack/SharpWMI) - WMI execution.
- [CSExec](https://github.com/malcomvetter/CSExec) - Service creation.
- [SharpMove](https://github.com/0xthirteen/SharpMove) - Multiple movement techniques.
- [MoveKit](https://github.com/0xthirteen/MoveKit) - BOF movement toolkit.
- [SharpRDP](https://github.com/0xthirteen/SharpRDP) - RDP command execution.
- [SharpRDPHijack](https://github.com/bohops/SharpRDPHijack) - RDP session hijacking.
- [SCShell](https://github.com/Mr-Un1k0d3r/SCShell) - Service control manager execution.
- [SharpCOM](https://github.com/rvrsh3ll/SharpCOM) - COM execution.
- [PsExec](https://learn.microsoft.com/en-us/sysinternals/downloads/psexec) - Sysinternals execution (detectable).
- [smbexec.py](https://github.com/fortra/impacket) - SMB execution.
- [wmiexec.py](https://github.com/fortra/impacket) - WMI execution.
- [atexec.py](https://github.com/fortra/impacket) - Scheduled task execution.
- [dcomexec.py](https://github.com/fortra/impacket) - DCOM execution.
- [Portia](https://github.com/SpiderLabs/portia) - Lateral movement.
- [DeathStar](https://github.com/byt3bl33d3r/DeathStar) - Automated AD takeover.
- [Vegile](https://github.com/Screetsec/Vegile) - Post-exploitation and persistence.
- [icebreaker](https://github.com/DanMcInerney/icebreaker) - Internal network takeover.
- apt2 - Automated penetration toolkit (archived).
- [nextnet](https://github.com/hdm/nextnet) - Pivot discovery.
- [IOXIDResolver](https://github.com/mubix/IOXIDResolver) - Network interface discovery via IOXIDResolver.
- [krbrelayx](https://github.com/dirkjanm/krbrelayx) - Kerberos relay and unconstrained delegation abuse.
- [rpc2socks](https://github.com/lexfo/rpc2socks) - SOCKS over RPC.
- [sshiva](https://github.com/checkymander/sshiva) - SSH agent hijacking.
- hunter - Session hunting (archived).
- [MiscTools](https://github.com/rasta-mouse/MiscTools) - C# tradecraft.
- [CursedChrome](https://github.com/mandatoryprogrammer/CursedChrome) - Browser-based lateral movement.
- [WireTap](https://github.com/djhohnstein/WireTap) - Teams conversation extraction.
- [Lockless](https://github.com/GhostPack/Lockless) - Browser and app data access without locks.
- [SharpDoor](https://github.com/infosecn1nja/SharpDoor) - RDP restrictions bypass.
- [SharpShares](https://github.com/djhohnstein/SharpShares) - Share enumeration.
- [Snaffler](https://github.com/SnaffCon/Snaffler) - Find interesting files on shares.
- [SauronEye](https://github.com/vivami/SauronEye) - File share hunting.
- [VmdkReader](https://github.com/leftp/VmdkReader) - VMDK disk reading.

---

## 13. Windows Privilege Escalation

### Enumeration and Automation

- [PrivescCheck](https://github.com/itm4n/PrivescCheck) - Comprehensive Windows privilege escalation enumeration.
- [winPEAS](https://github.com/carlospolop/PEASS-ng) - Powerful privilege escalation check with clear output.
- [Seatbelt](https://github.com/GhostPack/Seatbelt) - Host situational awareness.
- [SharpUp](https://github.com/GhostPack/SharpUp) - Privilege escalation checks.
- [WINspect](https://github.com/A-mIn3/WINspect) - PowerShell host inspection.
- [JAWS](https://github.com/411Hall/JAWS) - Just Another Windows Enum Script.
- [Watson](https://github.com/rasta-mouse/Watson) - Missing patch and privilege escalation checks.
- [wesng](https://github.com/bitsadmin/wesng) - Windows Exploit Suggester Next Generation.
- [BeRoot](https://github.com/AlessandroZ/BeRoot) - Privilege escalation checks.
- [Sherlock](https://github.com/rasta-mouse/Sherlock) - Missing patch checks.
- [HostRecon](https://github.com/dafthack/HostRecon) - Host reconnaissance.
- [ADAPE-Script](https://github.com/hausec/ADAPE-Script) - AD assessment.
- [PowerUp](https://github.com/PowerShellMafia/PowerSploit) - Classic privilege escalation checks.
- [WinPwn](https://github.com/S3cur3Th1sSh1t/WinPwn) - Recon and escalation automation.

### Exploits and Abuse

- [UACME](https://github.com/hfiref0x/UACME) - UAC bypass collection.
- [WinPwnage](https://github.com/rootm0s/WinPwnage) - UAC bypass and privilege escalation.
- [WindowsExploits](https://github.com/abatchy17/WindowsExploits) - Compiled local exploits.
- [WindowsExploits/Exploits](https://github.com/WindowsExploits/Exploits) - Exploit collection.
- [SecWiki Windows kernel exploits](https://github.com/SecWiki/windows-kernel-exploits) - Kernel exploit archive.
- [Tokenvator](https://github.com/0xbadjuju/Tokenvator) - Token manipulation.
- [Robber](https://github.com/MojtabaTajik/Robber) - Token privilege abuse.
- [Juicy Potato](https://github.com/ohpe/juicy-potato) - COM token impersonation (legacy).
- [RoguePotato](https://github.com/antonioCoco/RoguePotato) - Service account to SYSTEM.
- [RogueWinRM](https://github.com/antonioCoco/RogueWinRM) - Service account to SYSTEM.
- [PrintSpoofer](https://github.com/itm4n/PrintSpoofer) - Impersonation privilege abuse.
- [BadPotato](https://github.com/BeichenDream/BadPotato) - C# PrintSpoofer.
- [Lovely-Potato](https://github.com/TsukiCTF/Lovely-Potato) - Automated potato exploitation.
- [FullPowers](https://github.com/itm4n/FullPowers) - Recover service account privileges.
- [UsoDllLoader](https://github.com/itm4n/UsoDllLoader) - Load DLLs from System32.
- [Priv2Admin](https://github.com/gtworek/Priv2Admin) - Abuse Windows privileges.
- [siofra](https://github.com/Cybereason/siofra) - DLL hijack scanner.
- [rattler](https://github.com/sensepost/rattler) - DLL preloading scanner.
- [Windows Privilege Escalation Guide](https://www.absolomb.com/2018-01-26-Windows-Privilege-Escalation-Guide/) - Methodology.
- [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings) - Practical Windows PrivEsc checklist.

### Privilege Abuse Cheatsheet

- **SeImpersonate / SeAssignPrimaryToken** - Potato family (RoguePotato, PrintSpoofer, GodPotato, SweetPotato).
- **SeBackup / SeRestore** - Read protected files, dump SAM/SYSTEM, registry hives.
- **SeTakeOwnership** - Take ownership of files and registry keys.
- **SeDebug** - Access other processes, including LSASS.
- **SeLoadDriver** - Load vulnerable drivers (BYOVD).
- **SeTcb** - Act as part of the operating system.
- **SeCreateToken** - Create arbitrary tokens.
- **AlwaysInstallElevated** - MSI execution as SYSTEM.
- **Unquoted service paths** - Path interception.
- **Weak service permissions** - Service binary replacement or config change.
- **DLL hijacking and sideloading** - Search-order and phantom DLLs.
- **Scheduled task abuse** - Writable task binaries or task creation rights.
- **COM hijacking** - HKCU CLSID and TreatAs.
- **Registry autoruns** - Writable autorun keys.

---

## 14. Linux Privilege Escalation

- [linPEAS](https://github.com/carlospolop/PEASS-ng) - Comprehensive Linux enumeration.
- [linPEAS (legacy path)](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS) - Original repository path.
- [winPEAS (legacy path)](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/winPEAS) - Original repository path.
- [linux-exploit-suggester](https://github.com/mzet-/linux-exploit-suggester) - Kernel exploit suggestions.
- [linux-exploit-suggester-2](https://github.com/jondonas/linux-exploit-suggester-2) - Kernel exploit suggestions.
- [LinEnum](https://github.com/rebootuser/LinEnum) - Enumeration script.
- [linux-smart-enumeration](https://github.com/diego-treitos/linux-smart-enumeration) - Progressive enumeration.
- [Lynis](https://github.com/CISOfy/lynis) - Security auditing.
- [BeRoot](https://github.com/AlessandroZ/BeRoot) - Privilege escalation checks.
- [Vuls](https://github.com/future-architect/vuls) - Vulnerability scanning.
- [AutoLocalPrivilegeEscalation](https://github.com/ngalongc/AutoLocalPrivilegeEscalation) - Automation.
- [yodo](https://github.com/b3rito/yodo) - Privilege escalation tool.
- [linux-soft-exploit-suggester](https://github.com/belane/linux-soft-exploit-suggester) - Vulnerable software lookup.
- [swap_digger](https://github.com/sevagas/swap_digger) - Swap file analysis.
- [RootHelper](https://github.com/NullArray/RootHelper) - Post-exploitation helper.
- [MIDA-Multitool](https://github.com/NullArray/MIDA-Multitool) - Recon and exploitation.
- [dirty_sock](https://github.com/initstring/dirty_sock) - Snapd privilege escalation.
- [KeyTabExtract](https://github.com/sosdave/KeyTabExtract) - Keytab analysis.
- [pspy](https://github.com/DominicBreuker/pspy) - Process monitoring without root.
- [modDetective](https://github.com/itsKindred/modDetective) - Kernel module analysis.
- [sudo_inject](https://github.com/nongiach/sudo_inject) - Sudo token injection.
- [SUID3NUM](https://github.com/Anon-Exploiter/SUID3NUM) - SUID binary triage.
- [GTFOBLookup](https://github.com/nccgroup/GTFOBLookup) - Offline GTFOBins.
- [SUDO_KILLER](https://github.com/TH3xACE/SUDO_KILLER) - Sudo misconfiguration exploitation.
- [linuxprivchecker](https://raw.githubusercontent.com/sleventyeleven/linuxprivchecker/master/linuxprivchecker.py) - Classic checker.
- [unix-privesc-check](https://github.com/inquisb/unix-privesc-check) - Unix privilege escalation checks.
- [tas](https://github.com/hc0d3r/tas) - TTY manipulation and fake binaries.
- [SecWiki Linux kernel exploits](https://github.com/SecWiki/linux-kernel-exploits) - Kernel exploit archive.
- [uptux](https://github.com/initstring/uptux) - Linux privilege escalation checks.
- [static-binaries](https://github.com/andrew-d/static-binaries) - Portable binaries for compromised hosts.
- [GTFOBins](https://gtfobins.github.io/) - Unix binary abuse.
- [Linux Privilege Escalation checklist](https://github.com/Ignitetechnologies/Linux-Privilege-Escalation) - Practical checklist.
- [Linux Capabilities](https://man7.org/linux/man-pages/man7/capabilities.7.html) - cap_setuid, cap_sys_admin and friends.
- [Container escape to host](https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/docker-security/docker-breakout-privilege-escalation/index.html) - Namespace, cgroup and mount abuse.

---

## 15. macOS and Apple Tradecraft

- [EvilOSX](https://github.com/Marten4n6/EvilOSX) - macOS RAT.
- [EggShell](https://github.com/neoneggplant/EggShell) - macOS/Linux surveillance.
- [Mythic Poseidon](https://github.com/MythicAgents/poseidon) - Go agent for macOS.
- [Sliver](https://github.com/BishopFox/sliver) - macOS implants.
- [MacHound](https://github.com/XMCyber/MacHound) - BloodHound collector for macOS.
- [TCC abuse](https://book.hacktricks.wiki/en/macos-hardening/macos-security-and-privilege-escalation/macos-security-protections/macos-tcc/index.html) - Transparency, Consent and Control bypass research.
- [LaunchAgents and LaunchDaemons](https://developer.apple.com/library/archive/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/Introduction.html) - Persistence.
- [Login Items](https://support.apple.com/guide/mac-help/mh15189/mac) - Persistence.
- [Keychain dumping](https://ss64.com/mac/security.html) - security command and chainbreaker.
- [chainbreaker](https://github.com/n0fate/chainbreaker) - Keychain forensic extraction.
- [osascript](https://developer.apple.com/library/archive/documentation/AppleScript/Conceptual/AppleScriptLangGuide/introduction/ASLR_intro.html) - Script execution and phishing.
- [JXA](https://developer.apple.com/library/archive/documentation/LanguagesUtilities/Conceptual/MacAutomationScriptingGuide/) - JavaScript for Automation.
- [pkgutil and installer](https://ss64.com/mac/pkgutil.html) - Package execution.
- [codesign](https://ss64.com/mac/codesign.html) - Signing and verification.
- [Gatekeeper bypass research](https://book.hacktricks.wiki/en/macos-hardening/macos-security-and-privilege-escalation/macos-security-protections/macos-gatekeeper/index.html) - Quarantine and notarization abuse.
- [TCC databases](https://book.hacktricks.wiki/en/macos-hardening/macos-security-and-privilege-escalation/macos-security-protections/macos-tcc/index.html) - Full Disk Access and screen recording grants.
- [macOS post-exploitation](https://book.hacktricks.wiki/en/macos-hardening/index.html) - Enumeration and persistence techniques.
- [macOS Security Compliance Project](https://github.com/usnistgov/macos_security) - Baseline and hardening.

---

## 16. Pivoting and Tunneling

- [Chisel](https://github.com/jpillora/chisel) - TCP/UDP tunnel over HTTP.
- [SharpChisel](https://github.com/shantanu561993/SharpChisel) - C# Chisel client.
- [Ligolo-ng](https://github.com/nicocha30/ligolo-ng) - TUN-based pivoting.
- [Ligolo (original)](https://github.com/sysdream/ligolo) - Original Ligolo.
- [pingtunnel](https://github.com/esrrhs/pingtunnel) - ICMP tunneling.
- [VPNPivot](https://github.com/0x36/VPNPivot) - VPN pivoting.
- [SSF (Secure Socket Funneling)](https://github.com/securesocketfunneling/ssf) - Multi-protocol tunneling.
- [Invoke-SocksProxy](https://github.com/p3nt4/Invoke-SocksProxy) - PowerShell SOCKS proxy.
- [reGeorg](https://github.com/sensepost/reGeorg) - HTTP tunnel through web shells.
- [reGeorg-Weblogic](https://github.com/hayasec/reGeorg-Weblogic) - WebLogic variant.
- [ABPTTS](https://github.com/nccgroup/ABPTTS) - HTTP tunnel through ASP.NET.
- [PivotSuite](https://github.com/RedTeamOperations/PivotSuite) - Network pivoting.
- [egressbuster](https://github.com/trustedsec/egressbuster) - Egress testing.
- [bypass-firewalls-by-DNS-history](https://github.com/vincentcox/bypass-firewalls-by-DNS-history) - Origin discovery.
- [SocksOverRDP](https://github.com/nccgroup/SocksOverRDP) - SOCKS over RDP.
- [mssqlproxy](https://github.com/blackarrowsec/mssqlproxy) - MSSQL pivoting.
- [rpc2socks](https://github.com/lexfo/rpc2socks) - SOCKS over RPC.
- [socat](https://linux.die.net/man/1/socat) - Relay and tunnel.
- [sshuttle](https://github.com/sshuttle/sshuttle) - VPN-like SSH tunneling.
- [proxychains-ng](https://github.com/rofl0r/proxychains-ng) - Force TCP through proxies.
- [gost](https://github.com/ginuerzh/gost) - Multi-protocol proxy.
- [frp](https://github.com/fatedier/frp) - Fast reverse proxy.
- [Cloudflared](https://github.com/cloudflare/cloudflared) - Cloudflare tunnels.
- [WireGuard](https://www.wireguard.com/) - Modern VPN tunnel.
- [OpenVPN](https://openvpn.net/) - Classic VPN.
- [Tunna](https://github.com/SECFORCE/Tunna) - TCP over HTTP.
- [HTran](https://github.com/HiwinCN/HTran) - Connection bouncer.

---

## 17. Persistence

### Windows Persistence

- [SharPersist](https://github.com/fireeye/SharPersist) - Modular persistence toolkit.
- [SharpHide](https://github.com/outflanknl/SharpHide) - Hidden scheduled tasks.
- [DAMP](https://github.com/HarmJ0y/DAMP) - Discretionary ACL modification persistence.
- [Empire](https://github.com/BC-SECURITY/Empire) - Persistence modules.
- [Scheduled tasks](https://learn.microsoft.com/en-us/windows/win32/taskschd/task-scheduler-start-page) - Native persistence.
- [Windows services](https://learn.microsoft.com/en-us/windows/win32/services/services) - Service persistence.
- [WMI event subscriptions](https://learn.microsoft.com/en-us/windows/win32/wmisdk/receiving-events-at-all-times) - Fileless persistence.
- [COM hijacking](https://www.ired.team/offensive-security/persistence/t1122-com-hijacking) - CLSID and TreatAs abuse.
- [DLL search order hijacking](https://attack.mitre.org/techniques/T1574/001/) - Sideloading.
- [AppInit DLLs](https://learn.microsoft.com/en-us/windows/win32/dlls/secure-boot-and-appinit-dlls) - Legacy persistence.
- [Image File Execution Options](https://attack.mitre.org/techniques/T1546/012/) - Debugger persistence.
- [Accessibility features](https://attack.mitre.org/techniques/T1546/008/) - Sticky keys, utilman and magnifier.
- [Sticky-Keys-Slayer](https://github.com/linuz/Sticky-Keys-Slayer) - Backdoor detection.
- [sticky_keys_hunter](https://github.com/ztgrace/sticky_keys_hunter) - Detection.
- [Logon scripts](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn581922%28v=ws.11%29) - GPO persistence.
- [Run keys](https://learn.microsoft.com/en-us/windows/win32/setupapi/run-and-runonce-registry-keys) - Registry persistence.
- [Winlogon](https://attack.mitre.org/techniques/T1547/004/) - Shell and userinit.
- [Print monitors](https://attack.mitre.org/techniques/T1547/010/) - Print subsystem persistence.
- [Port monitors](https://learn.microsoft.com/en-us/windows-hardware/drivers/print/port-monitors) - Print persistence.
- [Time providers](https://attack.mitre.org/techniques/T1547/003/) - DLL persistence.
- [BITS jobs](https://attack.mitre.org/techniques/T1197/) - Transfer persistence.
- [CLR profiling](https://attack.mitre.org/techniques/T1574/) - .NET persistence.
- [AppDomainManager](https://learn.microsoft.com/en-us/dotnet/framework/app-domains/application-domains) - .NET injection.
- [WinSxS](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/configure-a-windows-repair-source) - Component store abuse.

### Linux and macOS Persistence

- [cron](https://man7.org/linux/man-pages/man5/crontab.5.html) - Scheduled tasks.
- [systemd](https://www.freedesktop.org/software/systemd/man/systemd.service.html) - Services and timers.
- rc.local - Boot scripts (traditional init systems).
- [SSH authorized_keys](https://www.ssh.com/academy/ssh/authorized-keys-file) - Key persistence.
- [PAM backdoor](https://attack.mitre.org/techniques/T1556/004/) - Authentication module abuse.
- [LD_PRELOAD](https://man7.org/linux/man-pages/man8/ld.so.8.html) - Library injection.
- [Bash startup files](https://www.gnu.org/software/bash/manual/html_node/Bash-Startup-Files.html) - Shell persistence.
- [udev rules](https://www.freedesktop.org/software/systemd/man/udev.html) - Device-trigger persistence.
- [eBPF](https://ebpf.io/) - Kernel persistence research.
- [macOS LaunchAgents/Daemons](https://developer.apple.com/library/archive/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/Introduction.html) - Apple persistence.
- [macOS login items](https://support.apple.com/guide/mac-help/mh15189/mac) - User persistence.
- [macOS configuration profiles](https://support.apple.com/guide/mac-help/mh35561/mac) - MDM persistence.
- [macOS dylib hijacking](https://book.hacktricks.wiki/en/macos-hardening/index.html) - Dynamic library hijack.

---

## 18. Cloud Red Team Operations

### Multi-Cloud Methodology

1. **Credential acquisition** - IMDS, SSRF, CI/CD secrets, source code, phishing, SaaS tokens.
2. **Identity enumeration** - Who am I, what can I do, which roles can I assume, which resources can I reach.
3. **Attack-path analysis** - IAM graph, trust relationships, cross-account and cross-tenant paths.
4. **Privilege escalation** - Policy attachment, role chaining, service-specific privesc.
5. **Persistence** - New credentials, backdoor roles, federation, OAuth apps, Lambda/Function triggers.
6. **Collection and exfiltration** - Storage, databases, secrets, logs, snapshots.
7. **Impact** - Data access, resource control, billing abuse, supply chain.

### Multi-Cloud Tooling

- [ScoutSuite](https://github.com/nccgroup/ScoutSuite) - Multi-cloud security auditing.
- [Prowler](https://github.com/prowler-cloud/prowler) - AWS, Azure, GCP and Kubernetes assessment.
- [CloudFox](https://github.com/BishopFox/cloudfox) - Situational awareness for AWS, Azure and GCP.
- [Cartography](https://github.com/lyft/cartography) - Asset and relationship graph.
- [Steampipe](https://github.com/turbot/steampipe) - Cloud APIs as SQL.
- [Cloudlist](https://github.com/projectdiscovery/cloudlist) - Multi-cloud asset listing.
- [TruffleHog](https://github.com/trufflesecurity/trufflehog) - Secret discovery.
- [Gitleaks](https://github.com/gitleaks/gitleaks) - Secret detection.
- [Cloud_enum](https://github.com/initstring/cloud_enum) - Public cloud asset enumeration.
- [Stratus Red Team](https://github.com/DataDog/stratus-red-team) - Cloud attack emulation.
- [CloudGoat](https://github.com/RhinoSecurityLabs/cloudgoat) - Vulnerable AWS environments for practice.
- [IAM Vulnerable](https://github.com/BishopFox/iam-vulnerable) - Practice IAM privilege escalation.
- [Kubernetes Goat](https://github.com/madhuakula/kubernetes-goat) - Vulnerable Kubernetes cluster.

### AWS

- [Pacu](https://github.com/RhinoSecurityLabs/pacu) - AWS exploitation framework.
- [CloudFox](https://github.com/BishopFox/cloudfox) - AWS situational awareness.
- [PMapper](https://github.com/nccgroup/PMapper) - IAM privilege escalation graph.
- [Cloudsplaining](https://github.com/salesforce/cloudsplaining) - IAM policy risk analysis.
- [enumerate-iam](https://github.com/andresriancho/enumerate-iam) - Permission enumeration.
- [ScoutSuite](https://github.com/nccgroup/ScoutSuite) - Multi-cloud audit.
- [Prowler](https://github.com/prowler-cloud/prowler) - Security assessment.
- [aws_pwn](https://github.com/dagrz/aws_pwn) - AWS exploitation scripts.
- [Endgame](https://github.com/DavidDikker/endgame) - Resource policy exploitation.
- [weirdAAL](https://github.com/carnal0wnage/weirdAAL) - AWS attack library.
- [S3Scanner](https://github.com/sa7mon/S3Scanner) - Open bucket discovery.
- [cloud_enum](https://github.com/initstring/cloud_enum) - Multi-cloud asset enumeration.
- [AWS IAM Privilege Escalation](https://github.com/RhinoSecurityLabs/AWS-IAM-Privilege-Escalation) - Techniques.
- [IAM Vulnerable](https://github.com/BishopFox/iam-vulnerable) - Practice environment.
- [awspx](https://github.com/FSecureLABS/awspx) - IAM graph visualization.
- [CloudMapper](https://github.com/duo-labs/cloudmapper) - AWS visualization.
- [Cloud Custodian](https://github.com/cloud-custodian/cloud-custodian) - Policy engine (defense awareness).
- [IMDS documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-service.html) - IMDSv1 vs IMDSv2.
- [Stratus Red Team](https://github.com/DataDog/stratus-red-team) - AWS/Azure/GCP attack emulation.
- [CloudGoat](https://github.com/RhinoSecurityLabs/cloudgoat) - Practice range.

**Common AWS attack paths:** over-permissive IAM roles, `iam:PassRole` plus `lambda:CreateFunction`, `sts:AssumeRole` chains, SSRF to IMDSv1, public S3 buckets, exposed EBS/RDS snapshots, Secrets Manager and SSM parameters, CodeBuild/CodePipeline secrets, ECS task role theft, EKS service account tokens, cross-account role trusts, CloudTrail gaps, and Lambda environment variables.

### Azure and Entra ID

- [ROADtools](https://github.com/dirkjanm/ROADtools) - Entra ID enumeration.
- [AADInternals](https://github.com/Gerenios/AADInternals) - Deep Entra ID abuse.
- [AzureHound](https://github.com/SpecterOps/AzureHound) - BloodHound collector.
- [MicroBurst](https://github.com/NetSPI/MicroBurst) - Azure offensive toolkit.
- [PowerZure](https://github.com/hausec/PowerZure) - Azure exploitation.
- [Stormspotter](https://github.com/Azure/Stormspotter) - Azure resource graph.
- [GraphRunner](https://github.com/dafthack/GraphRunner) - Microsoft Graph post-exploitation.
- [TokenTactics](https://github.com/rvrsh3ll/TokenTactics) - Token abuse.
- [TeamFiltration](https://github.com/Flangvik/TeamFiltration) - Teams/O365 attacks.
- [MFASweep](https://github.com/dafthack/MFASweep) - MFA checks.
- [AzureHound](https://github.com/SpecterOps/AzureHound) - Collector.
- [Monkey365](https://github.com/silverhack/monkey365) - Microsoft 365 and Azure scanner.
- [ScubaGear](https://github.com/cisagov/ScubaGear) - M365 baseline assessment.
- [ScoutSuite](https://github.com/nccgroup/ScoutSuite) - Azure audit.
- [Prowler](https://github.com/prowler-cloud/prowler) - Azure assessment.
- [Azure IMDS](https://learn.microsoft.com/en-us/azure/virtual-machines/instance-metadata-service) - Managed identity token access.
- [AzureHound docs](https://bloodhound.readthedocs.io/) - Collector usage.

**Common Azure attack paths:** managed identity tokens via IMDS, over-permissive role assignments, service principal secrets and certificates, app registration ownership, OAuth consent, PIM activation gaps, Azure Automation and Runbook credentials, Key Vault access policies, Storage account SAS tokens, Azure Functions and App Service identity, Entra Connect (ADSync) privilege, and cross-tenant B2B/guest abuse.

### Google Cloud Platform

- [gcp_enum](https://github.com/hakaioffsec/gcp_enum) - GCP enumeration.
- [gcp_scanner](https://github.com/google/gcp_scanner) - Google-published scanner.
- [GCPBucketBrute](https://github.com/RhinoSecurityLabs/GCPBucketBrute) - GCS bucket enumeration.
- [hayat](https://github.com/DenizParlak/hayat) - GCP auditing.
- [GCP IAM Privilege Escalation](https://github.com/RhinoSecurityLabs/GCP-IAM-Privilege-Escalation) - Privesc techniques.
- GCPHound - Community BloodHound OpenGraph collector for GCP (early-stage).
- [ScoutSuite](https://github.com/nccgroup/ScoutSuite) - GCP audit.
- [Prowler](https://github.com/prowler-cloud/prowler) - GCP assessment.
- [CloudFox](https://github.com/BishopFox/cloudfox) - GCP situational awareness.

**Common GCP attack paths:** service account key files, default compute service account, `iam.serviceAccounts.actAs`, `iam.serviceAccountKeys.create`, Cloud Functions environment variables, GCS bucket ACLs, metadata server tokens, Cloud Build and Artifact Registry, and org policy gaps.

### SaaS, CI/CD and Supply Chain

- [TruffleHog](https://github.com/trufflesecurity/trufflehog) - Secrets in repos and pipelines.
- [Gitleaks](https://github.com/gitleaks/gitleaks) - Git history secrets.
- [gitrob](https://github.com/michenriksen/gitrob) - GitHub organization reconnaissance.
- [trufflehog](https://github.com/trufflesecurity/trufflehog) - CI/CD secret discovery.
- [Mythic](https://github.com/its-a-feature/Mythic) - C2 for post-compromise operations.
- [OWASP CI/CD Top 10](https://owasp.org/www-project-top-10-ci-cd-security-risks/) - CI/CD attack research and risk baseline.
- [Dependency confusion](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610) - Package namespace takeover research.
- [Typosquatting](https://en.wikipedia.org/wiki/Typosquatting) - Malicious package detection and awareness.
- [Sigstore](https://www.sigstore.dev/) - Supply chain signing (defense awareness).
- [SLSA](https://slsa.dev/) - Supply chain levels (defense awareness).
- [OWASP CI/CD Top 10](https://owasp.org/www-project-top-10-ci-cd-security-risks/) - CI/CD risk baseline.
- [GitHub Actions security](https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions) - Hardening reference.

### Cloud OPSEC Notes

- Cloud audit logs are extremely high fidelity. Assume every API call is logged with identity, source IP, user agent and timestamp.
- Prefer read-only enumeration until the objective requires a write.
- Understand what creates a new credential or persistence object: `CreateAccessKey`, `CreateServicePrincipal`, `AddFederatedCredential`, `CreateFunction`, `CreateRole`, `PutBucketPolicy`, OAuth consent grants and role assignments.
- Watch for Defender for Cloud, GuardDuty, Security Command Center and Entra ID Protection detections.
- Clean up test resources, keys, roles and functions; document everything you create.

---

## 19. Containers and Kubernetes

- [kube-hunter](https://github.com/aquasecurity/kube-hunter) - Kubernetes penetration testing.
- [kube-bench](https://github.com/aquasecurity/kube-bench) - CIS benchmark checks.
- [kubeletctl](https://github.com/cyberark/kubeletctl) - Kubelet API client.
- [peirates](https://github.com/inguardians/peirates) - Kubernetes post-exploitation.
- [Kubescape](https://github.com/kubescape/kubescape) - Kubernetes security posture.
- [Trivy](https://github.com/aquasecurity/trivy) - Container and cluster vulnerability scanning.
- KubeStriker - Community Kubernetes security assessment tool.
- [Bad Pods](https://github.com/BishopFox/badPods) - Pod privilege escalation examples.
- [CDK](https://github.com/cdk-team/CDK) - Container escape toolkit.
- [Deepce](https://github.com/stealthcopter/deepce) - Docker enumeration and escape.
- [amicontained](https://github.com/genuinetools/amicontained) - Container capability discovery.
- [Docker Bench for Security](https://github.com/docker/docker-bench-security) - Docker CIS checks.
- [Falco](https://github.com/falcosecurity/falco) - Runtime detection (defense awareness).
- [Kubernetes Goat](https://github.com/madhuakula/kubernetes-goat) - Practice environment.
- [KubeInvaders](https://github.com/lucky-sideburn/KubeInvaders) - Chaos and security testing.
- [Kubernetes security checklist](https://kubernetes.io/docs/concepts/security/) - Official security concepts.
- [OWASP Kubernetes Top 10](https://owasp.org/www-project-kubernetes-top-ten/) - Risk baseline.

**Common Kubernetes attack paths:** exposed kubelet API, anonymous auth, over-permissive RBAC, service account token mounting, privileged pods, hostPath mounts, hostPID/hostNetwork, missing NetworkPolicies, secrets in environment variables, exposed etcd, vulnerable admission controllers, and image supply chain.

---

## 20. Web Application Pentesting

### Discovery and Content

- [gobuster](https://github.com/OJ/gobuster) - Directory and DNS busting.
- [dirble](https://github.com/nccgroup/dirble) - Fast directory brute forcing.
- [dirsearch](https://github.com/maurosoria/dirsearch) - Web path discovery.
- [feroxbuster](https://github.com/epi052/feroxbuster) - Recursive content discovery.
- [ffuf](https://github.com/ffuf/ffuf) - Fast web fuzzing.
- [wfuzz](https://github.com/xmendez/wfuzz) - Web fuzzer.
- [turbosearch](https://github.com/helviojunior/turbosearch) - Directory discovery.
- [parameth](https://github.com/maK-/parameth) - Parameter brute forcing.
- [ParamSpider](https://github.com/devanshbatham/ParamSpider) - Archive parameter mining.
- [Arjun](https://github.com/s0md3v/Arjun) - Parameter discovery.
- [dirscraper](https://github.com/Cillian-Collins/dirscraper) - Directory lookup from JavaScript.
- [snallygaster](https://github.com/hannob/snallygaster) - Hidden file discovery.
- [Breacher](https://github.com/s0md3v/Breacher) - Admin panel finder.
- [server-status_PWN](https://github.com/mazen160/server-status_PWN) - Apache server-status exploitation.
- [CMSeeK](https://github.com/Tuhinshubhra/CMSeeK) - CMS detection and exploitation.
- [WhatWaf](https://github.com/Ekultek/WhatWaf) - WAF detection and bypass.
- [nuclei](https://github.com/projectdiscovery/nuclei) - Template-based web scanning.
- [Nikto](https://github.com/sullo/nikto) - Web server scanner.
- [Wapiti](https://github.com/wapiti-scanner/wapiti) - Web application scanner.
- [ZAP](https://www.zaproxy.org/) - Zed Attack Proxy.
- [Burp Suite](https://portswigger.net/burp) - Commercial web testing platform.
- [Caido](https://caido.io/) - Modern lightweight web security toolkit.
- [mitmproxy](https://mitmproxy.org/) - Intercepting proxy.
- [WAScan](https://github.com/m4ll0k/WAScan) - All-in-one scanner.
- [GyoiThon](https://github.com/gyoisamurai/GyoiThon) - CMS and vulnerability scanner.
- [XSStrike](https://github.com/s0md3v/XSStrike) - XSS discovery.
- [dalfox](https://github.com/hahwul/dalfox) - XSS scanner.
- [sqlmap](https://github.com/sqlmapproject/sqlmap) - SQL injection.
- [NoSQLMap](https://github.com/codingo/NoSQLMap) - NoSQL injection.
- [Commix](https://github.com/commixproject/commix) - Command injection.
- [SSRFmap](https://github.com/swisskyrepo/SSRFmap) - SSRF exploitation.
- [SSRF-Testing](https://github.com/cujanovic/SSRF-Testing) - SSRF tutorials and payloads.
- [Gopherus](https://github.com/tarunkant/Gopherus) - Gopher SSRF payloads.
- [jwt_tool](https://github.com/ticarpi/jwt_tool) - JWT testing.
- [HackBar](https://github.com/d3vilbug/HackBar) - Burp extension.
- [awesome-burp-extensions](https://github.com/snoopysecurity/awesome-burp-extensions) - Burp extension list.
- [BurpSuite_403Bypasser](https://github.com/sting8k/BurpSuite_403Bypasser) - 403 bypass.
- [Autorize](https://github.com/Quitten/Autorize) - Authorization testing.
- [Turbo Intruder](https://github.com/PortSwigger/turbo-intruder) - High-speed request engine.
- [GadgetProbe](https://github.com/BishopFox/GadgetProbe) - Java deserialization gadget probing.
- [Java-Deserialization-Scanner](https://github.com/federicodotta/Java-Deserialization-Scanner) - Deserialization scanner.
- [ysoserial](https://github.com/frohoff/ysoserial) - Java deserialization payloads.
- [ysoserial.net](https://github.com/pwntester/ysoserial.net) - .NET deserialization payloads.
- [PHPGGC](https://github.com/ambionics/phpggc) - PHP unserialize payload generator.
- [marshalsec](https://github.com/mbechler/marshalsec) - Java unmarshalling research.
- [XXEinjector](https://github.com/enjoiz/XXEinjector) - XXE exploitation.
- [oxml_xxe](https://github.com/BuffaloWill/oxml_xxe) - Office XXE payloads.
- [LFiFreak](https://github.com/OsandaMalith/LFiFreak) - LFI exploitation.
- [tplmap](https://github.com/epinna/tplmap) - SSTI exploitation.
- [xcat](https://github.com/orf/xcat) - XPath injection.
- [fuxploider](https://github.com/almandin/fuxploider) - File upload exploitation.
- [freddy](https://github.com/nccgroup/freddy) - Deserialization detection.
- [IIS-ShortName-Scanner](https://github.com/irsdl/IIS-ShortName-Scanner) - IIS short filename discovery.
- [GitTools](https://github.com/internetwache/GitTools) - Exposed .git exploitation.
- [viewgen](https://github.com/0xacb/viewgen) - .NET ViewState generation.
- [RCEvil.NET](https://github.com/Illuminopi/RCEvil.NET) - .NET ViewState exploitation.
- [angularjs-csti-scanner](https://github.com/tijme/angularjs-csti-scanner) - AngularJS CSTI.
- [webshell collection](https://github.com/tennc/webshell) - Web shells for authorized testing.
- [p0wny-shell](https://github.com/flozz/p0wny-shell) - Single-file PHP shell.
- [WPScan](https://github.com/wpscanteam/wpscan) - WordPress scanner.
- [WPForce](https://github.com/n00py/WPForce) - WordPress attack tool.
- [WPSeku](https://github.com/m4ll0k/WPSeku) - WordPress scanner.
- [Wordpresscan](https://github.com/swisskyrepo/Wordpresscan) - WordPress scanner.
- [wordpress-exploit-framework](https://github.com/rastating/wordpress-exploit-framework) - WordPress exploitation.
- [droopescan](https://github.com/droope/droopescan) - Drupal scanner.
- [joomscan](https://github.com/rezasp/joomscan) - Joomla scanner.
- [Typo-Enumerator](https://github.com/whoot/Typo-Enumerator) - TYPO3 enumeration.
- [domi-owned](https://github.com/coldfusion39/domi-owned) - Lotus Domino exploitation.
- [CMSmap](https://github.com/Dionach/CMSmap) - WordPress, Joomla and Drupal scanner.
- [KingOfBugbountyTips](https://github.com/KingOfBugbounty/KingOfBugBountyTips) - Bug bounty techniques.

### Web Research and Payload References

- [PortSwigger Web Security Academy](https://portswigger.net/web-security) - The best free web security labs.
- [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings) - Payload and bypass reference.
- [HackTricks](https://book.hacktricks.wiki/) - Web, network, cloud and binary techniques.
- [OWASP WSTG](https://owasp.org/www-project-web-security-testing-guide/) - Testing guide.
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/) - Defensive and testing cheatsheets.
- [Awesome Web Security](https://github.com/qazbnm456/awesome-web-security) - Curated web security resources.

---

## 21. API, GraphQL and Mobile

### API Security

- [OWASP API Security Top 10](https://owasp.org/API-Security/editions/2023/en/0x00-header/) - Risk baseline.
- [RESTler](https://github.com/microsoft/restler-fuzzer) - Stateful REST API fuzzing.
- [Astra](https://github.com/flipkart-incubator/Astra) - REST API security testing.
- [Postman](https://www.postman.com/) - API development and testing.
- [Insomnia](https://insomnia.rest/) - API client.
- [Bruno](https://www.usebruno.com/) - Offline API client.
- [Kiterunner](https://github.com/assetnote/kiterunner) - API route discovery.
- [ffuf](https://github.com/ffuf/ffuf) - API fuzzing.
- [Nuclei](https://github.com/projectdiscovery/nuclei) - API vulnerability templates.
- [jwt_tool](https://github.com/ticarpi/jwt_tool) - JWT abuse.
- [APIsec University](https://www.apisecuniversity.com/) - Free API security training.
- [OWASP crAPI](https://github.com/OWASP/crAPI) - Completely Ridiculous API practice target.
- [VAmPI](https://github.com/erev0s/VAmPI) - Vulnerable API.
- [DVGA](https://github.com/dolevf/Damn-Vulnerable-GraphQL-Application) - Vulnerable GraphQL app.

### GraphQL

- [graphw00f](https://github.com/dolevf/graphw00f) - GraphQL fingerprinting.
- [InQL](https://github.com/doyensec/inql) - GraphQL testing.
- [Clairvoyance](https://github.com/nikitastupin/clairvoyance) - Schema recovery.
- [GraphQL Voyager](https://github.com/APIs-guru/graphql-voyager) - Schema visualization.
- [GraphQLmap](https://github.com/swisskyrepo/GraphQLmap) - GraphQL exploitation.
- [batchql](https://github.com/assetnote/batchql) - GraphQL batching attacks.
- [Damn Vulnerable GraphQL](https://github.com/dolevf/Damn-Vulnerable-GraphQL-Application) - Practice.

### Mobile

- [MobSF](https://github.com/MobSF/Mobile-Security-Framework-MobSF) - Mobile security framework.
- [Frida](https://frida.re/) - Dynamic instrumentation.
- [objection](https://github.com/sensepost/objection) - Runtime mobile exploration.
- [apktool](https://github.com/iBotPeaches/Apktool) - APK reverse engineering.
- [jadx](https://github.com/skylot/jadx) - Dex to Java decompiler.
- [dex2jar](https://github.com/pxb1988/dex2jar) - Dex conversion.
- [Ghidra](https://github.com/NationalSecurityAgency/ghidra) - NSA reverse engineering suite.
- [Hopper](https://www.hopperapp.com/) - macOS and iOS disassembler.
- [class-dump](https://github.com/nygard/class-dump) - Objective-C class extraction.
- [iOS Security Research](https://book.hacktricks.wiki/en/mobile-pentesting/ios-pentesting/index.html) - Checkra1n, palera1n, Frida and objection workflows.
- [Android Pentesting](https://book.hacktricks.wiki/en/mobile-pentesting/android-app-pentesting/index.html) - ADB, rooted devices, Magisk and Frida.
- [OWASP MASVS](https://mas.owasp.org/MASVS/) - Mobile security verification standard.
- [OWASP MASTG](https://mas.owasp.org/MASTG/) - Mobile testing guide.

---

## 22. Network, Wireless, Hardware and OT/ICS

### Network Attack and MITM

- [Responder](https://github.com/lgandx/Responder) - LLMNR/NBT-NS/mDNS poisoning and credential capture.
- [Inveigh](https://github.com/Kevin-Robertson/Inveigh) - Windows LLMNR/NBT-NS/mDNS/DHCPv6 spoofing.
- [mitm6](https://github.com/dirkjanm/mitm6) - IPv6 DNS takeover.
- [Bettercap](https://github.com/bettercap/bettercap) - MITM, sniffing and Wi-Fi.
- [Ettercap](https://www.ettercap-project.org/) - Classic MITM.
- [Wireshark](https://www.wireshark.org/) - Packet analysis.
- [tcpdump](https://www.tcpdump.org/) - Packet capture.
- [Scapy](https://scapy.net/) - Packet crafting.
- [arpspoof](https://linux.die.net/man/8/arpspoof) - ARP spoofing.
- [ntlmrelayx](https://github.com/fortra/impacket) - NTLM relay.
- [PetitPotam](https://github.com/topotam/PetitPotam) - Authentication coercion.
- [Coercer](https://github.com/p0dalirius/Coercer) - Automated coercion.
- [Responder](https://github.com/lgandx/Responder) - Poisoning and capture.

### Wireless

- [Aircrack-ng](https://www.aircrack-ng.org/) - Wi-Fi auditing.
- [Bettercap](https://github.com/bettercap/bettercap) - Wi-Fi and BLE.
- [hcxtools](https://github.com/ZerBea/hcxtools) - Handshake conversion.
- [Hashcat](https://hashcat.net/hashcat/) - GPU cracking.
- [Wifite](https://github.com/derv82/wifite2) - Automated wireless attacks.
- [EAPHammer](https://github.com/s0lst1c3/eaphammer) - Evil twin and EAP attacks.
- [WiFi-Pumpkin](https://github.com/P0cL4bs/wifipumpkin3) - Rogue AP framework.
- [Fluxion](https://github.com/FluxionNetwork/fluxion) - Wi-Fi social engineering.
- [Kismet](https://www.kismetwireless.net/) - Wireless detector and sniffer.
- Bluetooth and BLE research - GATT, pairing and BLE abuse (see HackTricks radio section).

### Hardware

- [Hak5](https://hak5.org/) - USB Rubber Ducky, Bash Bunny, LAN Turtle, WiFi Pineapple.
- [USB Rubber Ducky](https://github.com/hak5/usbrubberducky-payloads) - Keystroke injection and payloads.
- [Bash Bunny](https://hak5.org/) - Multi-function USB attack platform.
- [WiFi Pineapple](https://hak5.org/) - Wireless auditing.
- [LAN Turtle](https://hak5.org/) - Covert network access.
- [O.MG Cable](https://o.mg.lol/) - Implanted cable.
- [Proxmark3](https://github.com/RfidResearchGroup/proxmark3) - RFID and NFC.
- [Flipper Zero](https://flipperzero.one/) - Multi-tool for radio, RFID and NFC research.
- [ChipWhisperer](https://github.com/newaetech/chipwhisperer) - Side-channel analysis.
- [Bus Pirate](http://dangerousprototypes.com/docs/Bus_Pirate) - Hardware bus analysis.
- [Saleae Logic](https://www.saleae.com/) - Logic analysis.

### OT and ICS

- [Shodan](https://www.shodan.io/) - Industrial asset discovery.
- [Censys](https://search.censys.io/) - Internet asset discovery.
- [Nmap NSE](https://nmap.org/book/nse.html) - ICS protocol scripts.
- [Modbus](https://modbus.org/) - Protocol reference.
- [plcscan](https://github.com/yanlinlin82/plcscan) - PLC discovery.
- [s7scan](https://github.com/klsecservices/s7scan) - Siemens S7 discovery.
- [ISF (Industrial Exploitation Framework)](https://github.com/dark-lbp/isf) - ICS exploitation.
- [Metasploit ICS modules](https://github.com/rapid7/metasploit-framework) - ICS exploits.
- [Claroty](https://claroty.com/) - OT security (defense/vendor).
- [Dragos](https://www.dragos.com/) - OT threat intelligence (defense/vendor).
- [MITRE ATT&CK for ICS](https://attack.mitre.org/matrices/ics/) - Adversary tactics for ICS.
- [GRFICS](https://github.com/Fortiphyd/GRFICSv3) - ICS simulation.
- [OpenPLC](https://github.com/thiagoralves/OpenPLC_v3) - Open PLC for labs.

---

## 23. Exploit Development and Buffer Overflow

- [Buffer-Overflow-Labs](https://github.com/CyberSecurityUP/Buffer-Overflow-Labs) - Hands-on labs.
- [Buffer_Overflow](https://github.com/gh0x0st/Buffer_Overflow) - Windows buffer overflow guide.
- [Buffer-Overflow-Exploit-Development-Practice](https://github.com/freddiebarrsmith/Buffer-Overflow-Exploit-Development-Practice) - Practice.
- [Windows_BufferOverflowx32](https://github.com/21y4d/Windows_BufferOverflowx32) - 32-bit Windows exploitation.
- [Buffer-Overflow-Guide](https://github.com/johnjhacking/Buffer-Overflow-Guide) - Guide.
- [buffer-overflow-attack](https://github.com/npapernot/buffer-overflow-attack) - Educational examples.
- [OSCP-Buffer-Overflow](https://github.com/V1n1v131r4/OSCP-Buffer-Overflow) - OSCP-style practice.
- [BufferOverflow-Kit](https://github.com/KINGSABRI/BufferOverflow-Kit) - Toolkit.
- [awesome-exploit-development](https://github.com/FabioBaroni/awesome-exploit-development) - Curated resources.
- [pwntools](https://github.com/Gallopsled/pwntools) - CTF and exploit development framework.
- [linux-exploit-development-tutorial](https://github.com/hardenedlinux/linux-exploit-development-tutorial) - Linux exploitation.
- [Exploit-Challenges](https://github.com/Billy-Ellis/Exploit-Challenges) - Practice binaries.
- [Exploit-Development](https://github.com/wtsxDev/Exploit-Development) - Resources.
- [ROP Emporium](https://ropemporium.com/) - ROP practice.
- [How2Heap](https://github.com/shellphish/how2heap) - Heap exploitation.
- [Heap Exploitation](https://github.com/shellphish/how2heap) - glibc heap techniques.
- [Nightmare](https://github.com/guyinatuxedo/nightmare) - Binary exploitation course.
- [pwn.college](https://pwn.college/) - Free binary exploitation curriculum.
- [Corelan tutorials](https://www.corelan.be/) - Classic exploit writing.
- [FuzzySecurity tutorials](https://www.fuzzysecurity.com/tutorials.html) - Windows exploitation.
- [Windows Exploit Development](https://www.fuzzysecurity.com/tutorials.html) - Modern Windows heap and kernel research.
- [Kernel exploitation](https://github.com/xairy/linux-kernel-exploitation) - Windows and Linux kernel research.
- [pwndbg](https://github.com/pwndbg/pwndbg) - GDB plugin for exploitation.
- [GEF](https://github.com/hugsy/gef) - GDB enhanced features.
- [Ropper](https://github.com/sashs/Ropper) - ROP gadget finder.
- [ROPgadget](https://github.com/JonathanSalwan/ROPgadget) - Gadget finder.
- [one_gadget](https://github.com/david942j/one_gadget) - glibc one-gadget finder.
- [checksec](https://github.com/slimm609/checksec.sh) - Binary mitigation checks.
- [exploit.education](https://exploit.education/) - Practice targets.

---

## 24. Malware Analysis and Reverse Engineering

### Static and Dynamic Analysis

- [Ghidra](https://github.com/NationalSecurityAgency/ghidra) - NSA reverse engineering suite.
- [IDA Free](https://hex-rays.com/ida-free/) - Free IDA version.
- [IDA Pro](https://hex-rays.com/ida-pro/) - Commercial disassembler.
- [Binary Ninja](https://binary.ninja/) - Modern reverse engineering platform.
- [radare2](https://github.com/radareorg/radare2) - Reverse engineering framework.
- [rizin](https://github.com/rizinorg/rizin) - Fork of radare2.
- [Cutter](https://github.com/rizinorg/cutter) - GUI for rizin.
- [x64dbg](https://x64dbg.com/) - Windows debugger.
- [WinDbg](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/) - Windows kernel and user debugger.
- [OllyDbg](https://www.ollydbg.de/) - Legacy Windows debugger.
- [dnSpy](https://github.com/dnSpy/dnSpy) - .NET debugger and decompiler.
- [ILSpy](https://github.com/icsharpcode/ILSpy) - .NET decompiler.
- [de4dot](https://github.com/de4dot/de4dot) - .NET deobfuscator.
- [PE-bear](https://github.com/hasherezade/pe-bear) - PE analysis.
- [PEStudio](https://www.winitor.com/) - Static PE analysis.
- [CFF Explorer](https://ntcore.com/?page_id=388) - PE editor.
- [Detect It Easy](https://github.com/horsicq/Detect-It-Easy) - File type and packer detection.
- [YARA](https://github.com/VirusTotal/yara) - Pattern matching.
- [YARA-X](https://github.com/VirusTotal/yara-x) - Modern YARA.
- [CAPA](https://github.com/mandiant/capa) - Capability detection.
- [FLOSS](https://github.com/mandiant/flare-floss) - String deobfuscation.
- [strings](https://linux.die.net/man/1/strings) - Basic string extraction.
- [binwalk](https://github.com/ReFirmLabs/binwalk) - Firmware analysis.
- [Volatility3](https://github.com/volatilityfoundation/volatility3) - Memory forensics.
- [Rekall](https://github.com/google/rekall) - Memory forensics (legacy).
- [MemProcFS](https://github.com/ufrisk/MemProcFS) - Memory as a file system.
- [DIE](https://github.com/horsicq/Detect-It-Easy) - File identification.

### Sandboxing and Monitoring

- [CAPE](https://github.com/kevoreilly/CAPEv2) - Malware sandbox.
- [Cuckoo](https://github.com/cuckoosandbox/cuckoo) - Classic sandbox.
- [Procmon](https://learn.microsoft.com/en-us/sysinternals/downloads/procmon) - Process Monitor.
- [Process Hacker](https://processhacker.sourceforge.io/) - Process inspection.
- [API Monitor](http://www.rohitab.com/apimonitor) - API call monitoring.
- [Frida](https://frida.re/) - Dynamic instrumentation.
- [Speakeasy](https://github.com/mandiant/speakeasy) - Emulation.
- [Qiling](https://github.com/qilingframework/qiling) - Emulation framework.
- [Unicorn](https://github.com/unicorn-engine/unicorn) - CPU emulator.
- [TinyTracer](https://github.com/hasherezade/tiny_tracer) - API tracing.
- [FakeNet-NG](https://github.com/mandiant/flare-fakenet-ng) - Network simulation.
- [INetSim](https://www.inetsim.org/) - Network simulation.
- [Noriben](https://github.com/Rurik/Noriben) - Sandbox monitoring.
- [Sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon) - System monitoring.

### Malware Analysis Resources

- [awesome-malware-analysis](https://github.com/rshipp/awesome-malware-analysis) - Curated list.
- [malware-analysis topic](https://github.com/topics/malware-analysis) - GitHub topic.
- [Malware Analysis and Detection Engineering](https://github.com/Apress/malware-analysis-detection-engineering) - Book code.
- [SpiderLabs malware-analysis](https://github.com/SpiderLabs/malware-analysis) - Resources.
- [theZoo](https://github.com/ytisf/theZoo) - Live malware samples (handle carefully).
- [Malware-Analysis](https://github.com/arxlan786/Malware-Analysis) - Resources.
- [malzoo](https://github.com/nheijmans/malzoo) - Malware zoo.
- [PracticalMalwareAnalysis-Labs](https://github.com/mikesiko/PracticalMalwareAnalysis-Labs) - Book labs.
- [SSMA](https://github.com/secrary/SSMA) - Simple static malware analyzer.
- [aleph](https://github.com/merces/aleph) - Malware analysis toolkit.
- [retoolkit](https://github.com/mentebinaria/retoolkit) - Reverse engineering toolkit.
- [Reverse-Engineering](https://github.com/mytechnotalent/Reverse-Engineering) - Learning resources.
- [wtsxDev/reverse-engineering](https://github.com/wtsxDev/reverse-engineering) - Reverse engineering resources.
- [DoublePulsar detection script](https://github.com/countercept/doublepulsar-detection-script) - Detect DoublePulsar implants.
- [reverse-engineering topic](https://github.com/topics/reverse-engineering) - GitHub topic.
- [Z0FCourse_ReverseEngineering](https://github.com/0xZ0F/Z0FCourse_ReverseEngineering) - Course.
- [hax0rtahm1d/Reverse-Engineering](https://github.com/hax0rtahm1d/Reverse-Engineering) - Resources.
- [awesome-reversing](https://github.com/tylerha97/awesome-reversing) - Curated list.
- [Malpedia](https://malpedia.caad.fkie.fraunhofer.de/) - Malware family encyclopedia.
- [VirusTotal](https://www.virustotal.com/) - Sample and hash intelligence.
- [Hybrid Analysis](https://www.hybrid-analysis.com/) - Sandbox reports.
- [ANY.RUN](https://any.run/) - Interactive sandbox.
- [Joe Sandbox](https://www.joesandbox.com/) - Sandbox.
- [Triage](https://tria.ge/) - Sandbox.
- [MalwareBazaar](https://bazaar.abuse.ch/) - Sample repository.
- [URLhaus](https://urlhaus.abuse.ch/) - Malicious URL tracking.
- [ThreatFox](https://threatfox.abuse.ch/) - IOC sharing.
- Unpackme challenges - Unpacking practice (see Malware Unicorn and community crackmes).

---

## 25. Adversary Emulation and Purple Teaming

- [MITRE CALDERA](https://github.com/mitre/caldera) - Automated adversary emulation system.
- [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team) - Small, portable detection tests mapped to ATT&CK.
- [APTSimulator](https://github.com/NextronSystems/APTSimulator) - Make a system look compromised.
- [Network Flight Simulator](https://github.com/alphasoc/flightsim) - Generate malicious network traffic.
- [Metta](https://github.com/uber-common/metta) - Adversarial simulation.
- [Red Team Automation (RTA)](https://github.com/endgameinc/RTA) - Blue team detection testing.
- Prelude Operator - Adversary emulation (see Prelude documentation).
- [PurpleSharp](https://github.com/mvelazc0/PurpleSharp) - Purple team automation.
- [VECTR](https://github.com/SecurityRiskAdvisors/VECTR) - Track and report red/purple team results.
- [Infection Monkey](https://github.com/guardicore/monkey) - Breach and attack simulation.
- [Stratus Red Team](https://github.com/DataDog/stratus-red-team) - Cloud attack emulation.
- [Dark-Moon](https://github.com/ASCIT31/Dark-Moon) - Open-source autonomous AI penetration testing platform (suggested via GitHub issue/PR).
- [TIBER-EU](https://www.ecb.europa.eu/pub/pdf/other/ecb.tiber_eu_framework.en.pdf) - Intelligence-led red teaming.
- [CBEST](https://www.bankofengland.co.uk/) - UK intelligence-led testing.
- [iCAST](https://www.bankofengland.co.uk/) - Attack simulation testing.
- [Atomic Threat Coverage](https://github.com/atc-project/atomic-threat-coverage) - Detection coverage.
- [DeTTECT](https://github.com/rabobank-cdc/DeTTECT) - Detection coverage mapping.
- [MITRE ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/) - Technique coverage mapping.
- [SIGMA](https://github.com/SigmaHQ/sigma) - Detection rule format.
- [Awesome Threat Detection](https://github.com/0x4D31/awesome-threat-detection) - Detection engineering resources.

---

## 26. LLM, AI and Agentic Red Teaming

> AI red teaming targets the whole system: model, system prompt, retrieval data, tools, permissions, memory and the humans in the loop. A model that passes a safety benchmark can still be exploited through its tools.

### Frameworks and Standards

- [OWASP Top 10 for LLM Applications 2025](https://genai.owasp.org/llm-top-10/) - LLM01 prompt injection through LLM10 unbounded consumption.
- [OWASP Agentic Security Initiative](https://genai.owasp.org/) - Top 10 for agentic applications and threat modeling guidance.
- [OWASP MCP Top 10](https://genai.owasp.org/) - Security risks for Model Context Protocol deployments.
- [MITRE ATLAS](https://atlas.mitre.org/) - AI adversary tactics and techniques, including prompt injection, jailbreak, data poisoning, model theft and agent abuse.
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) - Risk governance and measurement.
- [NIST AI 600-1 Generative AI Profile](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence) - Generative AI risk profile.
- [Google SAIF](https://saif.google/) - Secure AI Framework.
- [Cloud Security Alliance MAESTRO](https://cloudsecurityalliance.org/) - Agentic AI threat modeling.
- [ISO/IEC 42001](https://www.iso.org/standard/81230.html) - AI management system standard.
- [EU AI Act](https://artificialintelligenceact.eu/) - Regulatory obligations.
- [OWASP AI Exchange](https://owaspai.org/) - Open AI security guidance.
- [AI Vulnerability Database (AVID)](https://avidml.org/) - AI vulnerability and failure taxonomy.
- [AI Incident Database](https://incidentdatabase.ai/) - Real-world AI incidents.
- [MLSecOps](https://mlsecops.com/) - AI/ML security operations community.

### LLM Red Teaming Tools

- [garak](https://github.com/NVIDIA/garak) - NVIDIA's LLM vulnerability scanner; probes and detectors for jailbreaks, prompt injection, leakage, toxicity, hallucination and more.
- [PyRIT](https://github.com/microsoft/PyRIT) - Microsoft's Python Risk Identification Toolkit; orchestrated multi-turn, multi-modal and agentic campaigns.
- [Promptfoo](https://github.com/promptfoo/promptfoo) - Plugin-based LLM red teaming and evals with CI integration; maps to OWASP LLM Top 10, NIST AI RMF and MITRE ATLAS.
- [DeepTeam](https://github.com/confident-ai/deepteam) - Open-source framework for red teaming LLMs and agents; 50+ vulnerability types and multi-turn attacks.
- [Giskard](https://github.com/Giskard-AI/giskard) - Testing and evaluation for ML and LLM systems, strong on RAG.
- [Augustus](https://github.com/praetorian-inc/augustus) - Go-based LLM security scanner with a large probe library.
- [Inspect AI](https://github.com/UKGovernmentBEIS/inspect_ai) - UK AI Safety Institute evaluation framework.
- [Inspect Evals](https://github.com/UKGovernmentBEIS/inspect_evals) - Evaluation suites including agentic and safety benchmarks.
- [PurpleLlama](https://github.com/meta-llama/PurpleLlama) - Meta's LLM safety and security toolkit, including CyberSecEval.
- [llm-guard](https://github.com/protectai/llm-guard) - Input/output scanning and guardrails.
- [Rebuff](https://github.com/protectai/rebuff) - Prompt injection detection.
- [NeMo Guardrails](https://github.com/NVIDIA/NeMo-Guardrails) - Programmable guardrails for conversational systems.
- [Guardrails AI](https://github.com/guardrails-ai/guardrails) - Output validation and structured generation.
- [Adversarial Robustness Toolbox (ART)](https://github.com/Trusted-AI/adversarial-robustness-toolbox) - Evasion, poisoning, extraction and inference attacks on ML models.
- [TextAttack](https://github.com/QData/TextAttack) - Adversarial NLP attacks and training.
- [Foolbox](https://github.com/bethgelab/foolbox) - Adversarial example library.
- [CleverHans](https://github.com/cleverhans-lab/cleverhans) - Adversarial example research.
- [llm-attacks](https://github.com/llm-attacks/llm-attacks) - GCG and adversarial suffix research.
- [Counterfit](https://github.com/Azure/counterfit) - Microsoft's archived ML attack tool (historical reference).

### MCP and Agentic Security Tooling

- [mcp-scan](https://github.com/invariantlabs-ai/mcp-scan) - Scan MCP servers for tool poisoning and unsafe configurations.
- [Agentic Radar](https://github.com/splx-ai/agentic-radar) - Agentic AI security scanner and threat modeling.
- [AgentDojo](https://github.com/ethz-spylab/agentdojo) - Dynamic evaluation of prompt injection attacks and defenses in agents.
- [InjecAgent](https://github.com/uiuc-kang-lab/InjecAgent) - Indirect prompt injection benchmark for tool-integrated agents.
- [PurpleLlama](https://github.com/meta-llama/PurpleLlama) - CyberSecEval and agentic risk evaluation.
- [Inspect Evals](https://github.com/UKGovernmentBEIS/inspect_evals) - AgentHarm and related agent safety evaluations.
- [MCP specification](https://modelcontextprotocol.io/) - Protocol reference and security considerations.
- [MCP security best practices](https://modelcontextprotocol.io/specification/draft/basic/security_best_practices) - Official guidance.

### Attack Techniques

**Prompt and instruction attacks**

- Direct prompt injection - user input overrides system/developer instructions.
- Indirect prompt injection - malicious instructions arrive via web pages, email, documents, RAG chunks, tool output, calendar invites or images.
- Stored and second-order injection - payload persists in memory, files or a knowledge base and triggers later.
- Payload splitting - the malicious instruction is distributed across fields, messages or documents.
- Encoding and obfuscation - Base64, ROT13, Unicode, homoglyphs, invisible characters, markdown/HTML comments, low-resource languages, ciphers.
- Role-play and persona jailbreaks - DAN, developer mode, hypothetical framing, emotional manipulation.
- Prefix and style injection - force an innocuous prefix to bypass refusal.
- Many-shot jailbreaking - long context filled with examples that normalize the target behavior.
- Multi-turn escalation - Crescendo, gradual reframing across turns.
- Automated jailbreaks - PAIR, Tree of Attacks with Pruning (TAP), GCG adversarial suffixes, AutoDAN, best-of-N sampling.
- System prompt extraction - repeated text, translation, summarization and formatting tricks.
- Safety bypass via tools - use a permitted tool to perform a forbidden action.
- Output handling attacks - markdown image exfiltration, link injection, XSS in rendered output, terminal escape sequences.
- Denial of service - context flooding, recursive tool calls, unbounded consumption, expensive reasoning loops.

**Data and model attacks**

- Sensitive information disclosure - PII, secrets, system prompts, adjacent-tenant data in RAG.
- Training data extraction and membership inference.
- Model extraction and stealing - replicate behavior through API queries.
- Data poisoning and backdooring - corrupt training, fine-tuning or retrieval data.
- Adversarial examples - perturbed inputs that change classification or generation.
- RAG poisoning - inject false or malicious entries into the vector store.
- Vector and embedding weaknesses - embedding inversion, cross-tenant retrieval, metadata leakage.
- Model supply chain - malicious models, pickles, LoRA adapters, tokenizers and dependencies.
- Model DoS - resource exhaustion, sponge examples, long-context abuse.

**Agentic and MCP attacks**

- Tool poisoning - malicious instructions embedded in tool descriptions or metadata.
- Rug pull - a benign tool changes behavior after installation or approval.
- Confused deputy - a malicious server shadows a benign tool and intercepts calls.
- Tool name collision and preference manipulation.
- Out-of-scope parameter abuse and parameter injection.
- Tool response poisoning - false errors, impersonation, tool transfer.
- Excessive agency - agent has more permissions than the task requires.
- Memory poisoning - persistent instructions or false facts stored across sessions.
- Cross-agent injection - one agent's output becomes another agent's trusted input.
- Human-in-the-loop bypass - social engineering the approver or exploiting auto-approval.
- Exfiltration through tool invocation - send data to an attacker-controlled endpoint via a legitimate tool.
- Credential and secret access through tools - file system, shell, browser, email and cloud connectors.
- MCP registry and server compromise - weak vetting, ownership checks and update channels.
- Remote MCP server attacks - both LLM-passive (server-side) and LLM-active (model-assisted) exploitation.

**Multimodal attacks**

- Instructions hidden in images, screenshots, PDFs, audio or video.
- Cross-modal injection - benign text plus malicious image.
- OCR and vision pipeline abuse.
- Steganographic and metadata payloads.
- Document parsing attacks - macros, embedded objects, external references.

### Benchmarks, Datasets and Practice

- [HackAPrompt](https://www.hackaprompt.com/) - Global prompt hacking competition and dataset.
- [Tensor Trust](https://tensortrust.ai/) - Prompt injection game and dataset.
- [Gandalf](https://gandalf.lakera.ai/) - Progressive prompt injection challenge.
- [Gray Swan Arena](https://www.grayswan.ai/) - AI red teaming competitions and evaluations.
- [Crucible](https://crucible.dreadnode.io/) - AI security challenges.
- [AI Village](https://aivillage.org/) - DEF CON AI Village talks and CTFs.
- [HarmBench](https://github.com/centerforaisafety/HarmBench) - Standardized harmful behavior evaluation.
- [JailbreakBench](https://github.com/JailbreakBench/jailbreakbench) - Jailbreak evaluation benchmark.
- [Open-Prompt-Injection](https://github.com/liu00222/Open-Prompt-Injection) - Prompt injection attacks and defenses benchmark.
- [AgentDojo](https://github.com/ethz-spylab/agentdojo) - Agent prompt injection benchmark.
- [InjecAgent](https://github.com/uiuc-kang-lab/InjecAgent) - Indirect injection benchmark.
- [AgentHarm](https://github.com/UKGovernmentBEIS/inspect_evals) - Agent harm benchmark.
- [MCPTox](https://arxiv.org/abs/2508.14925) - Tool poisoning benchmark for real-world MCP servers.
- [MCP Security Bench](https://arxiv.org/abs/2510.15994) - End-to-end MCP attack benchmark.
- [AI Incident Database](https://incidentdatabase.ai/) - Real incidents.
- [AVID](https://avidml.org/) - Vulnerability database.

### Key Papers

- [Not what you've signed up for: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection](https://arxiv.org/abs/2302.12173) - Greshake et al.
- [Universal and Transferable Adversarial Attacks on Aligned Language Models](https://arxiv.org/abs/2307.15043) - GCG.
- [Jailbreaking Black Box Large Language Models in Twenty Queries](https://arxiv.org/abs/2310.08419) - PAIR.
- [Tree of Attacks: Jailbreaking Black-Box LLMs Automatically](https://arxiv.org/abs/2312.02119) - TAP.
- [Great, Now Write an Article About That: The Crescendo Multi-Turn LLM Jailbreak Attack](https://arxiv.org/abs/2404.01833) - Crescendo.
- [Formalizing and Benchmarking Prompt Injection Attacks and Defenses](https://arxiv.org/abs/2310.12815) - Open-Prompt-Injection.
- [Extracting Training Data from Large Language Models](https://arxiv.org/abs/2012.07805) - Carlini et al.
- [Red Teaming Language Models with Language Models](https://arxiv.org/abs/2202.03286) - Perez et al.
- [AgentDojo: A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses for LLM Agents](https://arxiv.org/abs/2406.13352)
- [InjecAgent: Benchmarking Indirect Prompt Injections in Tool-Integrated LLM Agents](https://arxiv.org/abs/2403.02691)
- [AgentHarm: A Benchmark for Measuring Harmfulness of LLM Agents](https://arxiv.org/abs/2410.09024)
- [MCPTox: A Benchmark for Tool Poisoning Attack on Real-World MCP Servers](https://arxiv.org/abs/2508.14925)
- [MCP Security Bench (MSB): Benchmarking Attacks Against Model Context Protocol in LLM Agents](https://arxiv.org/abs/2510.15994)

### AI Red Team Resources

- [Embrace The Red](https://embracethered.com/blog/) - Johann Rehberger's AI red teaming research, especially indirect prompt injection and agent exploitation.
- [Simon Willison - Prompt Injection](https://simonwillison.net/tags/prompt-injection/) - The best running commentary and incident tracking.
- [Lakera Blog](https://www.lakera.ai/blog) - Prompt injection and LLM security research.
- [HiddenLayer Research](https://hiddenlayer.com/research/) - Model and AI supply chain security.
- [Protect AI](https://protectai.com/) - MLSecOps and AI security.
- [Mindgard Blog](https://mindgard.ai/blog) - AI red teaming and testing.
- [Promptfoo Blog](https://www.promptfoo.dev/blog/) - Red teaming methodology and tooling.
- [Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/) - AI red team and threat intelligence.
- [Google DeepMind Safety](https://deepmind.google/discover/blog/) - AI safety and adversarial research.
- [Anthropic Research](https://www.anthropic.com/research) - Model safety, red teaming and jailbreak research.
- [Awesome LLM Security](https://github.com/corca-ai/awesome-llm-security) - Curated LLM security resources.
- [Awesome LLM Attacks](https://github.com/martinholovsky/awesome-llm-attacks) - Attack catalog mapped to OWASP, ATLAS and MCP.
- [Prompt Injection Taxonomy](https://github.com/Hellsender01/prompt-injection-taxonomy) - 250+ techniques across categories.
- [L1B3RT4S](https://github.com/elder-plinius/L1B3RT4S) - Public jailbreak prompt collection (research awareness).
- [Microsoft AI Red Team](https://learn.microsoft.com/en-us/security/ai-red-team/) - Microsoft's AI red team guidance and playbooks.

### Defensive and Guardrail Engineering

- Instruction hierarchy and privilege separation between system, developer, user and tool content.
- Spotlighting and delimiting untrusted content.
- Dual-LLM and quarantined processing patterns.
- Capability-based tool permissions and least privilege.
- Human approval for high-impact tool calls.
- Deterministic egress allow-lists and no auto-rendering of links/images.
- Input and output classifiers, plus policy enforcement outside the model.
- Sandboxed tool execution and filesystem isolation.
- Retrieval provenance, tenant isolation and signed documents.
- Continuous evaluation in CI with regression tests for known attacks.
- Logging, tracing and anomaly detection for tool calls and data access.

---

## 27. Reporting and Collaboration

- [SysReptor](https://github.com/Syslifters/sysreptor) - Modern pentest reporting platform.
- [Dradis](https://dradisframework.com/) - Collaboration and reporting.
- [Pwndoc](https://github.com/pwndoc/pwndoc) - Pentest report generator.
- [Serpico](https://github.com/SerpicoProject/Serpico) - Pentest reporting.
- [Ghostwriter](https://github.com/GhostManager/Ghostwriter) - Reporting and engagement management.
- [Faraday](https://github.com/infobyte/faraday) - Vulnerability management and collaboration.
- [PlexTrac](https://plextrac.com/) - Commercial reporting platform.
- [AttackForge](https://attackforge.com/) - Pentest management.
- [Obsidian](https://obsidian.md/) - Markdown knowledge base for notes.
- [CherryTree](https://www.giuspen.net/cherrytree/) - Hierarchical notes.
- [CVSS](https://www.first.org/cvss/) - Severity scoring.
- [EPSS](https://www.first.org/epss/) - Exploit prediction scoring.
- [MITRE ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/) - Technique mapping.
- [Dradis templates](https://github.com/dradis/dradis-ce) - Report templates.
- Pentest report templates - See SysReptor and Ghostwriter repositories for community templates.

### Report Quality Checklist

- Executive summary written for non-technical stakeholders.
- Scope, timeline, rules of engagement and limitations.
- Attack narrative with evidence and timestamps.
- Findings with technical detail, business impact, evidence, remediation and references.
- Severity and risk rating methodology (CVSS, EPSS, client-specific).
- ATT&CK and kill-chain mapping.
- Reproducible steps and proof of impact.
- Cleanup and deconfliction notes.
- Strategic recommendations and a remediation roadmap.
- Retest criteria and verification steps.

---

## 28. Wordlists, Cheatsheets and Awesome Lists

### Wordlists

- [SecLists](https://github.com/danielmiessler/SecLists) - The essential collection.
- [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings) - Payloads and bypasses.
- [fuzzdb](https://github.com/fuzzdb-project/fuzzdb) - Fuzzing dictionaries.
- [Probable-Wordlists](https://github.com/berzerk0/Probable-Wordlists) - Real-world password lists.
- [Assetnote Wordlists](https://wordlists.assetnote.io/) - High-quality content discovery lists.
- [OneListForAll](https://github.com/six2dez/OneListForAll) - Consolidated wordlists.
- [n0kovo Subdomains](https://github.com/n0kovo/n0kovo_subdomains) - Subdomain wordlists.
- [Weakpass](https://weakpass.com/) - Password wordlists.
- [CrackStation](https://crackstation.net/) - Password cracking resources.
- [hashcat rules](https://github.com/hashcat/hashcat) - Rule-based cracking.
- [OneRuleToRuleThemAll](https://github.com/NotSoSecure/password_cracking_rules) - Effective hashcat rule.
- [KAONASHI](https://github.com/rokups/kaonashi) - Password profiling.
- [CUPP](https://github.com/Mebus/cupp) - Custom wordlist generation.
- [CeWL](https://github.com/digininja/CeWL) - Website wordlist generation.
- [Mentalist](https://github.com/sc0tfree/mentalist) - Wordlist generator.
- [Pydictor](https://github.com/LandGrey/pydictor) - Wordlist generator.

### Cheatsheets and Knowledge Bases

- [HackTricks](https://book.hacktricks.wiki/) - Web, network, cloud, binary and red team techniques.
- [The Hacker Recipes](https://www.thehacker.recipes/) - AD and infrastructure recipes.
- [Internal All The Things](https://github.com/swisskyrepo/InternalAllTheThings) - Internal pentest notes.
- [WADComs](https://wadcoms.github.io/) - Windows/AD command cheat sheet.
- [GTFOBins](https://gtfobins.github.io/) - Unix binary abuse.
- [LOLBAS](https://lolbas-project.github.io/) - Windows binary abuse.
- [LOLDrivers](https://www.loldrivers.io/) - Vulnerable drivers.
- [Living Off Trusted Sites](https://lots-project.com/) - Trusted domains.
- [HackTools](https://github.com/LasCC/HackTools) - Browser extension cheat sheet.
- [ired.team](https://www.ired.team/) - Red team notes and experiments.
- [AD Security](https://adsecurity.org/) - Sean Metcalf's AD security knowledge.
- [Pentest Book](https://github.com/six2dez/pentest-book) - Pentest notes.
- [Red Teaming Cheat Sheet](https://github.com/0xJs/RedTeaming_CheatSheet) - Commands and techniques.
- [MITRE ATT&CK](https://attack.mitre.org/) - Technique reference.
- [MITRE ATLAS](https://atlas.mitre.org/) - AI technique reference.
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/) - Defensive guidance.

### Awesome Lists and Repositories

- [Red-Teaming-Toolkit](https://github.com/infosecn1nja/Red-Teaming-Toolkit) - Curated red team toolkit.
- [Pentest-Tools](https://github.com/S3cur3Th1sSh1t/Pentest-Tools) - Pentest tool collection.
- [Awesome-Red-Teaming](https://github.com/yeyintminthuhtut/Awesome-Red-Teaming) - Curated red team list.
- [awesome-pentest](https://github.com/enaqx/awesome-pentest) - Pentest resources.
- [Awesome-Pentest (Muhammd)](https://github.com/Muhammd/Awesome-Pentest) - Pentest resources.
- [Awesome-PenTest-Practice](https://github.com/CyberSecurityUP/Awesome-PenTest-Practice) - Practice resources.
- [awesome-oscp](https://github.com/0x4D31/awesome-oscp) - OSCP resources.
- [OSCP-Human-Guide](https://github.com/six2dez/OSCP-Human-Guide) - OSCP guide.
- [OSCP-Prep](https://github.com/RustyShackleford221/OSCP-Prep) - OSCP preparation.
- [OSCP-Survival-Guide](https://github.com/wwong99/pentest-notes/blob/master/oscp_resources/OSCP-Survival-Guide.md) - Survival guide.
- [awesome-c2-frameworks](https://github.com/loseys/awesome-c2-frameworks) - C2 comparison and resources.
- [awesome-malware-analysis](https://github.com/rshipp/awesome-malware-analysis) - Malware analysis.
- [awesome-reversing](https://github.com/tylerha97/awesome-reversing) - Reverse engineering.
- [awesome-cloud-security](https://github.com/Su1ph3r/awesome-cloud-security) - Cloud security resources.
- [awesome-llm-security](https://github.com/corca-ai/awesome-llm-security) - LLM security.
- [awesome-llm-attacks](https://github.com/martinholovsky/awesome-llm-attacks) - LLM attacks.
- [Awesome-Red-Team-Operations](https://github.com/JoasASantos/Awesome-Red-Team-Operations) - This repository.
- [Google Drive resource folder](https://drive.google.com/drive/u/0/folders/12Mvq6kE2HJDwN2CZhEGWizyWt87YunkU) - Community shared resources.

---

## 29. Blogs, Articles, Research and Newsletters

### Red Team and Offensive Security Blogs

- [SpecterOps Blog](https://specterops.io/blog/) - AD, Azure, BloodHound and tradecraft.
- [TrustedSec Blog](https://www.trustedsec.com/blog/) - Red team and adversary research.
- [MDSec Research](https://www.mdsec.co.uk/knowledge-centre/) - Windows internals, evasion and C2.
- [Outflank Blog](https://outflank.nl/blog/) - Windows and AD research.
- [ired.team](https://www.ired.team/) - Hands-on red team notes.
- [Black Hills Information Security](https://www.blackhillsinfosec.com/blog/) - Practical offensive and defensive content.
- [SANS Internet Storm Center](https://isc.sans.edu/) - Daily threat and detection notes.
- [The DFIR Report](https://thedfirreport.com/) - Real intrusion walkthroughs and TTPs.
- [Red Canary Blog](https://redcanary.com/blog/) - Detection engineering.
- [Palo Alto Unit 42](https://unit42.paloaltonetworks.com/) - Threat research and tooling analysis.
- [Mandiant Blog](https://www.mandiant.com/resources/blog) - Threat intelligence and malware.
- [CrowdStrike Blog](https://www.crowdstrike.com/blog/) - Adversary tradecraft and cloud.
- [Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/) - Threat intelligence and AI security.
- [Google Threat Intelligence](https://cloud.google.com/blog/topics/threat-intelligence) - APT and malware research.
- [Cisco Talos](https://blog.talosintelligence.com/) - Threat research.
- [SentinelLabs](https://www.sentinelone.com/labs/) - Malware and adversary research.
- [Elastic Security Labs](https://www.elastic.co/security-labs) - Detection and malware.
- [WithSecure Labs](https://labs.withsecure.com/) - Research.
- [Zero Day Initiative](https://www.zerodayinitiative.com/blog) - Vulnerability research.
- [Project Zero](https://googleprojectzero.blogspot.com/) - Deep vulnerability research.
- [Trail of Bits Blog](https://blog.trailofbits.com/) - Security engineering and exploitation.
- [Include Security Blog](https://blog.includesecurity.com/) - Tooling and C2 research.
- [Bishop Fox Blog](https://bishopfox.com/blog) - Red team tools and cloud.
- [Praetorian Blog](https://www.praetorian.com/blog/) - Offensive security and AI.
- [Dreadnode](https://blog.dreadnode.io/) - AI and offensive research.
- [Embrace The Red](https://embracethered.com/blog/) - AI/LLM red teaming.
- [Simon Willison](https://simonwillison.net/) - Prompt injection and AI security.
- [Lakera Blog](https://www.lakera.ai/blog) - LLM security.
- [HiddenLayer](https://hiddenlayer.com/research/) - AI supply chain and model security.
- [Protect AI](https://protectai.com/) - MLSecOps.
- [Mindgard](https://mindgard.ai/blog) - AI red teaming.
- [HackTricks](https://book.hacktricks.wiki/) - Technique wiki.
- [The Hacker Recipes](https://www.thehacker.recipes/) - AD and infrastructure.
- [AD Security](https://adsecurity.org/) - Active Directory security.
- [Red Team Guide](https://redteam.guide/) - Methodology.
- [Pentest Book](https://github.com/six2dez/pentest-book) - Notes.

### Newsletters and Podcasts

- [tl;dr sec](https://tldrsec.com/) - Weekly security research digest.
- [Detection Engineering Weekly](https://www.detectionengineering.net/) - Detection content.
- [Risky Business](https://risky.biz/) - Security news and interviews.
- [Darknet Diaries](https://darknetdiaries.com/) - Stories from the breach side.
- [Malicious Life](https://malicious.life/) - Malware history and interviews.
- [SANS NewsBites](https://www.sans.org/newsletters/newsbites/) - Weekly news.
- [SANS ISC](https://isc.sans.edu/) - Daily handlers' diary.
- [CyberWire](https://thecyberwire.com/) - Daily briefing.
- [Krebs on Security](https://krebsonsecurity.com/) - Investigative security journalism.
- [BleepingComputer](https://www.bleepingcomputer.com/) - Security news.
- [The Record](https://therecord.media/) - Cyber policy and incidents.
- [Hacker News](https://news.ycombinator.com/) - Technical community.
- [Red Team Village](https://redteamvillage.io/) - Community content.

### Research Repositories and Aggregators

- [Papers We Love](https://github.com/papers-we-love/papers-we-love) - Computer science papers.
- [arXiv cs.CR](https://arxiv.org/list/cs.CR/recent) - Recent security papers.
- [arXiv cs.AI](https://arxiv.org/list/cs.AI/recent) - AI research.
- [Semantic Scholar](https://www.semanticscholar.org/) - Research search.
- [Google Scholar](https://scholar.google.com/) - Academic search.
- [USENIX Security](https://www.usenix.org/conferences) - Conference proceedings.
- [IEEE S&P](https://www.ieee-security.org/) - Security and privacy.
- [ACM CCS](https://www.sigsac.org/ccs.html) - Computer and communications security.
- [NDSS](https://www.ndss-symposium.org/) - Network and distributed system security.
- [Black Hat archives](https://www.blackhat.com/html/archives.html) - Talk archives.
- [DEF CON media](https://media.defcon.org/) - Talk archives.

---

## 30. Conferences and Talks

### Offensive Security Conferences

- [DEF CON](https://defcon.org/) - The largest hacker conference; villages, CTFs and talks.
- [Black Hat](https://www.blackhat.com/) - Briefings and trainings.
- [BSides](https://www.securitybsides.com/) - Global community conferences.
- [HITB](https://conference.hitb.org/) - Hack In The Box.
- [Troopers](https://troopers.de/) - Deep technical security conference.
- [Sec-T](https://www.sec-t.org/) - Sweden.
- [Chaos Communication Congress](https://events.ccc.de/) - CCC.
- [OffensiveCon](https://www.offensivecon.org/) - Offensive security research.
- [REcon](https://recon.cx/) - Reverse engineering.
- [SSTIC](https://www.sstic.org/) - French security conference.
- [Botconf](https://www.botconf.eu/) - Botnet and malware research.
- [Nullcon](https://nullcon.net/) - India.
- [hack.lu](https://hack.lu/) - Luxembourg.
- [Hexacon](https://www.hexacon.fr/) - Offensive security.
- [Insomni'hack](https://insomnihack.ch/) - Switzerland.
- [Pwn2Own](https://www.pwn2own.com/) - Exploitation contest.
- [TyphoonCon](https://typhooncon.com/) - Japan.
- [Zer0Con](https://zer0con.org/) - Korea.
- [SecTor](https://www.blackhat.com/sector/) - Canada.
- [Wild West Hackin' Fest](https://wildwesthackinfest.com/) - Community conference.
- [Kernelcon](https://kernelcon.org/) - Community conference.
- [GrrCon](https://grrcon.com/) - Community conference.
- [ShmooCon](https://shmoocon.org/) - East coast community conference.
- [CircleCityCon](https://circlecitycon.com/) - Community conference.
- [AI Village](https://aivillage.org/) - DEF CON AI Village.
- [Red Team Village](https://redteamvillage.io/) - DEF CON Red Team Village.
- [Adversary Village](https://adversaryvillage.org/) - DEF CON Adversary Village.
- [Blue Team Village](https://blueteamvillage.org/) - DEF CON Blue Team Village.
- [ATT&CKcon](https://attack.mitre.org/resources/attackcon/) - ATT&CK community.
- [SANS Summit](https://www.sans.org/cyber-security-summit/) - SANS summits.
- [RSA Conference](https://www.rsaconference.com/) - Industry conference.
- [WiCyS](https://www.wicys.org/) - Women in CyberSecurity.
- [The Diana Initiative](https://www.dianainitiative.org/) - Diversity in security.

---

## 31. Books

### Red Team and Penetration Testing

- **The Hacker Playbook 3** - Peter Kim.
- **Red Team Development and Operations** - Joe Vest and James Tubberville.
- **Red Team Field Manual (RTFM)** - Ben Clark.
- **Operator Handbook** - Joshua Picolet.
- **Penetration Testing: A Hands-On Introduction to Hacking** - Georgia Weidman.
- **The Web Application Hacker's Handbook** - Dafydd Stuttard and Marcus Pinto.
- **The Tangled Web** - Michal Zalewski.
- **Web Application Security: Exploitation and Countermeasures** - Andrew Hoffman.
- **Bug Bounty Bootcamp** - Vickie Li.
- **Real-World Bug Hunting** - Peter Yaworski.
- **Web Hacking 101** - Peter Yaworski.
- **Hacking APIs** - Corey Ball.
- **The Pentester BluePrint** - Phillip Wylie and Kim Crawley.
- **Adversarial Tradecraft in Cybersecurity** - Dan Borges.
- **Red Team Strategies** - Johann Rehberger (AI/LLM red teaming).
- **The Art of Cyberwarfare** - Jon DiMaggio.
- **Sandworm** - Andy Greenberg.
- **This Is How They Tell Me the World Ends** - Nicole Perlroth.
- **Countdown to Zero Day** - Kim Zetter.
- **The Cuckoo's Egg** - Clifford Stoll.
- **Ghost in the Wires** - Kevin Mitnick.
- **The Art of Deception** - Kevin Mitnick.
- **The Art of Intrusion** - Kevin Mitnick.
- **Kingpin** - Kevin Poulsen.
- **The Art of Invisibility** - Kevin Mitnick.
- **Social Engineering: The Science of Human Hacking** - Christopher Hadnagy.
- **The Psychology of Social Engineering** - various.

### Exploitation, Malware and Reverse Engineering

- **Hacking: The Art of Exploitation** - Jon Erickson.
- **The Shellcoder's Handbook** - Chris Anley et al.
- **Practical Malware Analysis** - Michael Sikorski and Andrew Honig.
- **Practical Reverse Engineering** - Bruce Dang et al.
- **The IDA Pro Book** - Chris Eagle.
- **Ghidra Book** - Chris Eagle and Kara Nance.
- **Practical Binary Analysis** - Dennis Andriesse.
- **Learning Linux Binary Analysis** - Ryan O'Neill.
- **The Art of Memory Forensics** - Michael Ligh et al.
- **Windows Internals** - Mark Russinovich et al.
- **Windows via C/C++** - Jeffrey Richter and Christophe Nasarre.
- **The Art of Software Security Assessment** - Mark Dowd et al.
- **A Bug Hunter's Diary** - Tobias Klein.
- **Fuzzing for Software Security Testing** - Ari Takanen et al.
- **The Fuzzing Book** - Andreas Zeller et al.

### Active Directory, Cloud and Identity

- **Active Directory Security** - Sean Metcalf (articles and talks).
- **Attacking Active Directory** - various community resources.
- **Azure Security** - various; see Microsoft Learn and SpecterOps.
- **Cloud Security Handbook** - various.
- **Kubernetes Security** - Liz Rice and Michael Hausenblas.
- **Container Security** - Liz Rice.
- **Hacking Kubernetes** - Andrew Martin and Michael Hausenblas.
- **AWS Security** - Dylan Shields.
- **Practical Cloud Security** - Chris Dotson.
- **Identity and Access Management** - various.

### AI and LLM Security

- **Red Team Strategies** - Johann Rehberger.
- **The Developer's Playbook for Large Language Model Security** - Steve Wilson.
- **AI Security and Privacy** - various.
- **Adversarial Machine Learning** - various academic texts.
- **Practical AI Security** - community resources.

---

## 32. Training, Labs and Certifications

> Certifications validate baseline knowledge. Hands-on labs, real engagements and the ability to explain impact are what actually matter.

### Training Providers and Courses

- [Red Team Leaders](https://redteamleaders.com/) - Red team operations training founded by Joas A Santos.
- [Red Team Leaders Courses](https://courses.redteamleaders.com/) - Course platform for red team, cloud, AD and offensive security training.
- [White Knight Labs Training](https://training.whiteknightlabs.com/) - Hands-on offensive security training built by active red team operators.
- [White Knight Labs - ARTOC](https://training.whiteknightlabs.com/live-training/advanced-red-team-operations-certification/) - Advanced Red Team Operations Certification.
- [White Knight Labs - OAOTC](https://training.whiteknightlabs.com/live-training/offensive-azure-operations-and-tactics-certification/) - Offensive Azure Operations and Tactics Certification.
- [White Knight Labs - ODPC](https://training.whiteknightlabs.com/live-training/offensive-development-practitioner-certification/) - Offensive Development Practitioner Certification (evasion and malware development).
- [White Knight Labs - OADOC](https://training.whiteknightlabs.com/offensive-active-directory-operations-certification/) - Offensive Active Directory Operations Certification.
- [White Knight Labs - OGOTC](https://training.whiteknightlabs.com/offensive-gcp-operations-and-tactics-certification-ogotc) - Offensive GCP Operations and Tactics Certification.
- [White Knight Labs - ASCPC](https://training.whiteknightlabs.com/ascpc-certification) - Attacking and Securing CI/CD Pipelines Certification.
- [White Knight Labs - ELPT](https://training.whiteknightlabs.com/certifications/entry-level-penetration-tester-certification/) - Entry-Level Penetration Tester Certification.
- [White Knight Labs Academy](https://training.whiteknightlabs.com/academy/) - Academy and on-demand content.
- [White Knight Labs CertForge Pro](https://training.whiteknightlabs.com/certforge-pro/) - Subscription access.
- [SANS Institute](https://www.sans.org/) - SEC560, SEC542, SEC565, SEC588, SEC660, SEC670, SEC760 and more.
- [OffSec](https://www.offsec.com/) - OSCP, OSEP, OSWE, OSED, OSWP and OSCE3.
- [Zero-Point Security](https://www.zeropointsecurity.co.uk/) - CRTO, CRTL and Red Team Ops.
- [Altered Security](https://www.alteredsecurity.com/) - CRTP, CRTE, CRTL and Azure AD courses.
- [SpecterOps Training](https://specterops.io/training/) - AD, BloodHound and adversary tradecraft.
- [TCM Security](https://academy.tcm-sec.com/) - PNPT, PJPT, PEH and practical courses.
- [Antisyphon Training](https://www.antisyphontraining.com/) - Pay-what-you-can defensive and offensive training.
- [Black Hills Information Security](https://www.blackhillsinfosec.com/) - Training and webcasts.
- [MalDev Academy](https://maldevacademy.com/) - Malware development and evasion.
- [Sektor7 Institute](https://institute.sektor7.net/) - Malware development and red team courses.
- [PentesterLab](https://pentesterlab.com/) - Web and code review labs.
- [PortSwigger Web Security Academy](https://portswigger.net/web-security) - Free web security labs.
- [Hack The Box Academy](https://academy.hackthebox.com/) - Offensive security paths.
- [TryHackMe](https://tryhackme.com/) - Guided labs and red team paths.
- [INE Security](https://ine.com/) - eJPT, eCPPT, eWPT and eWPTX.
- [APIsec University](https://www.apisecuniversity.com/) - API security.
- [Cybrary](https://www.cybrary.it/) - Security training.
- [Cloud Security Alliance](https://cloudsecurityalliance.org/education/) - Cloud security training.
- [Microsoft Learn](https://learn.microsoft.com/training/) - Azure and security learning paths.
- [AWS Skill Builder](https://skillbuilder.aws/) - AWS security learning.
- [Google Cloud Skills Boost](https://www.cloudskillsboost.google/) - GCP learning.
- [AI Village](https://aivillage.org/) - AI security talks and CTFs.
- [MLSecOps](https://mlsecops.com/) - AI/ML security community and content.

### Hands-On Labs and Ranges

- [Hack The Box](https://www.hackthebox.com/) - Machines, challenges and Pro Labs.
- [HTB Pro Labs](https://www.hackthebox.com/hacker/pro-labs) - Dante, Offshore, Cybernetics, RastaLabs, APTLabs and Zephyr.
- [TryHackMe](https://tryhackme.com/) - Guided and challenge labs.
- [OffSec Proving Grounds](https://www.offsec.com/labs/) - Practice machines.
- [Vulnlab](https://www.vulnlab.com/) - AD and internal labs.
- [PentesterLab](https://pentesterlab.com/) - Web exploitation labs.
- [PortSwigger Web Security Academy](https://portswigger.net/web-security) - Free labs.
- [pwn.college](https://pwn.college/) - Binary exploitation.
- [OverTheWire](https://overthewire.org/wargames/) - Classic wargames.
- [Root-Me](https://www.root-me.org/) - Challenges.
- [RingZer0](https://ringzer0ctf.com/) - CTF challenges.
- [VulnHub](https://www.vulnhub.com/) - Vulnerable VMs.
- [Hack The Box Academy](https://academy.hackthebox.com/) - Learning paths.
- [CyberDefenders](https://cyberdefenders.org/) - Blue team labs.
- [Blue Team Labs Online](https://blueteamlabs.online/) - Defensive labs.
- [LetsDefend](https://letsdefend.io/) - SOC and detection labs.
- [RangeForce](https://www.rangeforce.com/) - Cyber ranges.
- [Immersive Labs](https://www.immersivelabs.com/) - Cyber skills platform.
- [CloudGoat](https://github.com/RhinoSecurityLabs/cloudgoat) - AWS practice.
- [IAM Vulnerable](https://github.com/BishopFox/iam-vulnerable) - AWS IAM practice.
- [Kubernetes Goat](https://github.com/madhuakula/kubernetes-goat) - Kubernetes practice.
- [GRFICS](https://github.com/Fortiphyd/GRFICSv3) - ICS simulation.
- [OWASP crAPI](https://github.com/OWASP/crAPI) - API practice.
- [Damn Vulnerable GraphQL](https://github.com/dolevf/Damn-Vulnerable-GraphQL-Application) - GraphQL practice.
- [HackAPrompt](https://www.hackaprompt.com/) - Prompt injection practice.
- [Gandalf](https://gandalf.lakera.ai/) - LLM prompt injection game.
- [Tensor Trust](https://tensortrust.ai/) - Prompt injection game.
- [Gray Swan Arena](https://www.grayswan.ai/) - AI red teaming challenges.
- [Crucible](https://crucible.dreadnode.io/) - AI security challenges.

### Bug Bounty Platforms

- [HackerOne](https://www.hackerone.com/) - Bug bounty and VDP.
- [Bugcrowd](https://www.bugcrowd.com/) - Crowdsourced security.
- [Intigriti](https://www.intigriti.com/) - European bug bounty.
- [YesWeHack](https://www.yeswehack.com/) - Global bug bounty.
- [Open Bug Bounty](https://www.openbugbounty.org/) - Coordinated disclosure.
- [Synack](https://www.synack.com/) - Managed bug bounty.
- [Immunefi](https://immunefi.com/) - Web3 bug bounty.
- [HackenProof](https://hackenproof.com/) - Web3 and Web2 bounties.
- [Cobalt](https://www.cobalt.io/) - Pentest as a service.

### Certifications Map

- **Entry:** eJPT, PJPT, ELPT, PNPT, CEH (awareness).
- **Web:** OSWE, eWPT, eWPTX, Burp Suite Certified Practitioner.
- **Infrastructure:** OSCP, CRTP, PNPT, OADOC.
- **Red Team:** OSEP, CRTO, CRTL, ARTOC, CRTE.
- **Exploit Development:** OSED, OSEE, ODPC.
- **Cloud:** AWS Security Specialty, AZ-500, GCP Professional Cloud Security Engineer, OAOTC, OGOTC.
- **Detection/Blue:** GCIH, GCIA, GDAT, GCDA, BTL1, CDSA.
- **Management:** CISSP, CCSP, CISM, CISA.
- **AI Security:** emerging vendor and community certifications; prioritize hands-on AI red teaming portfolios.

---

## 33. Contributing

Contributions are welcome. Please:

1. Open an issue or pull request with a short description of the tool, technique or resource.
2. Use the existing format: name, link and a one-line description.
3. Add tools to the most specific section, not to multiple sections.
4. Prefer actively maintained projects; mark archived or historical tools clearly.
5. Include cloud, identity, AI/LLM and detection content where relevant.
6. Do not submit malware, stolen data, credentials or unlicensed commercial content.

**Issues reviewed (November 2026):** The repository issues were checked while updating this list. The only substantive tool suggestion was [Dark-Moon](https://github.com/ASCIT31/Dark-Moon), an open-source autonomous AI penetration testing platform, which has been added under Adversary Emulation. The remaining open issues contained no actionable tool or technique suggestions.

### Attribution

Originally created by Joas A Santos and S3cur3Th1sSh1t. Maintained by the community. All tools, techniques and resources belong to their respective authors and projects. This list is for authorized security testing and education only.

### License

This curated list is released under the MIT License. Individual tools and resources retain their own licenses.

---

**Stay legal, stay scoped, and document everything.**







