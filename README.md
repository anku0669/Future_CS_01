Vulnerability Assessment Report — AltoroMutual (demo.testfire.net)

Internship: Future Interns Cyber Security Internship 2026 — Task 1
Prepared by: Ankush Bhadwar
Date: 14 March 2026
Report Status: Final
Classification: Confidential (For educational use only)

1. Target Overview
Application Name: AltoroMutual
Target URL: https://demo.testfire.net
Host / IP Address: 65.61.137.117
Application Type: AltoroJ — intentionally vulnerable banking application
Developed By: HCL Technologies Ltd.
Technology Stack: Java (JSP), Apache Tomcat (Apache-Coyote/1.1), ISO-8859-1

Description:
AltoroMutual is a deliberately insecure web application designed for cybersecurity training and tool evaluation. The purpose of this assessment is to identify and document security weaknesses under controlled, ethical, and read-only conditions.

2. Scope of Assessment
2.1 In-Scope (Passive Testing Only)

The assessment strictly focused on publicly accessible endpoints using passive analysis techniques:

Homepage
Login Page (/login.jsp)
Feedback Form (/feedback.jsp)
Search Functionality (/search.jsp)
Server Status Page (/status_check.jsp)
Swagger UI (/swagger/index.html)
CGI Endpoint (/cgi.exe)

Additional Discovery:

Sensitive file identified: /admin/clients.xls (via OWASP ZAP spider crawl across 234 URLs)
2.2 Out-of-Scope Activities

The following activities were explicitly excluded:

Authentication bypass or credential-based attacks
Active exploitation of vulnerabilities (e.g., SQL Injection execution)
Access to authenticated dashboards or restricted areas
Denial-of-Service (DoS) testing
Third-party services (e.g., Swagger external integrations)

⚠️ Note: All testing adhered strictly to passive, non-intrusive methodologies. No exploitation or service disruption was performed.

3. Methodology and Tools

The assessment was conducted using a combination of automated tools and manual inspection techniques:

Tool	Purpose
OWASP ZAP 2.17.0 (Checkmarx)	Passive vulnerability scanning (11 alerts), spider crawl (234 URLs)
PTK	HTTP header and response analysis (16 findings, 10 unique)
Nmap 7.98	Network scanning and service enumeration
Browser Developer Tools (Chrome)	Header inspection, cookie analysis, DOM review
Wappalyzer	Technology stack identification
Shodan	External reconnaissance and host intelligence
Manual Review	Source code inspection and parameter analysis
4. Findings Summary
4.1 Severity Distribution
Severity Level	Count
🔴 High	4
🟠 Medium	4
🟡 Low	4
ℹ️ Informational	3
Total	15
4.2 High-Risk Vulnerabilities
ID	Vulnerability
V-01	Reflected Cross-Site Scripting (XSS)
V-02	SQL Injection (Potential)
V-03	Absence of Anti-CSRF Tokens
V-04	Exposure of Sensitive File (/admin/clients.xls)
4.3 Medium-Risk Vulnerabilities
ID	Vulnerability
V-05	Missing Content Security Policy (CSP) Header
V-06	Missing Anti-Clickjacking Protection (X-Frame-Options)
V-07	Absence of Subresource Integrity (SRI)
V-08	Server Banner Information Disclosure
4.4 Low-Risk Vulnerabilities
ID	Vulnerability
V-09	Session Cookie Missing SameSite Attribute
V-10	Inclusion of Cross-Domain JavaScript Resources
V-11	Missing X-Content-Type-Options Header
V-12	Missing Referrer-Policy Header
4.5 Informational Findings
ID	Observation
V-13	Publicly Accessible Swagger UI Without Authentication
V-14	Information Disclosure via HTML Comments
V-15	Session Token Identified in Application
5. Conclusion

The assessment identified multiple security misconfigurations and potential vulnerabilities across different severity levels. While the application is intentionally vulnerable for training purposes, the findings reflect real-world security risks commonly observed in production environments.

Key concerns include:

Input validation weaknesses (XSS, SQL Injection)
Lack of security headers
Exposure of sensitive resources
Inadequate session and request protection mechanisms
6. Recommendations (High-Level)
Implement robust input validation and output encoding
Enforce secure coding practices to mitigate injection attacks
Introduce CSRF protection mechanisms
Restrict access to sensitive files and directories
Configure essential HTTP security headers (CSP, HSTS, X-Frame-Options, etc.)
Improve session management policies