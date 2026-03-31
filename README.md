\# Browser Download Control Using Group Policy



> This project simulates a real-world enterprise security control used to prevent malware infections and data breaches.



\---



\## Overview



This project demonstrates how to prevent users from downloading file downloads from web browsers (including email attachments) using \*\*Group Policy\*\* in a Windows domain environment.



The objective is to replicate a real-world enterprise security scenario where organizations restrict file downloads to reduce the risk of \*\*malware infections, phishing attacks, and data exfiltration\*\*.



\---



\## Lab Environment



\* \*\*Domain\*\*: saada.local

\* \*\*Domain Controller\*\*: Windows Server (Active Directory)

\* \*\*Client Machine\*\*: Windows 10 (domain-joined)

\* \*\*Browser\*\*: Google Chrome



\---



\## Technologies Used



\* Active Directory Domain Services (AD DS)

\* Group Policy Management Console (GPMC)

\* Google Chrome Enterprise Policies (ADMX Templates)



\---



\## 🧭 Architecture Diagram



This lab simulates a domain-controlled environment where user actions are centrally managed using Group Policy.



!\[Lab Diagram](architecture/lab-diagram.png)



\### Flow



1\. User logs into a domain-joined Windows 10 machine  

2\. Opens Google Chrome browser  

3\. Accesses web-based email (e.g., Gmail / Outlook)  

4\. Attempts to download an email attachment  

5\. Group Policy enforces download restriction  



\---



\## Scenario



\### Before Policy Implementation



\* User can access email via browser  

\* Attachments can be downloaded without restriction  

\* Files are saved locally on the machine  



📸 See screenshots in: `/before-policy/`



\### After Policy Implementation



\* User attempts to download attachment  

\* Download is blocked by Group Policy  

\* Browser enforces enterprise security restriction  



📸 See screenshots in: `/after-policy/`



\---



\## 🔧 Implementation Steps (GUI-Based)



\### 1. Install Chrome ADMX Templates



\* Download Chrome ADMX Templates

&#x20; 1. Open Google Chrome on your Domain Controller

&#x20; 2. Go to: https://www.google.com/chrome/business/

&#x20; 3. Click: “Chrome Enterprise download”

&#x20; 4. Download: Chrome Enterprise Bundle (ZIP)



&#x20; Extract the Files

&#x20; 1. Right-click the downloaded .zip

&#x20; 2. Click Extract All

&#x20;    You’ll see a folder like: googlechromeenterprisebundle64



&#x20; Locate ADMX Files

&#x20; 1. Go inside:

&#x20;     Configuration/

&#x20;  └── admx/

&#x20;         Inside you’ll find:



&#x20;         chrome.admx

&#x20;         google.admx

&#x20;         Language folder (e.g., en-US)

&#x20;     

\* Copy files chrome.admx, google.admx and Paste into: `C:\\Windows\\PolicyDefinitions`



Copy Language Files 

&#x20;Open: admx\\en-US\\

&#x20;Copy chrome.adml, google.adml and Paste into: 'C:\\Windows\\PolicyDefinitions\\en-US'

&#x20; 



\### 2. Create a Group Policy Object (GPO)



\* Open \*\*Group Policy Management Console\*\*  

\* Right-click domain → \*\*Create GPO\*\*  

\* Name: `Block Email Attachments`



\### 3. Configure Chrome Download Restrictions



Navigate to:



User Configuration → Policies → Administrative Templates → Google → Google Chrome  



Enable:



\* \*\*Download Restrictions\*\* → Set to \*\*Block all downloads\*\*



\### 4. Apply Additional Security Settings (Optional)



\* Prevent users from bypassing Safe Browsing warnings  

\* Disable changing download directory



\### 5. Link GPO



\* Link the GPO to the domain or specific Organizational Unit (OU)



\### 6. Apply Policy



\* Restart client machine OR  

\* Log off and log back in  



\---



\## 📸 Screenshots



\### Before Policy



\* User login  

\* Email access  

\* Attachment download successful



\### GPO Configuration



\* GPO creation  

