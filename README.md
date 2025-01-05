# University Financial System Threat Modeling and Security Testing

## Project Description:
- You are working with the cybersecurity team in a software company specializing in building customized software systems tailored to clients' needs. Your role involves conducting security testing and threat modeling for software products throughout the Software Development Lifecycle (SDL), ensuring the production of secure systems.

- Your company has received a request from a university in your city to reimplement its financial system with the following requirements:
  - Web-Based Portal for Students:
    - The new portal allows students to access the university's financial system.
      - Students can view their current balance, payment history, set up payment accounts, make one-time payments, and configure automatic payments.
  - Existing Financial System:
    - The university already has a financial system with a frontend web interface and backend database hosted in its data center.
    - University staff/users access the system either via internal workstations or through a secure web portal over a VPN.
    - Security features include:
      - Encrypted internal network traffic and database records.
      - Authentication via Active Directory (AD) and authorization managed by AD Security Group Policy Objects (GPOs).
  - Student Access:
    - Students will connect to the web portal over HTTPS without requiring a VPN.
    - Authentication is managed by a separate Student AD Domain Controller located in the DMZ, validating student credentials and granting access based on Security Group membership.
- IT System Management:
  - Staff workstations are automatically patched and updated by the IT department.
  - Remote systems connecting to the web portal must meet the following requirements:
    - Current OS, security software with automatic updates, and the latest version of a supported web browser.
      
- Your team has been tasked with conducting threat modeling for the university's overall financial system to identify security vulnerabilities, recommend mitigations, and ensure secure implementation of the new web-based portal. The project includes:
  - Building a Data Flow Diagram (DFD) to visualize data flow within the system and identify attack surfaces.
  - Constructing an attack tree, verified against the MITRE ATT&CK framework, to map potential threats and their mitigation.
  - Generating a detailed threat list to document vulnerabilities and propose security controls.
    
- This project demonstrates how secure development practices, combined with effective threat modeling, can ensure the protection of sensitive financial data in a university environment.

## Focus on Threat Modeling:
- In this project, the authentication process using Kerberos was a primary focus of our threat modeling efforts. Given the criticality of securely managing access to the university’s financial system, we analyzed Kerberos-based authentication in depth. While we considered other system components, many processes were summarized under the broader category of “Grant or Access to a Service or Application Server.” However, the Kerberos authentication process received special attention to ensure its robustness against potential threats.

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
