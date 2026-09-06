# Skills Assessment: Incident Handling

## Objective

This is a brief walkthrough of the skills assessment portion of the Incident Handling module in HTB SOC Analyst Path. In this walkthrough we will do some Alert triage and identify some key indicators of compromise (IOCs). Follow along to learn some key SOC skills.

### Skills Learned

- Alert triage.
- Indicators of Compromise.
- Virus Total.
- MITRE ATT&CK Framework mapping.
- Development of critical thinking and problem-solving skills in cybersecurity.
- Threat intel
- Log analysis

### Tools Used

- Security Information and Event Management (SIEM) [The HIVE]
- Virus Total
- MITRE ATT&CK

## Steps

First we will create a case in The Hive with both alerts related to Insight Nexus:
<img width="1081" height="408" alt="Insight nexus alerts" src="https://github.com/user-attachments/assets/ebc92078-e85d-402e-b110-babc694e607c" />
<img width="608" height="903" alt="casedetails" src="https://github.com/user-attachments/assets/c5ade7b6-28ed-448d-96c5-376c5ded76e5" />

Now we can begin investigating!

Question 1: 
Open the alert "[InsightNexus] Admin Login via ManageEngine Web Console." Find the foreign IP address starting with "203" in the comments. Check VirusTotal for the information related to this IP address, and add the details as a comment in this alert. In VirusTotal, what is the name of the file starting with "Mango" in the Files Referring section?

<img width="2407" height="956" alt="alert merge outbound ip203" src="https://github.com/user-attachments/assets/8edc001e-e27f-4a51-b9a2-ac6dc6158c87" />
Here we can see the foreign IP. [Be sure to add a note for each step taken in the comments section on The Hive]

Now head over to Virus Total - https://www.virustotal.com/gui/home/upload

<img width="1130" height="271" alt="Virus Detection" src="https://github.com/user-attachments/assets/b1301d0f-a050-4e0f-8f0e-5b35081d270b" />
Upon first glance we don't see anything obviously suspicious about the IP. However note the 10+ files embedding this IP address. From here we will go to the Relations tab and find Referred files.

<img width="873" height="386" alt="files reffering" src="https://github.com/user-attachments/assets/0d1b805e-dec4-482a-97d0-fc789ca08f2b" />
From here we can see multiple detections on referred files. We also can find the answer to our first question. 

Answer 1: MangoJava.exe

<img width="625" height="83" alt="c C" src="https://github.com/user-attachments/assets/3bab4b37-8066-4eb8-b06d-6fe83f598684" />

And of course don't forget your notes!

Question 2:
In VirusTotal, go to the details of the IP address starting with "198." What is the name of the city shown in the Whois Lookup?

Alright so first be sure to copy the IP address from the comments beginning with "198". Then paste it over into your search bar on Virus Total and move to the Details tab to find the Whois Lookup.


<img width="2480" height="807" alt="whoois" src="https://github.com/user-attachments/assets/4b4927d3-5a4a-4a51-91fe-830d66f73f87" />

Now that we have the details on the Whois lookup we can find the answer to question number 2.

Answer 2: Los Angeles

<img width="624" height="77" alt="whoiscity" src="https://github.com/user-attachments/assets/8b990371-b984-480c-84eb-9c9cc475b85d" />

Question 3:
If malware downloads files from a C2 (Command and Control) server into the victim network, under what MITRE technique ID does this tool transfer technique fall? Type it as your answer. The format is T1***.

So for this we will head over to the MITRE ATT&CK FRAMEWORK - https://attack.mitre.org/

<img width="180" height="698" alt="C Cmitre" src="https://github.com/user-attachments/assets/51343a7b-381a-45c3-b638-d8cae3b022e0" />

Under the Command and Control tab we find an entry title "Ingress Tool Transfer" This is our answer to question 3. Bonus points click on this C&C type and learn about it. Make notes in The HIVE.

Answer 3:T1105

<img width="622" height="93" alt="lateralC C" src="https://github.com/user-attachments/assets/c0a7c301-822d-44cb-bbd0-26874d786607" />


Question 4:
Open TheHive and check the rule ID 92153 related to the VaultCli.dll module. What is the MITRE technique ID for this activity? The format is T1***.

Back on The Hive we are going to filter for a specific Ruleid:
<img width="2414" height="294" alt="filters" src="https://github.com/user-attachments/assets/5033d6d4-c4fd-47ac-841f-5a9ce3c0f308" />

Now we have the right alert. We will go ahead and preview the alert:
<img width="1403" height="1007" alt="mitreid" src="https://github.com/user-attachments/assets/0a0fcd4d-23d5-4ad8-8305-8b4f5f4ce6b4" />

You will notice under the alert preview we can see that the alert actually gives us the MITRE ATT&CK id. It also show to associated tactic "Credential Access"

Answer 4: T1555


Question 5:
Download the "logs-wazuh.zip" file from resources, and identify the suspicious PowerShell command in the logs. Type the suspicious IP address after decoding the command.

Now we are going to download the log file and do some investigating! You can open the Log using Notepad.

<img width="1092" height="996" alt="powershell notepad" src="https://github.com/user-attachments/assets/39f72b1c-6d61-406d-97a8-1acee2039dc4" />


Step one we use find [ctrl + F] and look for Powershell. 

<img width="1093" height="85" alt="encoded command" src="https://github.com/user-attachments/assets/f998bf99-39e2-4cdb-8067-be43ac88b0b0" />

Then if we scroll down we can see the command. But it looks like it is Encoded with Base64. So we are going to have to decode the command in order to get our suspicious IP. Head on over to cyberchef and we can get this command decoded. cyberchef.org

<img width="2041" height="893" alt="decoded command" src="https://github.com/user-attachments/assets/c6938dc8-61f0-4ab2-a3ba-02f7eba4bc93" />

There we have our answer to question 5.

Answer 5: 198.51.100.24

Question 6:

In the same file (i.e., logs-wazuh.zip), identify the user who executed the suspicious PowerShell command. The format is domain\user.

Once again we will take a look at the Powershell execution, but this time we are going to home in on the User.

<img width="1071" height="112" alt="Screenshot 2026-09-06 024006" src="https://github.com/user-attachments/assets/ed8fb559-d1ff-4393-b9d4-c44cbead28ce" />


Right there below the encoded command from before we can find the user. Be sure to format your answer correctly on HTB. This one cannot just be copy/paste.

Answer 6: CORP\svc-update




Thank you for taking a look on this writeup on the skills assessment for Incident Handling on Hack the Box. In this LAB we got to investigate alerts using The Hive. We used some great tools such as Virus Total and Mitre Att&ck framework. We even got to do some log analysis. Hope you learned and enjoyed.


