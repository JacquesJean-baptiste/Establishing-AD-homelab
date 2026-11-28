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
To host the lab, I downloaded and installed VMware Workstation Pro 17.6.4 from the Broadcom support portal. VMware is a hypervisor, so it lets me run the server as a virtual machine on my PC instead of dedicated hardware. This keeps the lab isolated from my main system. It also lets me snapshot or rebuild the environment if something breaks.

<img width="950" height="392" alt="0-01 workstation-install" src="https://github.com/user-attachments/assets/e2c8ad73-6e33-43b9-8fca-440988e5b8a2" />

---

I downloaded the Windows Server 2022 64-bit ISO from Microsoft's Evaluation Center. The ISO is the installation media for the server operating system. The evaluation edition is free and works for lab and learning purposes. I saved it locally so I could attach it to the virtual machine later.

<img width="949" height="438" alt="0-02 server-ISO-download" src="https://github.com/user-attachments/assets/7c70b10e-e3e6-45bd-aed3-8d3140da7b4b" />

---


#### Step 1: Creating a New VM

I opened VMware Workstation and started the New Virtual Machine Wizard. I chose the Typical configuration, which applies standard hardware defaults. This is enough for a lab and avoids unnecessary advanced settings. It also keeps the VM compatible with Workstation 17.5 and later.

<img width="1277" height="746" alt="1-01 creating-new-vm png" src="https://github.com/user-attachments/assets/e5a2ded9-4603-43d4-ae60-f69d6747f54d" />

---

I selected Microsoft Windows as the guest operating system and Windows Server 2022 as the version. This tells VMware which virtual hardware profile and defaults to use for the VM. The correct selection also helps the VM perform well and be compatible with VMware Tools later.

<img width="1278" height="704" alt="1-02 select-VM-OS png" src="https://github.com/user-attachments/assets/72caaedb-1e72-4c80-9a7e-785d8367e6a4" />

---

I set the maximum disk size to 20 GB, below VMware's 60 GB recommendation, because the lab only needs a small footprint. The disk file starts small and grows as data is added, so it doesn't use the full 20 GB up front. I kept the default option of splitting the virtual disk into multiple files. This makes the VM easier to move to another computer.

<img width="1280" height="706" alt="1-03 disk-capacity png" src="https://github.com/user-attachments/assets/627cbc61-0667-4152-b0da-e3b99d03041d" />

---


#### Step 2: Installing Windows Server on VM

With the VM created and powered off, I right-clicked it in the Library and opened Settings. This screen is where the virtual hardware gets configured before the first boot. The VM is set to 2 GB of memory, 2 processors, a 20 GB NVMe disk, and a NAT network adapter. NAT lets the VM reach the internet through my PC's connection while staying separate from my physical network.

<img width="1277" height="704" alt="2-01 installing-windows-server-on-VM png" src="https://github.com/user-attachments/assets/61fa56bd-3283-4cbe-87f2-9860caf4fb36" />

---

Under the CD/DVD (SATA) device, I selected 'Use ISO image file' and browsed to the Windows Server evaluation ISO in my Downloads folder. This acts like inserting a virtual installation disc into the server. I also kept 'Connect at power on' checked. That way the VM boots directly into Windows Setup on its first start.

<img width="1278" height="728" alt="2-02 add-ISO-img png" src="https://github.com/user-attachments/assets/6bbb1027-9957-499d-87d7-b9b719062dd2" />

---


#### Step 3: Setting Up Windows Server

I powered on the VM, and it booted from the ISO into Microsoft Server Operating System Setup. The first screen asks for language, time and currency format, and keyboard layout. I kept the defaults of English (United States) and a US keyboard. After that I clicked Next to continue.

<img width="1280" height="701" alt="3-02 select-server-OS png" src="https://github.com/user-attachments/assets/9a0fb08b-e5ad-42c0-be3c-54e99aefb36f" />

---

Setup offered four editions: Standard and Datacenter, each with and without Desktop Experience. I selected Windows Server 2022 Standard Evaluation (Desktop Experience). This installs the full graphical interface rather than the command-line-only Server Core. The GUI makes it easier to learn Active Directory tools and take screenshots for documentation.

<img width="1278" height="703" alt="3-01 setting-up-windows-server png" src="https://github.com/user-attachments/assets/c986fc01-4508-4af4-8a78-4b7ee0852944" />

---

After the installation finished, the VM rebooted on its own and landed on the lock screen. The server prompts for Ctrl+Alt+Delete before login, which is a standard Windows Server security feature. In VMware, I sent this through the VM menu so my host PC wouldn't intercept the key combination. I then signed in with the Administrator password I set during setup.

<img width="1277" height="707" alt="3-03 let-system-reboot png" src="https://github.com/user-attachments/assets/bd4c4d56-c587-4d21-a485-7c798183601e" />

---


#### Step 4: Installing Active Directory