\* Policy configuration  

\* Chrome policy settings



\### After Policy



\* Download blocked  

\* Error message displayed  

\* Policy enforcement confirmed



\---


### Additional Security Validation

- User-initiated downloads from websites are blocked  
- Download attempts from external sources fail  
- Demonstrates protection beyond email attachments  

📸 Examples:
- `/after-policy/normal-download-blocked.png`  
- `/after-policy/drive-by-blocked.png`

\---



\## Security Impact



\* Prevents malware downloads  

\* Reduces phishing attack risk  

\* Enforces organizational security policies  

\* Demonstrates centralized IT control  



\---


### Protection Against Drive-By Downloads

By blocking all downloads at the browser level, this policy also reduces the risk of drive-by download attacks.

Drive-by downloads occur when a user visits a malicious or compromised website that attempts to download files without the user's full awareness.

While modern browsers require user interaction for most downloads, this control ensures that:

- Any attempted download is completely blocked  
- Users cannot accidentally download malicious files  
- Malware delivery via compromised websites is prevented  

This extends protection beyond email security to general web browsing.

\---



\## 🔐 Compliance \& Data Loss Prevention (DLP) Impact



\### Why This Matters



Data Loss Prevention (DLP) is about preventing sensitive information from leaving your organization without authorization. This project demonstrates how a single GPO configuration enforces DLP controls:



\#### 1. Prevents Unauthorized File Transfers



| Scenario | Without DLP (Before) | With DLP (After) |

|----------|--------------------|----------------|

| Employee receives confidential financial report via email | Downloads to personal device → Can forward, copy to USB, upload to personal cloud | BLOCKED - Cannot download in first place |

| HR receives resume with SSNs and personal data | Downloads attachment → Data now on local machine, vulnerable to theft | BLOCKED - Data stays in email server, properly secured |

| Executive receives M\&A confidential documents | Downloads to laptop → If laptop stolen, documents compromised | BLOCKED - Documents never leave secure email environment |



\#### 2. Real-World DLP Controls Your GPO Enforces



| GPO Configuration | DLP Control Achieved |

|------------------|--------------------|

| Block all downloads | Data cannot leave secure email environment |

| Disable download directory | Users can't redirect to unprotected locations |

| Safe browsing enforcement | Prevents bypassing security warnings |



\---



\### 🔗 Compliance Framework Mapping



| Framework | Control | How Your GPO Addresses It |

|----------|--------|--------------------------|

| \*\*ISO 27001\*\* | A.8.2 - User Endpoint Devices | Enforces security on Windows 10 endpoints across the domain |

| \*\*ISO 27001\*\* | A.8.7 - Protection from Malware | Blocks email attachments to prevent malware delivery |

| \*\*ISO 27001\*\* | A.13.2 - Information Transfer | Prevents unauthorized data transfer through email downloads |

| \*\*ISO 27001\*\* | A.12.6 - Technical Vulnerability Management | Centralized policy ensures consistent security |

| \*\*NIST 800-53\*\* | PR.AC-3 / PR.DS-5 / PR.IP-1 | Access control, leakage protection, baseline security across endpoints |

| \*\*HIPAA\*\* | 164.312(a)(1), 164.312(e)(1), 164.308(a)(5) | Controls access and transmission of PHI, enforces security awareness |

| \*\*GDPR\*\* | Article 32 / Article 25 / Article 5(1)(f) | Technical measures secure personal data and maintain integrity |

| \*\*PCI DSS\*\* | Requirement 6 - Secure Systems | Enforces consistent endpoint security configuration |



\---



\### GDPR (European Privacy Law) Compliance



My Group Policy implementation aligns with key GDPR principles by enforcing \*\*technical data protection controls\*\* at the endpoint level.



| GDPR Article | Control Goal | How Your GPO Meets It |

|-------------|--------------|----------------------|

| \*\*Article 32 – Security of Processing\*\* | Ensure personal data is processed securely, with appropriate technical and organizational measures | Blocks email attachment downloads, preventing sensitive data from being saved to local or unsecured devices. Reduces risk of unauthorized access, malware infection, or accidental data leaks. |

