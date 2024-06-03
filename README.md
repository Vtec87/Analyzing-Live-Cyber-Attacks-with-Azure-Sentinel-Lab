


---

# Threat Hunting with Azure Sentinel Lab
**By Victor Patterson Sr**

## Technical Summary: Analyzing Live Cyber Attacks with Azure Sentinel Lab

**In a Nutshell:**

Imagine having a cyber radar that not only detects but also visualizes real-time cyber threats globally. This is precisely what I explored in this lab using Azure Sentinel, a superhero among security tools. Here’s how I made the digital world visible:

### How I Did It:
1. **Set the Stage:**
   - I created a virtual decoy (a honeypot) to attract cyber villains, luring them into a virtual trap.

2. **Spy on the Invaders:**
   - Azure Sentinel acted as my digital detective, collecting and analyzing attack logs in real-time, particularly focusing on suspicious attempts to breach our virtual fortress via Remote Desktop Protocol (RDP).

3. **Live Action Monitoring:**
   - Picture a live dashboard displaying incoming threats – that’s what Azure Sentinel offered. Instantly, I could see and respond to ongoing cyber skirmishes.

4. **Geolocation Magic:**
   - I wrote a script using PowerShell to reveal the physical locations of these digital invaders. Imagine a world map with pinpointed cyber-attack origins – it’s like cyber forensics.

5. **Visualizing the Battle:**
   - The coolest part: I turned all this data into a dynamic map. Attacks were not just numbers; they were dots on a global map, showing their patterns and origins.

### My Cyber Arsenal:
- **Azure Sentinel:** The Cyber Sentry
- **Azure Virtual Machines:** The Virtual Battlefield
- **PowerShell:** The Cyber Wizard’s Spell Book
- **Geolocation API:** The Digital GPS

### The Impact:
- I created a cyber monitoring system that is not just effective but visually stunning.
- Caught live cyber villains attempting RDP break-ins from all corners of the digital globe.
- Visualized the cyber battlefield globally, making cyber threats tangible.

### Why It Matters:
In a world where cyber threats are often unseen, having this kind of cyber vision is a game-changer. Azure Sentinel isn't just a tool; it's a cyber superhero that empowers security teams to see, understand, and act against evolving threats in real-time.

## Lab Presentation Steps:

### Introduction:
Ever wondered what it's like to see cyber threats in action and track them globally? In this lab, I will take you through a thrilling journey where we expose a virtual decoy, track live cyber-attacks, and visualize their global reach using Azure Sentinel and PowerShell. Get ready for a digital adventure that showcases the power of cybersecurity tools in action!

### Steps:
1. **Azure Subscription and VM:**
   - (Already Completed) If you’ve got an Azure subscription and portal access, we’re good to go. ![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/7116f9a3-833d-4321-9187-96c9545a61fc)
1.	Azure Subscription and VM:
o	- (Already Completed) If you've got an Azure subscription and portal access, we're good to go.  
o	**VM Configuration: ** I'll kick off by setting up a virtual machine (VM), intentionally tweaking its security settings to create a controlled environment for educational purposes. ![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/6a667073-0001-4a44-88bd-2750cad644c1)

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/eaf39909-1b01-4948-ac60-68c8b6ce2d7a)

1. Creating the VM with Intentional Security Vulnerabilities:
Setup: I will initiate the setup of a virtual machine with intentional security vulnerabilities.
Resource Group: The specifically assigned resource group for this lab is identified as HoneypotlabV.
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/43efd9f5-aa39-4607-9951-ae471d161180) 
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/bc619dfe-3409-4e7c-8e91-b232b7907517)
2. Administrative Account Setup for Lab Purposes:
Simplified Credentials for Lab Administration:

Username: vtechadmin
Password: Create your own secure password (e.g., Password####).
Configuration Details:

Disabled External Firewall: This exposes the VM to internet traffic, deliberately attracting potential attacks.
Temporarily Halted Windows Firewall: I've disabled the Windows firewall temporarily to observe raw attack attempts.
Important Note: This setup is exclusively for educational purposes and should never be replicated in a real-world scenario. As part of the VM creation, I've also established a new firewall by navigating to advanced settings under the NIC network security group.
3. Firewall Configuration for Enhanced Lab Security:
Removing Default Rule: First, I've removed the default rule (1000
) since it's a default setting.
Creating a New Inbound Rule: I'll be crafting a new inbound rule with broader allowances into the VM:
Destination Port: Set as a wildcard (*) for any protocol.
Action: Allow
Priority: Assigned a low priority value of 100.
Name: Distinctively labeled as SMOOTH_CRIMINAL_l.
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/6768dff6-1434-424b-8f4f-c005df0e06e7)
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/9e1426ee-d560-4a02-a22a-6181c141578f)
4. Broad Inbound Rule Configuration:
Priority: Set to 100 to ensure the rule takes precedence.
Gateway Opening: As a result of this adjustment, the VM is now open to all traffic from the internet, creating an entry point for potential cyberattacks.
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/41b6db26-606c-4a74-a898-cadd4a691312)
5. Successful Configuration:
Confirmation: Confirmed that the setup was executed correctly, deliberately exposing the VM to the public internet. After that, I clicked review & create.
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/a44258c3-d28d-4b9f-9244-f75402e2c862)
Final Step: I then reviewed the configuration settings and clicked "Create" to finalize the setup.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/36b57937-1381-4823-bd56-8f2f09d55467)

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/040c78a0-2d3e-47d9-b16c-0852b504f7f7)

