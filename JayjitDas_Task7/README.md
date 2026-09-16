# OASIS INFOBYTE - Security Analyst Internship

# Task 7: Vulnerability Scanning with Nikto

## Project Information

- **Internship:** OASIS Infobyte – Security Analyst
- **Task:** Task 7 – Vulnerability Scanning with Nikto
- **Level:** Intermediate
- **Tool:** Nikto
- **Operating System:** Kali Linux
- **Target:** 192.168.56.101
- **Target Environment:** Local Metasploitable / DVWA security-training laboratory
- **Target Protocol:** HTTP
- **Target Port:** 80
- **Nikto Version:** 2.6.1

---

## 1. Objective

The objective of this task is to use Nikto to perform an automated
web-server security scan, analyze the findings, identify security
issues, assign appropriate severity levels, and recommend remediation
steps.

All testing was performed against a locally controlled and authorized
security-training environment.

---

## 2. What is Nikto?

Nikto is an open-source web-server scanner used to perform tests for
security-related issues in web servers.

It can identify areas such as:

- Server and software misconfigurations
- Outdated server and software versions
- Default files and programs
- Insecure or exposed files
- Directory indexing
- HTTP configuration problems
- Security-header issues
- Other potentially dangerous web-server conditions

Nikto is a specialized web-server assessment tool and is different
from a general network scanner such as Nmap.

---

## 3. Lab Environment

The target used for this task was:

