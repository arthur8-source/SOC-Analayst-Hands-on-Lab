# SOC-Analayst-Hands on-Lab

# Advanced SOC Analyst Lab with LimaCharlie

## Introduction
Welcome to my Advanced SOC Analyst Lab, a hands-on cybersecurity project designed to simulate a Security Operations Center (SOC) environment using [LimaCharlie](https://limacharlie.io/), a free-tier Endpoint Detection and Response (EDR) and Security Information and Event Management (SIEM) platform. Inspired by the practical, execution-focused approach of the "So You Want to Be a SOC Analyst?" course ([link](https://ddi.sh/sywtbsa)), this project goes beyond theory to deliver a fully functional lab where I:
- Set up and running live attack simulations
- Use EDR solutions to detect adversary actions
- Building and testing custom detection & blocking rules
- Analyzing telemetry from real malware and C2 frameworks
 This repository serves as a portfolio piece to demonstrate my readiness for a SOC analyst role, highlighting skills in threat simulation, EDR configuration, rule engineering, and data analysis—all critical competencies sought by cybersecurity employers.

---

## Project Goals
- **Threat Simulation**: Replicate adversarial tactics (e.g., ransomware encryption, C2 beaconing) to understand attacker behavior.
- **Detection and Response**: Build and test precise detection rules and automated blocking actions in a live environment.
- **Telemetry Analysis**: Parse and visualize attack data to uncover patterns and validate response efficacy.
- **Professional Documentation**: Present the project in a clear, structured way suitable for technical review or interview discussions.

---

## Skills Showcased
- **Threat Simulation**: Crafted Python scripts to mimic ransomware and APT-style C2 persistence.
- **EDR Proficiency**: Configured LimaCharlie for real-time monitoring, detection, and response.
- **Rule Engineering**: Developed multi-condition YAML rules to catch subtle attack indicators while minimizing false positives.
- **Data Analysis**: Used Python to process JSON telemetry logs and generate an attack timeline graph.
- **Cloud Infrastructure**: Deployed and secured Ubuntu VMs on AWS Free Tier for attack-and-defend scenarios.
- **Technical Communication**: Documented setup, execution, and findings in a concise, employer-friendly format.

---

| Skill | Tool/Method |
|-------|-------------|
| Threat Simulation | Python, Cryptography |
| EDR Configuration | LimaCharlie |
| Rule Creation | YAML, Logical Operators |
| Telemetry Analysis | Matplotlib, JSON Parsing |
| Cloud Setup | AWS EC2, SSH |

---

#  Part 1: Setting Up the Environment

####  Virtualization Setup
To simulate a realistic network environment, I set up two virtual machines (VMs):
- **Windows VM**: For testing and simulating attacks.
- **Linux (Ubuntu) VM**: For running various security tools.

####  Setup a free LimaCharlie account
LimaCharlie is a powerful “SecOps Cloud Platform”. It not only comes with a cross-platform EDR agent, but also handles all of the log shipping/ingestion and has a threat detection engine.
[Click here to create a free LimaCharlie account](https://limacharlie.io/)  
- Once the org is created, click “Add Sensor”
- Select the Endpoint tab

- Select Windows

- Provide a description such as: Windows VM - Lab

- Click Create

- Select the Installation Key we just created
- Add Sensor
   ![Console](Screenshots/LimaCharlie_add_Sensor.png)
   Add Sensor
  
 ## Configure LimaCharlie to ingest Sysmon logs from our VM
- I configure LimaCharlie to also ship the Sysmon event logs alongside its own EDR telemetry
- LimaCharlie will now start shipping Sysmon logs which provide a wealth of EDR-like telemetry, some of which is redundant to LC’s own telemetry, but Sysmon is still a very power visibility tool that runs well alongside any EDR agent.
- Another reason i am ingesting Sysmon logs is that the built-in Sigma rules we are about to enable largely depend on Sysmon logs as that is what most of them were written for.

  ![Console](Screenshots/Sysmon_logs_Config.png)
    Sysmon Config

  
##  Enable Sigma EDR Ruleset
- Finally, let’s turn on the open source Sigma ruleset to assist our detection efforts.

![Console](Screenshots/Sigma_Ruleset.png)
  Sigma Ruleset

# Part 2: Adversary Simulation

In the second part of the series, I focused on simulating adversarial activities to understand how attackers operate and how to detect their actions effectively.

####  Command and Control (C2) Setup
To simulate real-world attacks, I set up a Command and Control (C2) server using Sliver, an open-source C2 framework. This involved generating a payload and deploying it on the Windows VM to establish a communication channel between the attacker (C2 server) and the victim (Windows VM).

####  Executing the Payload
I executed the generated payload on the Windows VM, which initiated a connection back to the C2 server. This setup allowed me to interact with the compromised system through the C2 framework, mimicking the actions of a real attacker.

   ![Console](Screenshots/Generate_C2_Implants.png)

## Drop our C2 implant on Windows and launch it
- a web server on the Linux VM which is serving up the location we saved our C2 implant in the previous step.
- Click on your implant name to download it to the Windows VM


## Open your new C2 Session

- In Edge, browse to http://<linux_vm_ip>:8080

- This is a web server on the Linux VM which is serving up the location we saved our C2 implant in the previous step.
- Click on your implant name to download it to the Windows VM
- Download your Sliver C2 implant from the Linux VM web server.

## Open your new C2 Session
 Switch back to Linux VM Sliver Client
- Within a few moments, your C2 implant should callback to your Sliver server
- Your new C2 session has arrived
- Verify your session in Sliver, taking note of the Session ID
-You are now interacting directly with the C2 session on the Windows VM. Let’s run a few basic commands to get our bearing on the victim host.


## Exploring EDR Telemetry
- Let’s hop into the LimaCharlie web UI and check out some basic features.
- Click your active Windows sensor 

- One of the easiest ways to spot unusual processes is to simply look for ones that are NOT signed

- My C2 implant shows as not signed, and is also active on the network.


  ![Console](Screenshots/Console.png)
  ![Console](Screenshots/Detecting_vss.png)
  ![Console](Screenshots/Detections.png)
  ![Console](Screenshots/shell.png)
  ![Console](Screenshots/Sigma_Ruleset.png)
  ![Console](Screenshots/Yara.single.png)
  ![Console](Screenshots/File_System.png)
 
  ![Console](Screenshots/Getsystem.png)
  ![Console](Screenshots/Hash.png)
  ![Console](Screenshots/Implants.png)
  ![Console](Screenshots/LSASS_Detection.png)

  ![Console](Screenshots/Network.png)
  ![Console](Screenshots/Network_Connections.png)
  ![Console](Screenshots/Process_Tree.png)
  ![Console](Screenshots/Processes.png)
  
  
  ![Console](Screenshots/VSS_Deletion_rules.png)
  ![Console](Screenshots/Virus_Total.png)
  ![Console](Screenshots/Whomai.png)
  ![Console](Screenshots/YARA_Detections2.png)
  ![Console](Screenshots/YARA_Detection_Memory.png)
  ![Console](Screenshots/sensor_endpoint.png)
  
  
