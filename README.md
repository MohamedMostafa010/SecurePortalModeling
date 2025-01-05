# University Financial System Threat Modeling and Security Testing

## Project Description:
- You are working with the cybersecurity team in a software company specializing in building customized software systems tailored to clients' needs. Your role involves conducting security testing and threat modeling for software products throughout the Software Development Lifecycle (SDL), ensuring the production of secure systems.

- Your company has received a request from a university in your city to reimplement its financial system with the following requirements:
  - **Web-Based Portal for Students:**
    - The new portal allows students to access the university's financial system.
    - Students can view their current balance, payment history, set up payment accounts, make one-time payments, and configure automatic payments.
  - **Existing Financial System:**
    - The university already has a financial system with a frontend web interface and backend database hosted in its data center.
    - University staff/users access the system either via internal workstations or through a secure web portal over a VPN.
    - **Security features include:**
      - Encrypted internal network traffic and database records.
      - Authentication via Active Directory (AD) and authorization managed by AD Security Group Policy Objects (GPOs).
  - **Student Access:**
    - Students will connect to the web portal over HTTPS without requiring a VPN.
    - Authentication is managed by a separate Student AD Domain Controller located in the DMZ, validating student credentials and granting access based on Security Group membership.
- **IT System Management:**
  - Staff workstations are automatically patched and updated by the IT department.
  - Remote systems connecting to the web portal must meet the following requirements (Validated by a NAC System):
    - Current OS, security software with automatic updates, and the latest version of a supported web browser.
      
- Your team has been tasked with conducting threat modeling for the university's overall financial system to identify security vulnerabilities, recommend mitigations, and ensure secure implementation of the new web-based portal. The project includes:
  - Building a Data Flow Diagram (DFD) to visualize data flow within the system and identify attack surfaces.
  - Constructing an attack tree, verified against the MITRE ATT&CK framework, to map potential threats and their mitigation.
  - Generating a detailed threat list to document vulnerabilities and propose security controls.
    
- This project demonstrates how secure development practices, combined with effective threat modeling, can ensure the protection of sensitive financial data in a university environment.

## Purpose of the Project:
- The purpose of this project is to identify and analyze potential security threats to a systemthrough a structured approach to threat modeling. The project aims to:
  - Understand and document the system's architecture using a Data Flow Diagram (DFD).
  - Identify and categorize possible security threats using the Microsoft Threat Modeling Tool (MTM).
  - Review generated threats and propose mitigation strategies.
  - Explore specific attack scenarios through the creation of an attack tree.
- By doing so, the project seeks to improve the system's security posture and provide actionable recommendations to minimize vulnerabilities.

## Focus on Threat Modeling:
- In this project, the authentication process using Kerberos was a primary focus of our threat modeling efforts (as shown in the DFD). Given the criticality of securely managing access to the university’s financial system, we analyzed Kerberos-based authentication in depth. While we considered other system components, many processes were summarized under the broader category of “Grant or Access to a Service or Application Server.” However, the Kerberos authentication process received special attention to ensure its robustness against potential threats.
- The DFD illustrates how data flows between various entities,such as user devices, the Authentication Server (AS), Ticket Granting Service (TGS), and application servers. This broad view ensures that all potential access scenarios are analyzed, identifying critical components, data flows, and potential vulnerabilities across different usage environments.
![Threat Modeling Image 0](/assets/threatmodelingimage0.png)
![Threat Modeling Image 1](/assets/threatmodelingimage1.png)
![Threat Modeling Image 2](/assets/threatmodelingimage2.png)

## Project Steps Made:
- **Data Flow Diagram (DFD):**
  - The initial DFD was created using an online tool to map data flow and identify system components and processes.
  - The DFD was then refined and finalized using Microsoft Threat Modeling Tool to improve visualization and alignment with industry standards.
- **Threat Identification and Mitigation:**
  - A total of 113 threats were identified during the threat modeling process.
  - We successfully mitigated 96 of the threats, achieving an 85% threat resolution rate, demonstrating the effectiveness of our mitigation strategies.
- **Attack Tree Development:**
  - A single threat was selected to construct an attack tree, which was verified against the MITRE ATT&CK framework.
  - The attack tree provided a clear, hierarchical representation of potential attack paths and their countermeasures.