## Log Analytics Workspace and Azure Sentinel Setup

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/cf1fe46c-d913-4eff-9ff4-2ea18fe385d9)

### Log Analytics Workspace:
- **Establishment:** I've set up a dedicated workspace to store logs originating from the VM.
  - **Objective:** To ingest essential Windows event logs for comprehensive analysis.

### Custom Log Creation:
- **Personalized Log:** I've created a custom log that includes geographic information, providing insights into the origins of potential attackers.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/040ac775-7398-4e92-a2b6-9d4a6dc21e81)

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/1c56a31c-18c1-4f23-a27a-9608759b7b4c)

## Microsoft Defender for Cloud Lab Steps

### Step 1: Azure Defender for Cloud Enrollment and Data Aggregation for Sentinel
- **Access Microsoft Defender for Cloud:** Start by navigating to Microsoft Defender for Cloud through the Azure Portal.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/2da7a120-8db6-4d4e-bc53-c1afa5283a70)



## Provisioning Plans:

1. **Subscription and Resource Group Selection:** 
   - Start by choosing the relevant subscription and resource group for the enrollment process.

2. **Plan Selection:** 
   - Opt for both the "Foundational CSPM" and "Servers" plans. These plans provide crucial security and compliance monitoring for your Azure resources, including your servers, such as HoneyPot-VM.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/80d01267-24ff-4264-94db-37a2512f102a)

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/39585636-ce01-4752-9d59-be5e89835584)

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/02df6b10-9d60-417b-8d5b-3679398c1414)

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/0b332263-d997-446f-a074-b5e8b170a8ea)

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/081ed156-2a81-46b4-9ad1-4413adcf59d3)

- **Select Plans:** Choose both the "Foundational CSPM" and "Servers" plans.
- **Save:** Click "Save" to apply the selected plans.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/40320751-7fbd-4b86-9d08-a076056c5ae7)


- **Select "All Events":** Choose "All Events" and click "Save".
- **Navigate Back:** Return to the Log Analytics workspace.
- **Select Honeypot VM:** Choose your honeypot VM from the list.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/2e65a739-8bc0-4642-9a19-f5feff2fc50e)

- **View Log Analytics:** Your Log Analytics workspace will now display data similar to the example below:

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/9b6a3e76-79ae-4e11-99c3-eb33adc0a4cd)

## Step 2: Log Analytics Workspace and Azure Sentinel Integration

1. **Log Analytics Workspace Creation:**
   - I established a Log Analytics workspace to serve as a centralized hub for storing VM logs.

2. **Selection of VM:**
   - Within the Log Analytics workspace interface, I navigated to the left-hand side of the screen and selected the designated VM.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/c517a44b-b752-4e8d-ab8f-a303fbd1eea8)


### 3. VM Selection:
- **Targeted Honeypot VM:** I specifically chose the Honeypot VM to ensure seamless integration with the Log Analytics workspace. This focused selection facilitates precise data aggregation for enhanced monitoring and analysis.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/882681cb-b6b7-4829-9ff0-be4bd13b3c31)

### 4. Connector Activation:
- **Ensuring Data Flow**: After selecting the Honeypot VM, I proactively activated the connector within the Log Analytics workspace. This critical step ensured secure and efficient data flow from the VM to the Sentinel environment, enabling comprehensive threat analysis.
•	**5. Sentinel Installation:**
•	   - *Search and Activate:* To enhance the capabilities of Azure Sentinel, I initiated the installation process directly from the Azure Portal. By searching for Sentinel and seamlessly installing it, I ensured that the Honeypot VM contributes to the overarching security framework. 

### 5. Sentinel Installation:
- **Search and Activate**: To enhance Azure Sentinel's capabilities, I initiated the installation process directly from the Azure Portal. By searching for Sentinel and seamlessly installing it, I ensured that the Honeypot VM integrates effectively into the overarching security framework.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/94bb3a1d-d401-4521-8c14-a341b439c4e7)

### 6. Workspace Selection:
- **Tailored Integration**: During the installation of Azure Sentinel, I strategically selected a specific Log Analytics workspace. This deliberate choice ensures seamless system integration with the designated workspace, streamlining data management and optimizing analysis capabilities.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/607ea5a5-efe6-432d-9cd9-4061a681d3ba)

### 7. Dynamic IP Capture:
- **Proactive IP Retrieval**: Recognizing the importance of real-time tracking, I navigated back to the VM during the installation phase. By effectively capturing the dynamic IP address (20.163.31.144), I ensured accurate alignment between the virtual environment and Azure Sentinel, facilitating precise geolocation analysis in subsequent steps.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/3f3d2bc9-f899-41d2-8d20-27155a7244d8)

