# SQL-Injection Detection and Analysis

#  Overview
This project demonstrates the design and implementation of a Security Operations Center (SOC) detection workflow focused on identifying and analyzing SQL Injection attacks in a controlled lab environment.  The lab simulates real-world attack scenarios using a vulnerable web application and integrates SIEM monitoring, alerting, and incident analysis

# Objectives:
	•	Detect SQL Injection attempts in real time
	•	Build a SIEM-based alerting mechanism
	•	Analyze attack patterns using logs
	•	Generate actionable alerts via email
	•	Simulate SOC analyst workflow from detection → response

# Components:                                         # Role
  * Kali Linux                     -->                  Attacker machine
  * DVWA (Damn Vulnerable Web App) -->                  Target web application
  * Splunk SIEM                    -->                  Log collection, analysis, alerting
  * Web Server Logs                -->                  Data source for detection
  * SMTP (Gmail)                   -->                  Alert notification system


# Tools & Technologies:
	•	Kali Linux
	•	DVWA
	•	Splunk Enterprise
	•	Apache / Web Logs
	•	SMTP (Gmail App Password)
	•	VirtualBox

# Attack Simulation:

  Apache2 runs the DVWA web app, handles HTTP requests, and logs all activity for Splunk to monitor.
  MySQL (MariaDB) stores the data and executes the SQL queries, including the injected ones during the attack.
  
  <img width="1600" height="742" alt="SOC lab1" src="https://github.com/user-attachments/assets/a34ecd67-4beb-4d90-b77e-e1c862dd4d7a" />

  <img width="1600" height="742" alt="SOC lab2" src="https://github.com/user-attachments/assets/1d295945-c864-43d7-b56f-38a62f5f7d3b" />

 # SQL Injection attacks were performed on DVWA using payloads such as:
	•	' OR 1=1--
	•	' UNION SELECT user, password FROM users-- 
	•	ORDER BY enumeration techniques

 <img width="1600" height="742" alt="SOC lab5" src="https://github.com/user-attachments/assets/a4d3c849-8937-4c32-9e02-e727c9d52b5a" />

 <img width="1600" height="742" alt="SOC lab8" src="https://github.com/user-attachments/assets/fc894018-58cb-40f4-9888-9becf9b63d12" />

# Attack Goals:
  •	Enumerate table structure
  •	Bypass authentication
  •	Extract database information

# Detection (Splunk)

 <img width="1600" height="742" alt="SOC lab3" src="https://github.com/user-attachments/assets/60da412b-a927-4d16-b348-6ef0b79337e3" />

 <img width="1600" height="742" alt="SOC lab4" src="https://github.com/user-attachments/assets/0bb4531e-cb53-4729-a56d-515837f768a8" />

# Detection Strategy:
	•	Keyword-based detection of SQL payloads: (index=* ("UNION SELECT" OR "OR 1=1" OR "ORDER BY" OR "SELECT" OR "FROM"))

  <img width="1600" height="742" alt="SOC lab11" src="https://github.com/user-attachments/assets/edaceb87-9b2b-49e4-8059-4b25de8ad241" />

	•	Identification of suspicious query patterns
	•	Grouping by IP and request

 <img width="1600" height="742" alt="SOC lab14" src="https://github.com/user-attachments/assets/139f3862-05ba-48fa-9e35-a9d0bde166e9" />

 <img width="1600" height="742" alt="SOC lab9" src="https://github.com/user-attachments/assets/913bf27c-3618-4fcf-a8ef-f9ffa0ebf8fd" />

 <img width="1600" height="742" alt="SOC lab10" src="https://github.com/user-attachments/assets/14808d8c-3314-4ea0-84bd-66133e7668ea" />

# Alert Configuration:
**Alert Settings**:
	•	Type: Real-time
	•	Trigger: Per-result
	•	Throttle: Optional (to avoid alert flooding)
	•	Condition: When SQL injection pattern is detected

 <img width="1600" height="742" alt="SOC lab15" src="https://github.com/user-attachments/assets/212d8d36-4eb9-4c32-9690-4d92c19c74ab" />

 <img width="1600" height="742" alt="SOC lab17" src="https://github.com/user-attachments/assets/1a33bf02-54aa-41a9-989e-63907b97aaa6" />

 <img width="1600" height="742" alt="SOC lab16" src="https://github.com/user-attachments/assets/4e1c53a1-2a87-45ee-bb7d-1a1db3ffb3eb" />

# Mitigation Recommendations
	•	Use prepared statements / parameterized queries
	•	Implement input validation & sanitization
	•	Deploy Web Application Firewall (WAF)
	•	Enable logging and monitoring
	•	Apply least privilege database access

# Future Improvements
	•	Add machine learning anomaly detection
	•	Integrate SOAR automation
	•	Build dashboard visualizations
	•	Expand to other attacks (XSS, RCE, LFI)
	•	Integrate threat intelligence feeds
  
# Author's Note: 
This project successfully demonstrates a full SOC workflow, from attack simulation to detection and alerting. It highlights the importance of SIEM tools in identifying web-based attacks and reinforces practical skills required of a cybersecurity analyst.
