# 🖥️ Local Active Directory Lab Setup (Beginner Friendly)

This repository provides a **step-by-step beginner-friendly lab setup** for building a local **Active Directory (AD)** environment using **Oracle VM VirtualBox** and **Windows Server 2019**. This project is perfect for IT students, entry-level professionals, or anyone looking to learn the fundamentals of Windows Server, AD, and networking — all on your local machine.

---

## 📦 What You'll Need

| Tool                    | Purpose                                          |
|-------------------------|--------------------------------------------------|
| Oracle VirtualBox       | Free tool to run virtual machines (VMs)          |
| Windows Server 2019 ISO | OS for the Domain Controller (DC) VM             |

---

## 🔗 Downloads

### ✅ Step 1: Download Oracle VirtualBox

1. Visit the official Oracle VirtualBox download page:  
   🔗 https://www.virtualbox.org/wiki/Downloads

2. Download the version that matches your OS (Windows, macOS, or Linux).

3. Run the installer and use default settings.

📸 _Add a screenshot of the installation wizard here._

---

### ✅ Step 2: Download Windows Server 2019 ISO

1. Go to Microsoft Evaluation Center:  
   🔗 https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019

2. Choose **ISO** as the download format and fill in the basic form.

3. Download the ISO and store it where you'll mount it in VirtualBox.

📸 _Screenshot idea: Form filled out and download progress._

---

## ⚙️ Step-by-Step Lab Setup

### 🔧 Step 3: Create a Virtual Machine (VM)

1. Open VirtualBox.
2. Click **New** → Name it `AD-DC` or `DomainController`.
3. Set:
   - Type: `Microsoft Windows`
   - Version: `Windows 2019 (64-bit)`
4. Memory: 4 GB minimum (4096 MB)
5. Create a virtual hard disk:
   - Format: VDI
   - Storage: Dynamically allocated
   - Size: At least 60 GB

📸 _Add screenshots of VM settings._

---

### 🧩 Step 4: Install Windows Server 2019

1. Start the VM and select the ISO as the boot disk.
2. Complete installation:
   - Choose Standard Edition (Desktop Experience)
   - Use entire disk (default)
   - Set a secure Administrator password

📸 _Add screenshots of installation and login._

---

### 🌐 Step 5: Configure Static IP Address

1. Go to **Network Settings**:
   - Control Panel → Network and Sharing → Change Adapter Settings
2. Right-click `Ethernet` → Properties → IPv4 → Properties
3. Configure:
   - IP: `192.168.100.10`
   - Subnet: `255.255.255.0`
   - Gateway: (Optional) `192.168.100.1`
   - DNS: `127.0.0.1`

📸 _Add screenshot of IPv4 static IP configuration._

---

### 🏗️ Step 6: Install Active Directory Domain Services (AD DS)

1. Open **Server Manager**
2. Click **Add roles and features**
3. Choose:
   - Role-based or feature-based installation
   - Select this server
   - Add **AD DS** and **DNS Server**

📸 _Screenshot of selected roles._

---

### 🏁 Step 7: Promote Server to Domain Controller

1. After installation, click the flag in Server Manager
2. Choose **Promote this server to a domain controller**
3. Options:
   - Create a new forest
   - Domain name: `lab.local`
   - Set DSRM password
   - Leave defaults and click Install

📸 _Screenshot of each step and reboot._

---

### ✅ Step 8: Verify Active Directory

1. After reboot, login and open:
   - **Server Manager** → Tools → **Active Directory Users and Computers**
2. Create:
   - Organizational Units (OUs)
   - Sample Users
   - Security Groups

📸 _Screenshot of ADUC with OUs and users._

---

## 🧠 Bonus Section: Automation with PowerShell (Scripts in Separate Repo or Folder)

To further automate this lab, you can use PowerShell to:

- Install AD roles
- Promote the server to a domain controller
- Create OUs
- Bulk-create users
- Create security groups and assign members

These scripts will be available in a dedicated `scripts/` folder or separate repo.

### Scripts You'll Eventually Have:

| Script Name                     | Function                                 |
|--------------------------------|------------------------------------------|
| `install_features.ps1`         | Installs AD DS + DNS roles               |
| `promote_to_dc.ps1`            | Promotes server to domain controller     |
| `create_ous.ps1`               | Creates OUs like IT, HR, Users           |
| `create_users.ps1`             | Creates 10 sample users                  |
| `create_group_and_add_users.ps1` | Creates group and adds users           |

> These PowerShell scripts are designed for full automation and will be added in a separate script-focused README.

---

## 📸 Screenshots Folder

Store all screenshots inside the `/screenshots` folder.  
Reference them like this inside the README:

```markdown
![Step 5 - Static IP](./screenshots/static-ip.png)
```

---

## ✅ Key Skills Practiced

- VirtualBox VM setup and networking
- Windows Server 2019 installation and configuration
- Active Directory setup (AD DS, DNS)
- Organizational structure in AD
- Real-world IT lab simulation
- PowerShell-based automation for sysadmin tasks

---