From the Server Manager dashboard, I opened the Manage menu and selected Add Roles and Features. This wizard is how Windows Server adds new capabilities, including Active Directory Domain Services (AD DS). The dashboard's Quick Start panel lists the same option. The wizard also lets me choose the destination server, which here is the local VM.

<img width="1279" height="702" alt="4-01 installing-AD png" src="https://github.com/user-attachments/assets/24b0ea02-1daa-4910-94e7-be74eb4c7b26" />

---

In the wizard, I selected the AD DS role and reviewed the Features page, where Group Policy Management is checked. AD DS is the service that stores and manages users, computers, and policies for the domain. Group Policy Management adds the console used to create and apply those policies. Having both installed up front means the tools are ready when I start building out the domain.

<img width="1277" height="707" alt="4-02 features-selected png" src="https://github.com/user-attachments/assets/32329048-b4cd-4fb9-8765-5f86ca378ca9" />

---

Once the installation completed, the results page reported 'Configuration required' for Active Directory Domain Services. Installing the role only adds the software. It doesn't make the server a domain controller yet. I clicked 'Promote this server to a domain controller' to launch the configuration wizard and finish the setup.

<img width="1277" height="702" alt="4-03 promote-server png" src="https://github.com/user-attachments/assets/c78de166-1e32-430a-a166-55233498817e" />

---

In the AD DS Configuration Wizard, I selected 'Add a new forest' because this is the first domain in a new environment. I entered testlab.local as the root domain name. The forest is the top-level security boundary in Active Directory, and the root domain is the first domain created within it. The wizard then walks through domain controller options, DNS, and file paths before the prerequisites check.

<img width="1277" height="704" alt="4-04 new-forest png" src="https://github.com/user-attachments/assets/1ec17217-60f6-4acb-8c46-a2cb9f89bd13" />

---

The prerequisites check passed, though it flagged warnings about legacy cryptography defaults and the absence of a static IP on the network adapter. Neither blocks installation. In a production environment I would assign a static IP first, since domain controllers depend on stable addressing for DNS. I clicked Install, and the server rebooted automatically at the end of the promotion.

<img width="1277" height="705" alt="4-05 prerequisites-passed png" src="https://github.com/user-attachments/assets/5cdeafe9-559f-483b-9277-cc081f0eb506" />

---

After the reboot, I opened Active Directory Users and Computers (ADUC) from the Tools menu. The testlab.local domain appears in the console tree, which confirms the promotion succeeded. The Server Manager sidebar now also lists DNS, which was installed alongside AD DS to resolve domain names. ADUC is the main tool for managing users, groups, computers, and organizational units.

<img width="1278" height="704" alt="4-06 ADUC-completed png" src="https://github.com/user-attachments/assets/93c1ce73-c1cf-4b4b-a379-4f47526a7b53" />

---


#### Step 5: Creating Organizational Units (OUs)

In ADUC, I right-clicked the testlab.local domain and selected New > Organizational Unit. The menu also shows the other object types I can create, such as users, groups, and computers. OUs are containers that organize those objects into a logical structure. That structure is what lets administrators delegate control and apply Group Policy to specific sets of users or computers.

<img width="1277" height="704" alt="5-01 creating-OUs png" src="https://github.com/user-attachments/assets/063f1e01-3dcf-42c5-b226-310f4b38eab9" />

---

I named the first OU 'Employees' and left 'Protect container from accidental deletion' checked. This is the container where I'll place user accounts for the lab. The protection setting prevents the OU from being removed by mistake, which is a good habit for any directory structure. From here I can create more OUs, users, and groups to simulate a real company environment.

<img width="1278" height="706" alt="5-02 naming-OU png" src="https://github.com/user-attachments/assets/ec40f870-b52d-4765-a5f3-5b2eddfaddd7" />

---


#### Step 6: What I Learned

This lab showed me how the layers of a Windows environment fit together and how they relate to everyday help desk work. Running the server in VMware taught me how a hypervisor allocates hardware resources, which helps when troubleshooting VMs or reproducing user issues in a safe test environment. Building Active Directory, DNS, and Organizational Units showed me how user identities are created, structured, and authenticated, which supports core help desk tasks like password resets, account lockouts, onboarding, and offboarding. Installing Group Policy Management also gave me context for how policies linked to OUs control settings like password rules and desktop configuration, so I know where to look when a setting isn't applying to a user.

---

#### Step 7: Final Thoughts

This project gave me hands-on experience with the same core technologies used in enterprise IT environments, and it connected concepts from my A+ studies to real administration work. Building the environment from scratch showed me how each layer depends on the one before it: the hypervisor, the operating system, the directory service, and then the organizational structure. The prerequisite warnings, like the missing static IP, also reminded me that production environments require more planning than a lab. Next, I plan to assign a static IP, create users and groups, apply Group Policy Objects, and join a Windows client VM to the domain. These steps will build the skills that help desk and sysadmin roles use every day, like account management and password resets.

---