| \*\*Article 25 – Data Protection by Design and by Default\*\* | Embed data protection into system design and default configurations | The GPO automatically applies to all domain-joined users. Users cannot bypass the control, ensuring protection is enforced by default. |

| \*\*Article 5(1)(f) – Integrity and Confidentiality\*\* | Maintain data integrity and confidentiality, protecting against unauthorized or accidental loss | Attachments never leave the secure email environment, ensuring personal data remains confidential and protected from compromise. |



\*\*Key Takeaways:\*\*  

\* Email attachments containing sensitive information (e.g., financial data, HR documents, medical records) \*\*cannot be downloaded\*\*, mitigating risks of data breaches.  

\* The policy enforces GDPR principles \*\*without requiring user intervention\*\*, demonstrating both preventive and systemic data protection.  

\* This is a \*\*real-world example of a technical control\*\* directly supporting GDPR compliance in an enterprise environment.



\### Real-World Business Scenarios



\*\*Financial Services:\*\*  

\- Problem: Bank employees receiving SSNs  

\- Solution: GPO blocks attachments, ensuring secure email handling  

\- Compliance: GLBA  



\*\*Government Agency:\*\*  

\- Problem: Classified documents emailed internally  

\- Solution: Centralized GPO prevents downloads  

\- Compliance: FISMA  



\*\*Healthcare Organization:\*\*  

\- Problem: PHI emailed between departments  

\- Solution: Blocked downloads keep PHI in secure email  

\- Compliance: HIPAA  



\---



\### Business Impact Metrics



\*\*Before Implementation:\*\*



\* Users could download any attachment anywhere  

\* No control over storage of sensitive data  

\* 100% risk exposure to email malware  



\*\*After Implementation:\*\*



\* Centralized control on all endpoints  

\* Data protected at source (cannot leave email)  

\* Policy applied organization-wide in minutes  



\*\*Cost Savings Example:\*\*  



Organization with 1,000 employees:



\* Without GPO: $50/user for security training = $50,000  

\* With GPO: Enforced policy = $0/user = $0  



Real-World References:



IBM Cost of a Data Breach Report 2024 - Average breach cost $4.45M

Verizon DBIR 2024 - 94% of malware delivered via email

Gartner - "DLP is a critical control for compliance"



\---



\### Audit-Ready Documentation



\* ✅ \*\*Policy Configuration Evidence\*\* – Screenshots of GPO settings  

\* ✅ \*\*Implementation Verification\*\* – RSoP showing applied policies  

\* ✅ \*\*Effectiveness Testing\*\* – Before/after demonstration  

\* ✅ \*\*Centralized Management\*\* – One policy for all endpoints  



\---



\## Real-World Use Case



Attackers commonly use email attachments to deliver malware, ransomware, or phishing content. Enterprises enforce GPOs to:



\* Reduce ransomware attacks  

\* Prevent sensitive data leaks  

\* Centralize IT security policy enforcement  



\---



\## Security Principles Demonstrated



\* Least Privilege Access  

\* Defense in Depth  

\* Centralized Policy Enforcement  

\* Endpoint Hardening  



\---



\## Key Learning Outcomes



\* Hands-on experience with Active Directory  

\* Group Policy configuration and deployment  

\* Browser-level security enforcement  

\* Enterprise security best practices  



\---



\## Future Improvements



\* Implement USB storage blocking via GPO  

\* Integrate SIEM monitoring (e.g., Splunk)  

\* Add application whitelisting (AppLocker)  

\* Simulate malware delivery before/after control  



\---



\## Author



\*\*Abdirahman Ali\*\*  



\* GitHub: https://github.com/abdira  

\* LinkedIn: https://www.linkedin.com/in/abdirahman-ali-5b8a2b3b4/  



\---



\## ⭐ Project Value



This project showcases practical, real-world IT and cybersecurity skills aligned with enterprise environments, making it highly relevant for:



\* Scholarship applications  

\* Entry-level IT roles  

\* Cybersecurity (Blue Team) positions  