### 8. Remote Desktop Connection:
- **Seamless VM Access**: Using the dynamic IP address (20.163.31.144), I initiated a Remote Desktop Connection from my home computer. This step ensures direct access to the VM, facilitating the simulation of cyberattacks and allowing for real-time monitoring via Azure Sentinel.

- ![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/22ca456d-3288-44a7-87c3-a64d8dc286eb)
- Accept the Certificate Warning:
After accepting you should have access to your desktop

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/feab49d4-4b52-418f-b446-1f1791503269)

### 9. Initial VM Configuration:
- **Advertisement and Features Management**: Upon the VM loading, I proactively declined all advertisements and features. This strategic move helps maintain a focused and secure environment for the simulation, eliminating potential distractions and enhancing the accuracy of attack tracking through Azure Sentinel.


  ![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/ce33e9ee-5674-4933-9c88-7cb7850cd853)

### 10. Active Remote Desktop Connection:
- **Successful Connection**: The Remote Desktop connection to the VM has been successfully established and is currently operational. This key step enables real-time monitoring and analysis of the simulated cyberattacks through the Azure Sentinel platform.

  ![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/03d09e8d-b908-4170-be7e-08ade7ef963f)

### 11. Log Analysis and Browser Setup:
- **Browser Installation**: Following the VM setup, I installed Microsoft Edge to facilitate comprehensive log analysis and web-based investigations. This step is crucial for visualizing attack patterns and identifying potential vulnerabilities.
- **Event Viewer Navigation**: I accessed the Event Viewer from the Start menu, specifically focusing on the "Security" logs under Windows Logs. This detailed log analysis provides insights into potential security breaches and helps understand the nature of cyber threats targeting the VM.

- ![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/a9f9b072-4060-49af-a4a4-02455495a81e)
- **12. Security Event Analysis (Event ID: 4625):**
- *Event Selection:* Within the Security Events displayed, I honed in on Event ID 4625, which signifies failed login attempts. This targeted focus allows for the identification and analysis of multiple login failures, particularly those related to Remote Desktop Protocol (RDP).
- *Double-Click for Details:* To delve deeper, I double-clicked on Event ID 4625, unveiling specific details about each failed login attempt. This granular information includes the username, source IP address, and additional contextual data critical for understanding the nature of the attack.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/ce328c60-1e22-43dd-bc8c-0ad81bdfd24a)

### 13. Simulating a Failed Login Attempt:
- **Purpose**: Since the Security Event Analysis revealed no existing failed login attempts, I simulated one for the purpose of this lab.
- **Creation of Failed Attempt**: Through intentional misconfiguration, I attempted a login with incorrect credentials. This simulated scenario triggered Event ID 4625, demonstrating the system's responsiveness to potential security threats.
- **Demonstration of Detection**: By expanding the newly created failed attempt event, I illustrated how Azure Sentinel promptly captures and logs such incidents. This live demonstration emphasizes the platform's efficacy in real-time threat detection and analysis monitoring.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/f0b3bc49-6fcd-4dbf-86dd-6e3113f54930)

### 14. Confirming Failed Login Attempt:
- **Verification**: To confirm the simulated failed login attempt was successfully recorded, I remotely attempted to log in to the VM a second time from my home desktop, deliberately entering an incorrect password.
- **Outcome**: The Security Event Logs, particularly Event ID 4625, promptly registered this intentional failed attempt. This confirms the effectiveness of Azure Sentinel in capturing and documenting security incidents in real-time.
- **Significance**: This step highlights the platform's reliability and responsiveness to unauthorized access attempts, emphasizing its critical role in strengthening cybersecurity defenses.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/0bd4a21f-76b3-4ed7-9188-8a29d53e1ad8)

### 15. Leveraging Failed Attempt Data:
- **Data Utilization**: The recorded failed login attempt, originating from Source Network Address 76.84.135.36, will be analyzed within Azure Sentinel.
- **Purpose**: This intentional use case demonstrates the platform's capability to process and analyze security incidents, empowering cybersecurity professionals to track and respond to potential threats effectively.
- **Learning Opportunity**: By showcasing the handling of a simulated incident, this step underscores the practical application of Azure Sentinel in identifying and addressing security vulnerabilities proactively.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/2c01d074-47a9-4020-86cf-8583acbabc75)


### 16. IP Geolocation Analysis:
- **Utilizing PowerShell**: I programmatically extracted geolocation data for the IP address 76.84.135.36.
- **Tool Integration**: Leveraging the IP Geolocation API (https://ipgeolocation.io/), I obtained precise coordinates corresponding to the identified IP address.
- **Practical Application**: This step demonstrates the automation capability of PowerShell in obtaining real-time geographic information, showcasing the integration of external tools for comprehensive threat intelligence.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/79600737-bb26-4c02-aadf-a2a3a750ab32)

