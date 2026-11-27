# Building Active Directory Lab  

## Overview
This project is a brief walkthrough on how I established a virtualized Active Directory environment in VMWare Workstation, using a Windows Server 2022 domain controller to host my testlab.local domain and simulate a small enterprise network.

---

### What Skills Will Be Displayed
- Virtualization 
- Active Directory and identity access management
- Group Policy Management

---

### How the Lab Is Set Up


#### Step 0: Before Getting Started
Before I could build the Windows server and Active Directory environments, I first needed to meet a few prerequisites. In order to use Active Directory, I needed to have VMWare Workstation installed on my PC.

<img width="950" height="392" alt="0-01 workstation-install" src="https://github.com/user-attachments/assets/e2c8ad73-6e33-43b9-8fca-440988e5b8a2" />

---

I also would need to download the Windows Server ISO that would be used to establish the Windows server.

<img width="949" height="438" alt="0-02 server-ISO-download" src="https://github.com/user-attachments/assets/7c70b10e-e3e6-45bd-aed3-8d3140da7b4b" />


#### Step 1: Creating a New VM

<img width="1277" height="746" alt="1-01 creating-new-vm png" src="https://github.com/user-attachments/assets/e5a2ded9-4603-43d4-ae60-f69d6747f54d" />

<img width="1278" height="704" alt="1-02 select-VM-OS png" src="https://github.com/user-attachments/assets/72caaedb-1e72-4c80-9a7e-785d8367e6a4" />

<img width="1280" height="706" alt="1-03 disk-capacity png" src="https://github.com/user-attachments/assets/627cbc61-0667-4152-b0da-e3b99d03041d" />


#### Step 2: Installing Windows Server on VM

<img width="1277" height="704" alt="2-01 installing-windows-server-on-VM png" src="https://github.com/user-attachments/assets/61fa56bd-3283-4cbe-87f2-9860caf4fb36" />

<img width="1278" height="728" alt="2-02 add-ISO-img png" src="https://github.com/user-attachments/assets/6bbb1027-9957-499d-87d7-b9b719062dd2" />


#### Step 3: Setting Up Windows Server

<img width="1280" height="701" alt="3-02 select-server-OS png" src="https://github.com/user-attachments/assets/9a0fb08b-e5ad-42c0-be3c-54e99aefb36f" />

<img width="1278" height="703" alt="3-01 setting-up-windows-server png" src="https://github.com/user-attachments/assets/c986fc01-4508-4af4-8a78-4b7ee0852944" />

<img width="1277" height="707" alt="3-03 let-system-reboot png" src="https://github.com/user-attachments/assets/bd4c4d56-c587-4d21-a485-7c798183601e" />


#### Step 4: Installing Active Directory

<img width="1279" height="702" alt="4-01 installing-AD png" src="https://github.com/user-attachments/assets/24b0ea02-1daa-4910-94e7-be74eb4c7b26" />

<img width="1277" height="707" alt="4-02 features-selected png" src="https://github.com/user-attachments/assets/32329048-b4cd-4fb9-8765-5f86ca378ca9" />

<img width="1277" height="702" alt="4-03 promote-server png" src="https://github.com/user-attachments/assets/c78de166-1e32-430a-a166-55233498817e" />

<img width="1277" height="704" alt="4-04 new-forest png" src="https://github.com/user-attachments/assets/1ec17217-60f6-4acb-8c46-a2cb9f89bd13" />

<img width="1277" height="705" alt="4-05 prerequisites-passed png" src="https://github.com/user-attachments/assets/5cdeafe9-559f-483b-9277-cc081f0eb506" />

<img width="1278" height="704" alt="4-06 ADUC-completed png" src="https://github.com/user-attachments/assets/93c1ce73-c1cf-4b4b-a379-4f47526a7b53" />


#### Step 5: Creating Organizational Units (OUs)

<img width="1277" height="704" alt="5-01 creating-OUs png" src="https://github.com/user-attachments/assets/063f1e01-3dcf-42c5-b226-310f4b38eab9" />

<img width="1278" height="706" alt="5-02 naming-OU png" src="https://github.com/user-attachments/assets/ec40f870-b52d-4765-a5f3-5b2eddfaddd7" />


#### Step 6: What I Learned

#### Step 7: Final Thoughts