## Microsoft Threat Modeling (MTM) Tool 2016 Features Used:
- **Automated Threat Analysis:** MTM scanned the imported DFD and generated a detailed threat list based on STRIDE categories (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege).
- **Mitigation Suggestions:** Leveraged MTM’s built-in mitigation suggestions to identify effective countermeasures for the listed threats, such as enforcing encrypted sessions and logging mechanisms.
- **Report Generation (Full and Custom Reports):** MTM offers a feature to generate detailed reports in full or custom formats.

## Identified Threats:
- During the analysis, the Microsoft Threat Modeling Tool 2016 (MTM) generated a detailed threat list based on the STRIDE framework (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, and Elevation of Privilege). we identified 113 threats in total, categorized under the STRIDE framework:
  - **Spoofing:** Risks related to impersonation and authentication.
  - **Tampering:** Concerns about data modification during transit.
  - **Repudiation:** Insufficient logging and user accountability.
  - **Information Disclosure:** Potential exposure of sensitive data.
  - **Denial of Service (DoS):** Service disruption through resource exhaustion.
  - **Elevation of Privilege:** Unauthorized access to high-level functionalities.
  ![Sample of Threats List](/assets/threatslistimage.png)
 
## Attack Tree:
- We have made an Attack Tree on the threat of ID number 246. Note that this attack tree is verified by the MITRE ATT&CK framework, I have utilized the MITRE ATT&CK framework extensively while constructing it to ensure accuracy and alignment with real-world tactics and techniques
![Attack Tree Image](/assets/attacktreeimage.png)
### Discussion of Attack Scenarios:
- Scenario 1:
  - **Vulnerability:** Misconfigured Database Network Services
  - A database service (e.g., MySQL, MongoDB) is exposed online with open ports and no proper rate-limiting, firewall rules, or IP filtering mechanisms. This misconfiguration allows unrestricted traffic from any source.
  - **Result:** Attackers can exploit this vulnerability to perform T1498.001 (Direct Network Flood) by sending a massive volume of requests to the exposed database.This overwhelms the database's resources (e.g., CPU, memory, or network bandwidth), causing service degradation or downtime, and preventing legitimate users from accessing the database.
- Scenario 2:
  - **Vulnerability:** Misconfigured Database or Log Aggregation Services
  - Log aggregation services(e.g., Elasticsearch, Fluentd, or Graylog)are publicly accessible without authentication or proper validation of incoming data.This makes the system vulnerable to attackers sending small requests that generate disproportionately large responses (amplified traffic).
  - **Result:** Attackers can exploit this vulnerability to perform T1498.002 (Reflection Amplification)by sending small queries to the log aggregation service that generate large responses.The amplified data is then redirected to the database or other targets, consuming all available resources and causing service disruption. This attack leverages the log aggregation service's capability to process and store extensive log data to overload other systems.
- Scenario 3:
  - **Vulnerability:** Insecure Database or Server Access
  - The database or its server is configured with weak authentication (e.g., default credentials, no multi-factor authentication) or improper access controls.This allows unauthorized users to gain direct access to compute resources.
  - **Result:** Attackers exploit this vulnerability to carry out T1496.001 (Compute Resource Hijacking)by using the database's CPU, memory, or storage to execute malicious tasks, such as running cryptojacking scripts to mine cryptocurrency.This depletes resources needed for legitimate operations, significantly degrading the database’s performance.
- Scenario 4:
  - **Vulnerability:** Exposed Database with High Log Traffic
  - A logging-enabled database is exposed online,accepting incoming traffic without restrictions or rate limits.Attackers can inject excessive log data (e.g., through fake requests or malformed payloads).
  - **Result:** Attackers utilize T1496.002 (Bandwidth Hijacking)by injecting excessive log data, consuming available bandwidth. This results in legitimate traffic being throttled or delayed, impacting the database's operational effectiveness.
 
## Challenges and Lessons Learned:
- **Balancing Simplicity and Detail:** One challenge was finding the right balance between providing enough detail in the DFD and keeping it simple enough for clear analysis. Including all potential access methods (VPN, internal workstations, etc.) added complexity to the modeling process.
- **Using the Microsoft Threat Modeling Tool (MTM):** Familiarizing ourselves with MTM 2016 and correctly importing the DFD took time. Learning how MTM categorizes threats and suggests mitigations was an iterative process, but it significantly enhanced our understanding of automated threat analysis.
- **Designing the Attack Tree:** Building the attack tree for Threat ID #246 was a new and challenging experience. Structuring the tree to cover all possible attack paths required careful thought and a clear understanding of the threat scenario.