### 17. Custom Log Creation and Log Analytics:
- **Firewall Configuration**: To enable log transmission, I temporarily disabled the firewall on my VM using the "wf.msc" command.
- **Custom Log Generation**: I created a customized log containing detailed geolocation information obtained from the IP Geolocation API.
- **Log Transmission**: The custom log was sent to the Log Analytics Workspace in Azure for centralized storage and analysis.

This step underscores the importance of data preparation for analysis and highlights the versatility of Azure services in handling diverse log formats.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/b790c287-de26-44dd-a897-b3344402ffe3)

### 18. Network Connectivity Testing:
- **Disabling Windows Defender Firewall**: I accessed the Windows Defender Firewall settings to temporarily disable it, allowing network connectivity.
- **Command Line Testing**: Using the command prompt on my main laptop, I initiated a continuous ping (Ping 76.84.135.36 -t) to the target IP address (76.84.135.36).

This step demonstrates the practical aspect of testing network connectivity post-configuration, ensuring seamless communication for further analysis.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/087078f3-e989-4ae9-b958-f85488dc7e39)


### 19. Firewall Deactivation:
- **Firewall Settings in VM**: I accessed the Windows Defender Firewall settings within the VM and turned off the firewall.
- **Ensuring Open Communication**: Deactivating the firewall is a crucial step to enable data flow between the VM and external resources for the next stages of the lab.

This action demonstrates the deliberate disabling of the firewall to allow unrestricted communication, providing a hands-on experience in managing security configurations. To access the firewall settings, I typed “wf.msc” and clicked “Windows Defender Firewall Properties”.
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/4215d2bb-2960-4e8c-ad4c-6ee7017664c4)
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/48dbb1dc-c2e3-42f1-9479-8934f6426c0f)

### 20. Firewall Deactivation (Continued):
- **Disabling Firewall Across Profiles**: I turned off the Firewall State in all three profiles - Domain, Private, and Public - to ensure comprehensive deactivation across different network scenarios.
- **Complete Firewall Inactivity**: With the firewall turned off in all profiles, the VM now allows unrestricted communication without any filtering based on network types.

This step is crucial to create an environment where external connections are not restricted, facilitating the exploration of cyber attacks and subsequent analysis.
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/9630aafa-d59b-4961-977b-dfc172000bcc)


Turning off the firewall for the Private Profile involves accessing the Windows Defender Firewall settings and disabling it specifically for the Private network profile.

1. **Access Windows Defender Firewall Settings**: Open the Windows Defender Firewall settings.
2. **Navigate to Profile Settings**: Find the option to manage firewall settings for different network profiles.
3. **Turn Off Firewall for Private Profile**: Locate the Private network profile and disable the firewall for this profile.
4. **Confirm Changes**: Save the settings to apply the changes.

By turning off the firewall for the Private Profile, you allow unrestricted communication for devices connected to private networks, ensuring seamless data flow within that network environment.
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/758e51c5-bf2b-41b5-bb21-b4fc2ab7b47a)
To turn off the firewall for the Public Profile, follow these simplified steps:

1. **Access Windows Defender Firewall Settings**: Open the Windows Defender Firewall settings.
2. **Navigate to Profile Settings**: Look for the option to manage firewall settings for different network profiles.
3. **Disable Firewall for Public Profile**: Locate the Public network profile and disable the firewall for this profile.
4. **Confirm Changes**: Save the settings to apply the changes.

Disabling the firewall for the Public Profile allows unrestricted communication for devices connected to public networks, ensuring seamless data flow within that network environment.
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/da391324-63eb-4e83-8acc-b6d476d0a29a)


### 22. Enabling Microsoft Defender for Cloud Data Collection:
- **Ignored SQL Server Plan:** I omitted the activation of the SQL Server plan since there are no SQL servers in the environment.
- **Activation of Selected Plans:** I activated the "Foundational CSPM" and "Servers" plans to initiate the collection of crucial data for security monitoring.
- **Azure Sentinel Setup:** I utilized the search bar to access Azure Sentinel, configuring the necessary settings.

#### Benefits:
- Gain comprehensive visibility into the security posture of the Azure environment.
- Securely collect and aggregate data from the HoneyPot-VM, including log data and security events.
- Prepare data for seamless ingestion and analysis within Azure Sentinel.

### 23. Connecting HoneyPot-VM to Microsoft Defender for Data Collection:
- **Locate HoneyPot-VM:** I navigated to the Azure Portal, found the HoneyPot-VM, and accessed the "Security" section.
- **Data Connector Addition:** I went to "Data connectors" and selected "Add data connector," choosing "Azure Defender for Cloud."
- **Configuration:** I followed on-screen instructions to configure the connection, providing necessary authorization credentials and specifying data sources.
- **Verification:** I ensured the connection status was verified, confirming active data collection.

#### Benefits:
- Establish a secure and reliable data flow from the HoneyPot-VM to Microsoft Defender for Cloud.
- Ensure collection of all relevant security events and logs from the VM for comprehensive analysis.
- Lay the groundwork for advanced threat detection and incident response capabilities in Azure Sentinel.