```text
http://192.168.56.101

The target was an intentionally vulnerable system in a controlled
local laboratory environment.

Nikto was executed from Kali Linux against the target web server.

4. Installation and Version Verification

Nikto was verified on Kali Linux using:

nikto -Version

The installed Nikto version was:
Nikto v2.6.1

5. Basic Nikto Scan

The basic scan was performed using:

nikto -h http://192.168.56.101

The complete scan output was saved to:

nikto_scan_results.txt

The output was saved using:

nikto -h http://192.168.56.101 -o nikto_scan_results.txt
Scan Summary
Target IP:       192.168.56.101
Target Port:     80
Server:          Apache/2.2.8 (Ubuntu) DAV/2
Nikto Version:   2.6.1
Requests:        8235
Errors:          0
Items Reported:  31
Hosts Tested:    1
6. Important Findings

The Nikto scan reported multiple security-related issues and
configuration weaknesses.

The following severity ratings are analyst-assigned for this
educational assessment. They are not official Nikto severity labels.

Finding 1 — Outdated Apache Web Server

Severity: High

Observed:

Apache/2.2.8 (Ubuntu) DAV/2

Issue:

The target is running an old Apache web-server version.

Risk:

Old software may contain publicly known security weaknesses and may no
longer receive security updates.

Recommendation:

Upgrade Apache to a currently supported release and keep the operating
system and web-server packages regularly patched.

Finding 2 — Outdated PHP Version

Severity: High

Observed:

PHP/5.2.4-2ubuntu5.10

Nikto reported that this PHP version appears to be outdated.

Risk:

Unsupported or obsolete software may contain known vulnerabilities and
can significantly increase the attack surface.

Recommendation:

Upgrade PHP to a supported version and remove obsolete components.

Finding 3 — PHP Information Disclosure

Severity: High

Observed:

/phpinfo.php: Output from the phpinfo() function was found.

Nikto also reported that PHP information and a PHP test script were
accessible.

Risk:

phpinfo() can expose detailed information about the PHP environment,
server configuration, modules, paths, and other technical details.

Recommendation:

Remove phpinfo.php and other diagnostic scripts from production
systems or restrict them to authorized administrators.

Finding 4 — Directory Indexing on /icons/

Severity: Medium

Observed:

/icons/: Directory indexing found.

Risk:

Directory listing can expose files and directory structure that should
not be publicly visible.

Recommendation:

Disable directory indexing unless it is explicitly required and
restrict access to sensitive directories.

Finding 5 — Directory Indexing on /doc/

Severity: Medium

Observed:

/doc/: Directory indexing found.

Nikto also reported that the directory is browsable.

Risk:

Browsable documentation or system directories may expose information
useful to an attacker.

Recommendation:

Remove unnecessary public documentation, disable directory listing,
and restrict access to administrative or internal documentation.

Finding 6 — Directory Indexing on /test/

Severity: Medium

Observed:

/test/: Directory indexing found.

Risk:

Test directories may contain debugging files, temporary applications,
old scripts, or sensitive information.

Recommendation:

Remove unused test directories from production systems or restrict
them to authorized users.

Finding 7 — Active HTTP TRACE Method

Severity: Medium

Observed:

HTTP TRACE method is active and replies

Nikto indicated that this may expose the host to Cross-Site Tracing
(XST)-related risks.

Risk:

An unnecessarily enabled TRACE method increases the HTTP attack surface
and may create security concerns in certain application environments.

Recommendation:

Disable the TRACE method unless it is explicitly required and verify
the web-server configuration.

Finding 8 — Missing X-Content-Type-Options Header

Severity: Low

Observed:

Suggested security header missing: x-content-type-options

Risk:

The absence of this header can reduce protection against MIME-type
sniffing behavior in supporting browsers.

Recommendation:

Configure the server to send an appropriate:

X-Content-Type-Options: nosniff

header where appropriate.

Finding 9 — Missing Strict-Transport-Security Header

Severity: Low / Informational

Observed:

Suggested security header missing: strict-transport-security

Risk:

HSTS helps browsers enforce HTTPS for sites that support secure HTTP.

Because this target was tested over HTTP and HTTPS was not available,
the practical applicability of HSTS to this specific test target is
limited.

Recommendation:

For production websites using HTTPS, configure an appropriate
Strict-Transport-Security policy.

Finding 10 — Missing Referrer-Policy Header

Severity: Low

Observed:

Suggested security header missing: referrer-policy

Risk:

Without an appropriate Referrer-Policy, browsers may send more
referrer information than intended depending on the request context.

Recommendation:

Configure a suitable Referrer-Policy according to application
requirements.

Finding 11 — Missing Permissions-Policy Header

Severity: Low

Observed:

Suggested security header missing: permissions-policy

Risk:

The absence of this header means browser-controlled feature
restrictions are not explicitly configured through this mechanism.

Recommendation:

Configure Permissions-Policy where appropriate to restrict
unnecessary browser capabilities.

Finding 12 — Missing Content-Security-Policy Header

Severity: Medium

Observed:

Suggested security header missing: content-security-policy

Risk:

A properly designed Content-Security-Policy can reduce the impact of
certain client-side attacks, including some forms of cross-site
scripting.

Recommendation:

Develop and deploy an appropriate Content-Security-Policy based on the
application's actual resources and functionality.

Finding 13 — X-Powered-By Information Disclosure

Severity: Low

Observed:

Retrieved x-powered-by header: PHP/5.2.4-2ubuntu5.10

Risk:

The response reveals the server-side technology and exact PHP version.

This information can help attackers fingerprint the application stack.

Recommendation:

Remove or minimize technology-identifying response headers where
practical and keep software patched.

Finding 14 — PHP Easter Eggs Exposed

Severity: Medium

Nikto detected PHP Easter Egg information through HTTP requests
containing specific query strings.

Risk:

Although these features are primarily informational, exposing
unnecessary implementation details can assist server fingerprinting
and reconnaissance.

Recommendation:

Disable unnecessary PHP Easter Egg features where supported and avoid
exposing unnecessary technology information.

Finding 15 — phpMyAdmin Accessible

Severity: High

Observed paths included:

/phpMyAdmin/ChangeLog
/phpMyAdmin/changelog.php
/phpMyAdmin/Documentation.html
/phpMyAdmin/README

Risk:

Publicly accessible phpMyAdmin significantly increases the attack
surface because it is a database administration interface.

Recommendation:

Restrict phpMyAdmin to authorized administrators, preferably through
network access controls or other strong access restrictions. Remove
it from production servers when it is not required.

Finding 16 — phpMyAdmin ChangeLog / ETag Information Disclosure

Severity: Low

Nikto reported information exposed through the ChangeLog response,
including ETag-related information.

Risk:

Version and file metadata may help attackers fingerprint the installed
software.

Recommendation:

Restrict access to change logs and administrative documentation and
minimize unnecessary information disclosure.

Finding 17 — Apache mod_negotiation / MultiViews Enabled

Severity: Medium

Observed:

Apache mod_negotiation is enabled with MultiViews

Nikto also identified:

/index.php

Risk:

Content negotiation can make resource discovery and file-name
enumeration easier in some configurations.

Recommendation:

Disable MultiViews where it is not required and explicitly configure
the web application routes and resources.

Finding 18 — Apache Default File / README Exposed

Severity: Low

Nikto identified an Apache default/readme resource under the web
content.

Risk:

Default installation files can reveal software details and provide
unnecessary information about the server.

Recommendation:

Remove default files, sample content, documentation, and installation
artifacts that are not required.

Finding 19 — X-Frame-Options Configuration Issue

Severity: Low

Nikto reported:

X-Frame-Options header is deprecated

and noted that modern policies can use the frame-ancestors
directive through Content-Security-Policy.

Risk:

Weak or outdated framing protections can increase the risk of UI
redressing/clickjacking depending on the application.

Recommendation:

Use an appropriate Content-Security-Policy with a frame-ancestors
directive and apply framing controls based on the application's needs.

Finding 20 — X-Content-Type-Options Not Set

Severity: Low

Observed:

The X-Content-Type-Options header is not set.

Risk:

Browsers may perform MIME-type sniffing in some situations.

Recommendation:

Set:

X-Content-Type-Options: nosniff

where appropriate.

7. Severity Summary

The findings can be grouped for remediation priority as follows.

Severity	Example Findings
High	Outdated Apache, outdated PHP, exposed phpinfo.php, exposed phpMyAdmin
Medium	Directory indexing, active TRACE, missing CSP, MultiViews, PHP Easter Eggs
Low	Missing security headers, technology disclosure, default files, metadata disclosure
Informational	Scan observations and configuration details without direct exploit evidence

The severity ratings above are an analyst assessment based on the
observed configuration and the potential security impact.

8. Important Note About Nikto Findings

Nikto is a web-server security scanner and many of its findings are
configuration issues, information disclosures, or indicators that
require manual validation.

A Nikto finding should not automatically be treated as a confirmed
exploitable vulnerability.

The complete raw output is preserved in:

nikto_scan_results.txt

The scan reported:

8235 requests
0 errors
31 items reported
1 host tested
9. HTTPS / SSL Check

The OASIS task requires an SSL-specific scan when the target supports
HTTPS.

HTTPS availability was checked using:

curl -k -I https://192.168.56.101

The result was:

curl: (7) Failed to connect

Therefore, HTTPS was not available on the tested target and an
SSL-specific Nikto scan was not performed.

10. Nikto Limitations

Nikto is useful for identifying many common web-server security
problems, but it has limitations.

Noisy Scanner

Nikto performs many HTTP requests to test web-server behavior,
files, configurations, and known issues.

Because of this, its activity can generate a large number of web-server
log entries and may trigger monitoring or intrusion-detection alerts.

For this reason, Nikto is considered a relatively noisy scanner.

False Positives

Some results require manual validation.

For example, a missing header is not necessarily a critical
vulnerability by itself.

Limited Application Understanding

Nikto focuses primarily on the web server and exposed web content.
It does not replace a full manual web-application penetration test.

Version-Based Findings

An old software version can indicate risk, but the exact installed
configuration and patch level should be confirmed before declaring a
specific vulnerability.

11. Nikto vs Nmap
Feature	Nikto	Nmap
Main purpose	Web-server security scanning	Network and service discovery
Primary focus	HTTP/HTTPS web services	Hosts, ports, services, and network behavior
Port discovery	Limited / secondary	Major capability
Web-server checks	Extensive	More limited
Service version detection	Web-focused	Broad service detection
Vulnerability-oriented web checks	Yes	Available through scripts, but not Nikto's specialty
Typical use	Web-server assessment	Network reconnaissance and service enumeration

Nmap is generally used to discover hosts, open ports, and services,
while Nikto specializes in checking web servers and web-accessible
resources for known security-related issues.

12. Recommendations

Based on the scan results, the following remediation priorities are
recommended:

Upgrade the outdated Apache web server.
Upgrade the outdated PHP installation.
Remove or restrict phpMyAdmin.
Remove exposed phpinfo and diagnostic scripts.
Disable unnecessary HTTP TRACE functionality.
Disable directory indexing on unnecessary directories.
Remove default, test, sample, and documentation files that should
not be publicly accessible.
Review and disable Apache MultiViews where unnecessary.
Implement appropriate HTTP security headers.
Reduce unnecessary technology and version information disclosure.
Review all exposed administrative and development resources.
Re-scan after remediation to verify that findings have been
addressed.
13. Evidence

The following screenshots document the Nikto scan:

screenshots/
├── 01-nikto-scan-1.png
├── 02-nikto-scan-2.png


The complete raw scan result is stored in:

nikto_scan_results.txt
14. Project Structure
SecurityAnalyst-Intermediate-Task7-Nikto/
│
├── README.md
├── nikto_scan_results.txt
└── screenshots/
    ├── 01-nikto-scan-1.png
    ├── 02-nikto-scan-2.png
    
15. Ethical Considerations

All testing was performed against a locally controlled,
intentionally vulnerable security-training environment.

The target was:

192.168.56.101

No external or unauthorized production systems were scanned.

Security scanning should only be performed on systems for which
explicit authorization has been provided.

16. Conclusion

Nikto was successfully used to scan the local web server at
192.168.56.101.

The scan identified 31 reported items after 8235 HTTP requests and
completed with zero reported errors.

The major security concerns included outdated Apache and PHP versions,
exposed phpinfo and phpMyAdmin resources, directory indexing, active
HTTP TRACE, Apache configuration issues, and several missing security
headers.

The assessment demonstrates that automated web-server scanning can
quickly identify configuration weaknesses and exposed resources.

However, Nikto findings should be manually validated before being
treated as confirmed vulnerabilities.

After remediation, the target should be scanned again to verify that
the identified security issues have been resolved.

Disclaimer :-

This project was performed solely for authorized educational and
security-training purposes in a controlled local laboratory.

Do not run Nikto or other vulnerability scanners against systems
without explicit authorization.