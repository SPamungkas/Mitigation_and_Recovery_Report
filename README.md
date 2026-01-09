# Mitigation_and_Recovery_Report
This project involved a comprehensive security assessment of OWASP Juice Shop, a modern web application designed with intentional security flaws. The testing focused specifically on high-traffic entry points the Search Bar and the Login Form. 

# About Me
Information Systems graduate, currently transitioning to Cyber Security. Previously served as a Technician at Oil and Gas Industry (Pertamina Patra Niaga vendor), where I developed a highly disciplined approach to managing critical infrastructure compliance and 24/7 reliability. Currently formalizing expertise through an intensive cybersecurity bootcamp at Dibimbing, I am eager to apply this technical foundation and structured approach to a security operations role.

# Note
This report was prepared as part of a security research project to demonstrate proficiency in web application penetration testing and vulnerability remediation.

# Executive Summary
The OWASP Juice Shop web application was found to contain critical security vulnerabilities during this assessment. The audit focused on core functionalities where user input directly interacts with the backend database and the frontend rendering engine.

The assessment first identified a SQL Injection vulnerability on the Login Page. This flaw allows an attacker to manipulate the authentication logic, leading to Vertical Privilege Escalation. By exploiting this, an unauthorized user can gain full access to the Admin account, resulting in severe system compromise. To remediate this, it is recommended to implement prepared statements with parameterized queries, enforce strict input validation, and use properly configured stored procedures.

Additionally, a Cross-Site Scripting (XSS) vulnerability was discovered. This flaw enables attackers to exfiltrate sensitive user data, such as session cookies and personal information. Beyond the technical impact, a successful XSS attack poses a significant reputational risk, potentially damaging client trust if their data is compromised. This can be mitigated by avoiding dangerous JavaScript sinks, applying context sensitive encoding, utilizing HTML sanitization, and tightening input validation protocols.

# Key Vulnerability Matrix 
Based on the penetration testing conducted on OWASP Juice Shop, two primary vulnerabilities were identified SQL Injection and DOM-based XSS.

To ensure the security of the application and its users, it is highly recommended that remediation efforts follow a Risk-Based Approach, prioritizing high-impact vulnerabilities first.

<div align="center">
  
| Vulnerability | CVSS 3.1 | Severity | Vector String |
| :--- | :---: | :--- | :--- |
| SQL Injection | **8.7** | 🔴 High | `(CVSS:3.1/AV:N/AC:L/PR:H/UI:N/S:C/C:H/I:H/A:N)` |
| DOM XSS | **5.3** | 🟠 Medium | `(CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N)` |

</div>

# Detailed Finding

1. SQL Injection on Login Form
-   CVSS: High (CVSS:3.1/AV:N/AC:L/PR:H/UI:N/S:C/C:H/I:H/A:N))
-   Description: A critical SQL Injection (SQLi) vulnerability was identified within the Login Form of the application. The application's backend fails to properly sanitize the email input field before incorporating it into a dynamic database query. An attacker can leverage this flaw by injecting malicious SQL commands to manipulate the query logic.
-   Host Affected: https://demo.owasp-juice.shop/#/login
-   Endpoint Affected: 1. /login parameter: -
-   POC: Input a SQL query into the login page; use the payload ' OR TRUE-- for the email field and any arbitrary value for the password. As a result, the administrator account is successfully accessed.
  <p align="center">
  <img width="500" height="247" alt="image" src="https://github.com/user-attachments/assets/70fd9c9f-2896-41fc-81d2-d1fbe26b33e2" />
  <br>
</p>

- Reccomendation: Implement Prepared Statements with Parameterized Queries, Enforce Strict Input Validation, Utilize Properly Configured Stored Procedures.

2. XSS (DOM)
-    CVSS: Medium (CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N)
-    Description: The attacker identified a DOM-based XSS vulnerability within the application. This flaw allows an attacker to inject malicious JavaScript into the client-side code, which can lead to the unauthorized exfiltration of sensitive information, such as session cookies and other personal user data.
-    Host Affected: https://demo.owasp-juice.shop/#/
-    Endpoint Affected: 1. /search parameter: q
-    POC: By injecting the payload <iframe src="javascript:alert('xss')"> into the q search parameter, it was observed that the application fails to sanitize the input. The DOM subsequently renders and executes the script, confirming the vulnerability to DOM-based XSS.
  <p align="center">
  <img width="500" height="246" alt="image" src="https://github.com/user-attachments/assets/9473fb83-25fb-4ac5-9705-c7e32584e551" />
  <br>
</p>

- Reccomendation: Avoid the Use of Dangerous Sink Functions, Implement Context-Sensitive Output Encoding, Utilize Robust HTML Sanitization, Tighten Input Validation Protocols.

# Conclusion
Based on the findings of the penetration testing assessment, the following resources and guidelines are provided as references for remediating and securing the web application.
- DOM based XSS Prevention - OWASP Cheat Sheet Series
- SQL Injection Prevention - OWASP Cheat Sheet Series