#### Noteworthy Points:
- SQL Server plan not activated due to the absence of SQL servers in the environment.
- Enabling Foundational CSPM and Servers plans covers basic security monitoring needs.
- Consider expanding data collection based on specific security requirements and desired threat detection capabilities.

### 24. Verification of Data Collection:
- **Connection Status Confirmation:** Prior to advancing to the next lab steps, I verified the connection status to ensure proper and functional data collection.

#### Key Emphasis:
- Ensured the integrity of the data flow from the HoneyPot-VM to Microsoft Defender for Cloud.
- Confirmed the active status of data collection to guarantee the availability of essential security events and logs.

#### Next Steps:
- With successful verification, proceed confidently to subsequent lab activities for a comprehensive exploration of Azure Sentinel's capabilities.

### 25. PowerShell Script Development:
- **Objective:** I crafted a PowerShell script with the aim of extracting attacker IP addresses from Windows logs for further analysis and visualization in Azure Sentinel.

#### Script Components:
- Utilized PowerShell's capabilities to navigate and extract relevant information from Windows event logs.
- Focused on retrieving IP addresses associated with detected attacks.

#### Benefits:
- Enhances the ability to identify and track potential threat actors through their IP addresses.
- Sets the stage for visualizing the geographic distribution of cyber attacks in Azure Sentinel.

#### Note to Consider:
- Ensured the script aligns with the specific log data collected from the HoneyPot-VM.
- Prepared the groundwork for the subsequent steps involving geolocation analysis and attack visualization.

#### Next Steps:
- Execute the PowerShell script as part of the overall strategy to gain insights into the global reach of cyber attacks. Proceed to the subsequent phases of the lab for a comprehensive exploration of Azure Sentinel's visualization capabilities.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/d8954a7c-8e41-40f8-81dc-5bd27d4c27c3)

### 2. PowerShell ISE Usage:
   - **Objective:** Opened PowerShell ISE on the VM to create a new script, facilitating a more efficient and organized script development environment.

### Procedure:
   1. Launched PowerShell ISE from the VM environment.
   2. Created a new script file to accommodate the upcoming PowerShell script development.

### Benefits:
Here's a revised version:

### 28. PowerShell ISE Usage:
   - **Objective:** Opened PowerShell ISE on the VM to create a new script, facilitating a more efficient and organized script development environment.

### Procedure:
   1. Launched PowerShell ISE from the VM environment.
   2. Created a new script file to accommodate the upcoming PowerShell script development.

### Benefits:
   - PowerShell ISE provides an integrated scripting environment with features like syntax highlighting, tab completion, and debugging tools, enhancing the scripting experience.
   - Starting a new script file ensures a clean slate for developing the PowerShell script focused on extracting attacker IP addresses.

### Note to Include in Documentation:
   - Emphasize the utilization of PowerShell ISE for script development, highlighting its advantages in terms of functionality and user-friendly features. This step demonstrates a deliberate choice in selecting tools for efficient task execution within the lab environment.
   - 
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/6e86e509-450c-4ae7-8dec-f29e70a4b0d4)
pasted my scripted.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/90a77e95-e83c-454e-9130-48da34494c8a)

**2. Developing and Running the PowerShell Script:**

   - **Objective:** Explain the process of creating and executing a PowerShell script for continuous monitoring of failed login attempts.

**Procedure:**

1. **Save Script to Desktop:**
   - Save the PowerShell script file as "LogExporter.ps1" on the Desktop for easy access and execution.

2. **Running the Script:**
   - Open PowerShell ISE on the VM and create a new script.

3. **Script Content:**
   - Copy the provided script content into the new script file.

4. **Save and Execute:**
   - Save the script and execute it. The script operates continuously, monitoring the Event Viewer for failed login attempts.

5. **Loop Functionality:**
   - The script uses a loop to iteratively check the Event Viewer for logs related to failed login attempts.

6. **Hidden Folder Note:**
   - If you have trouble locating the "C:\ProgramData" folder due to its hidden status, manually navigate to the folder.

**Note:**
   - The perpetual loop ensures ongoing monitoring of security events, specifically focusing on detecting failed login attempts. Placing the script on the Desktop makes it easily accessible for ongoing threat analysis.
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/6c4c030a-2a90-4a93-a2e7-854407c43450)



**Locating the Hidden Folder and Creating Default Log File:**

To locate the hidden folder and create a default log file for training the Log Analytics Workspace, follow these steps:

1. **Navigate to the Hidden Folder:**
   - Use the "Start" menu and select "Run" or press `Win + R`.
   - Type `C:\ProgramData\` and press Enter.
   - If the folder is not visible, manually navigate to the location.

2. **Run Command:**
   - In the "Run" dialog, enter the command:
     ```
     C:\ProgramData\$($LOGFILE_NAME)
     ```
   - This command is designed to access the specified log file.

3. **Auto-Creation of Default Log File:**
   - If the log file is not present, the script will automatically create a default log file.
   - This log file includes sample records that will be utilized later to train the Log Analytics Workspace for parsing our custom log.

**Note:**
- This step ensures the availability of a log file, facilitating the initial setup and training process for the Log Analytics Workspace. The default log file contains sample records crucial for configuring the workspace to parse and analyze custom logs effectively.

- ![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/96ef8317-3289-4832-97db-86c02e21d4d1)


**Script Execution and Output:**

While the script is running, it provides information on non-failed login attempts, which you might notice with purple highlighting in the output.

**Note:**
- The purple highlighting indicates failed login attempts, making it easy to distinguish them from successful ones.
  
This distinction is crucial for identifying and extracting relevant information from the logs, particularly focusing on security events and potential cyber threats.
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/f09018c9-b4da-404b-9182-514785684099)

---

**Script Execution and Output:**

While the script is running, it provides information on non-failed login attempts, which you might notice with purple highlighting in the output.

**Note:**
- The purple highlighting indicates failed login attempts, making it easy to distinguish them from successful ones.
  
This distinction is crucial for identifying and extracting relevant information from the logs, particularly focusing on security events and potential cyber threats.
Your instructions are clear and straightforward. Here's a refined version:

---

**Acquiring IP Geolocation API Key:**

In the next step, within the VM operating system, navigate to [https://ipgeolocation.io/](https://ipgeolocation.io/) and create an account to obtain the necessary API Key.

This API Key is essential for programmatically retrieving geolocation information based on IP addresses, enhancing the capabilities of the lab in mapping and visualizing the global reach of cyberattacks.
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/66f35917-02f3-4f5f-94aa-36b7ad6850d4)


**Integration with Third-Party Geo-location API:**

After acquiring the API Key, proceed to integrate the PowerShell script with a third-party geo-location API, such as IP2Location.

**Enriched Log Data:**

Upon execution, the script will systematically dispatch the extracted IP addresses to the geo-location API. In return, the API will provide additional enriched information, including latitude/longitude coordinates, city/state details, and other pertinent geographical data associated with each identified IP address.

This integration enhances the depth of log data, facilitating a more comprehensive analysis of the geographical origins of cyberattacks. The enriched data will be instrumental in plotting and visualizing the global reach of these attacks using Azure Sentinel.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/c32e7efe-eb55-400f-bd17-c667bd873263)
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/459c21d2-d97a-4826-a6d0-0523f1e8ba56)

**Creating Custom Log Name: FAILED_RDP_WITH_GEO**

During the custom log creation process, I named the custom log "FAILED_RDP_WITH_GEO" to accurately reflect the enriched nature of the log data. This name succinctly communicates the focus of the log, which includes geographical information derived from the integration with a third-party API.

This naming convention serves as a clear identifier for the custom log within the Log Analytics workspace. It highlights the specific context of the log, emphasizing its significance in tracking failed RDP attempts with enriched geographical details. This strategic naming ensures quick recognition and easy access for further analysis, enhancing the overall efficiency and effectiveness of security monitoring. 

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/23f74305-7206-4bd0-9afa-159721badff4)


**Demo: Verifying Log Integration**

To ensure the VM and Log Analytics synchronize effectively for log collection, I conducted a demonstration showcasing the verification process. This demo provided a comprehensive overview of the steps involved in verifying log integration.

1. **Navigating to Log Analytics Workspace:**
   - Opened the Azure portal.
   - Navigated to the Log Analytics workspaces.

2. **Accessing Custom Log Wizard:**
   - Located and selected the "Tables" section within the Log Analytics workspace.

3. **Creating a New Custom Log (MMA-based):**
   - Clicked on "Create" and selected "New custom log (MMA-based)."
   - Defined the custom log table by specifying the log file to be collected and set criteria for the log file.

4. **Defining Log Record Properties:**
   - Specified the fields to be extracted from the log file, ensuring that geographical information is included.

5. **Saving the Custom Log Definition:**
   - Saved the custom log definition, completing the setup for the log with enriched geographical data.

This demonstration provided a visual walkthrough of the essential steps to create and configure the custom log within the Azure portal. It highlighted the meticulous process of defining log properties and criteria for effective log collection, emphasizing the importance of including enriched geographical data for comprehensive analysis.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/f5070670-aa23-4ed7-ac2a-2c38775c63a1)

**Demo: Checking Security Events**

To ensure that security events are being captured and connected to the Azure Log Analytics workspace, I conducted a demonstration. This step is crucial in verifying the integration of security events from the VM to the Log Analytics workspace.

1. **Accessing Security Events:**
   - Typed "SecurityEvent" in the search bar and executed the command.

2. **Reviewing Windows Event Log:**
   - Examined the Windows event log from the VM within the Azure Log Analytics workspace.

3. **Connection Confirmation:**
   - Confirmed that the security events are successfully connecting to the Log Analytics workspace.

4. **Note: Deleting Unnecessary Elements**
   - Ensured that unnecessary elements, such as irrelevant lines, were removed to maintain a clean and accurate representation of security events.

This demonstration showcased the direct connection between the VM's security events and the Azure Log Analytics workspace. By reviewing the security event log, it confirmed that the integration process is functioning as expected, ensuring that all relevant security events are accurately captured and analyzed.
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/215d939b-37de-469d-a9dc-4615a89a7177)

**Querying Failed RDP Attempts with Geographical Information**

After allowing sufficient time for logs to accumulate, I executed a query to retrieve information from the custom log, "FAILED_RDP_WITH_GEO_CL." This log captures entries of failed Remote Desktop Protocol (RDP) attempts, enriched with geographical information.

### Steps:

1. **Run Query:**
   - Executed a query against "FAILED_RDP_WITH_GEO_CL."

2. **Results:**
   - Displayed the results of the query, showcasing various failed RDP attempts.

3. **Geographical Information:**
   - Highlighted entries with latitude and longitude details, providing a visual representation of the geographic locations associated with the failed RDP attempts.

### Summary:

This query presentation effectively demonstrates the success of the log collection and enrichment process. By incorporating geographical data into the log entries, it significantly enhances the visibility and analysis of failed RDP attempts on the VM. This enriched data not only provides insights into the frequency of such attempts but also their global distribution, which is crucial for comprehensive security monitoring and analysis.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/ff9125ca-ef26-45c4-a25d-ce2a29c3123a) 

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/dfe4d958-a9eb-482e-bb8a-d71353943e16)


**Field Extraction for Enhanced Analysis**

In the following steps, I extracted specific fields from the raw log data to enhance the analysis and visualization within Azure Sentinel.

### Steps:

1. **Expand Log Entry:**
   - Expanded a log entry within Azure Sentinel to view detailed information.

2. **Access Extraction Options:**
   - Clicked on the three dots (...) to reveal additional options.

3. **Select Extract Fields:**
   - Chose the "Extract fields" option to specify and extract relevant fields from the log entry.

### Summary:

These actions are crucial in the data preparation process, ensuring that essential information is extracted and made available for more focused and detailed analysis. This step enhances the ability to create precise visualizations and insights within Azure Sentinel, ultimately contributing to more effective security monitoring and threat detection.
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/3b66f814-7b41-4d26-832c-c3735a8aadb4)
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/58a653d6-c197-4321-b1f5-87a7633be4f5)
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/97dbc1dd-fbe0-40a3-8930-72d4cf637dcf)

**Azure Sentinel Threat Management Workbook Customization**

In the upcoming steps, I tailored the Azure Sentinel Threat Management Workbook for a more refined and targeted view of the security landscape.

### Steps:

1. **Access Threat Management Workbooks:**
   - Navigated to the Threat Management Workbooks section within Azure Sentinel.

2. **Initiate Workbook Creation:**
   - Clicked on "Create New" to start creating a new Threat Management Workbook.

3. **Enter Edit Mode:**
   - Switched to the editing mode of the workbook to apply customizations.

4. **Remove Unnecessary Widgets:**
   - Removed specific widgets from the right-hand side of the workbook to streamline the visual representation.

### Summary:

These actions were taken to streamline the visual representation of security data, providing a more focused and tailored view within the Threat Management Workbook. Customizing the workbook ensures that only the most relevant and critical information is displayed, enhancing the efficiency and effectiveness of threat management.
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/1edf81bd-ba1f-49dc-901f-0c89ae4219bb) ![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/025cb266-de9c-4029-ba48-76b2d5e5170b)
**Azure Sentinel Threat Management Workbook Customization**

In the upcoming steps, I tailored the Azure Sentinel Threat Management Workbook for a more refined and targeted view of the security landscape.

### Steps:

1. **Access Threat Management Workbooks:**
   - Navigated to the Threat Management Workbooks section within Azure Sentinel.

2. **Initiate Workbook Creation:**
   - Clicked on "Create New" to start creating a new Threat Management Workbook.

3. **Enter Edit Mode:**
   - Switched to the editing mode of the workbook to apply customizations.

4. **Remove Unnecessary Widgets:**
   - Removed specific widgets from the right-hand side of the workbook to streamline the visual representation.

5. **Add a New Query:**
   - Clicked "Add" and then selected "Add Query" to incorporate a new query into the workbook.

### Summary:

These actions were taken to streamline the visual representation of security data, providing a more focused and tailored view within the Threat Management Workbook. Customizing the workbook ensures that only the most relevant and critical information is displayed, enhancing the efficiency and effectiveness of threat management.
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/714a1510-cd31-4a79-89c6-e2dd3ca648d2)

Once I was in my new Workbook, I typed the following query to extract specific fields from the "FAILED_RDP_WITH_GEO_CL" log:

```kusto
| extend username = extract(@"username:([^,]+)", 1, RawData),
         timestamp = extract(@"timestamp:([^,]+)", 1, RawData),
         latitude = extract(@"latitude:([^,]+)", 1, RawData),
         longitude = extract(@"longitude:([^,]+)", 1, RawData),
         sourcehost = extract(@"sourcehost:([^,]+)", 1, RawData),
         state = extract(@"state:([^,]+)", 1, RawData),
         label = extract(@"label:([^,]+)", 1, RawData),
         destination = extract(@"destinationhost:([^,]+)", 1, RawData),
         country = extract(@"country:([^,]+)", 1, RawData)
| where destination != "samplehost"
| where sourcehost != ""
| summarize event_count=count() by latitude, longitude, sourcehost, label, destination, country
```

This query filters the log entries to exclude those with the destination host "samplehost" and ensures that the source host is not empty. Then, it summarizes the count of events by latitude, longitude, source host, label, destination, and country.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/d6b45e95-b7d5-4ed4-9deb-29cd2be64d7d)


**Azure Sentinel Threat Management Workbook Customization - Visual Data Representation**

Upon executing the query and customizing the Threat Management Workbook, the layout now offers a visually captivating and organized display of the extracted insights.

**Visual Enhancements:**
- We meticulously arranged the visual elements and widgets to ensure clarity and ease of interpretation.
- Each aspect of the data, including vital geo-location information, is presented in a visually engaging format.

**Key Benefits:**
- Improved readability and understanding of security-related data.
- The streamlined presentation enables rapid identification of potential threats and discernment of attack patterns.

Finally, to provide a real-time perspective of global threat landscapes, I integrated attack locations into an Azure Sentinel map.

![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/3bbb8a07-f21c-4b00-a216-4cb5369a7288)


**Live Cyber Attack Monitoring - Azure Sentinel**

**Workbook Title:** Failed RDP World Map

**Overview:**
- Introducing the "Failed RDP World Map," a meticulously crafted Threat Management Workbook tailored for real-time surveillance of cyber threats targeting your virtual environment.

**Key Features:**
1. **Real-time Visualization:** Immerse yourself in the pulse of cyber security with a visually immersive world map, dynamically illustrating ongoing attempts to breach your system via Remote Desktop Protocol (RDP).

2. **Global Reach Insights:** Gain profound insights into the worldwide landscape of cyber threats. Witness the spread of unauthorized access attempts across the globe, empowering you with a comprehensive understanding of potential vulnerabilities.

3. **Enhanced Situational Awareness:** Elevate your security posture with unparalleled situational awareness. Quickly identify, analyze, and respond to emerging threats, safeguarding your infrastructure with agility and precision.

**Benefits:**
- **Proactive Threat Detection:** Stay one step ahead of malicious actors with continuous, proactive monitoring. Detect and thwart potential threats in real time, mitigating risks before they escalate.
- **Instant Visualization:** Transform complex data into actionable insights at a glance. Instantly visualize attack patterns and their global origins, facilitating swift decision-making and response strategies.
- **Rapid Response Capabilities:** Equip your security teams with the tools they need to respond decisively to emerging threats. Streamline incident response processes and minimize potential damages with timely interventions.

This Threat Management Workbook isn't just a tool—it's your frontline defense in the ever-evolving landscape of cyber security. With the "Failed RDP World Map," you're empowered to anticipate, adapt, and overcome any challenge that comes your way.
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/42470cfb-2d97-43ad-86fe-757a0886e891)
![image](https://github.com/Vtec87/Analyzing-Live-Cyber-Attacks-with-Azure-Sentinel-Lab/assets/115051912/05cc7621-5a0a-43f1-92e3-35edc521c224)

**Lab Outcome/Key Learnings: Cyber Attack Analysis with Azure Sentinel**

**Achievements:**
1. **Deployment of a Vulnerable VM:**
   - Successfully deployed a virtual machine (VM) with deliberate security vulnerabilities to attract simulated cyber attacks.

2. **Azure Sentinel Configuration:**
   - Configured Azure Sentinel to ingest and analyze VM logs, enabling proactive detection and tracking of cyber attack attempts.

3. **PowerShell Script Development:**
   - Developed a PowerShell script to extract IP addresses from Windows logs, laying the groundwork for in-depth analysis.

4. **Geo-location Data Enrichment:**
   - Leveraged a geo-location API to enrich extracted IP addresses with precise geographic coordinates and additional contextual information.

5. **Interactive Azure Sentinel Map:**
   - Visualized attack locations on an interactive Azure Sentinel map, providing actionable insights into the global distribution of cyber threats.

**Conclusion:**
This lab underscores the robust capabilities of Azure Sentinel in cyber attack analysis. Through the integration of PowerShell scripting and geo-location data enrichment, it enables a comprehensive understanding of attack origins and patterns. Emphasizing the significance of advanced log analytics and visualization tools, it underscores their pivotal role in fortifying cybersecurity defenses.

**Technical Highlights:**
- Leveraged Azure Sentinel's advanced log analytics and visualization features for enhanced threat detection.
- Developed a PowerShell script to streamline log parsing and data extraction processes.
- Integrated seamlessly with a third-party geo-location API to augment data with precise geographical details.
- Employed custom log creation to optimize data organization and facilitate detailed analysis.

**Note:**
This lab serves as an educational resource and does not endorse real-world system exposure to cyber threats.

**By: Victor Patterson Sr.**
