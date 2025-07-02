# 🖥️ Local Active Directory Lab Setup (Beginner Friendly)

This repository provides a **step-by-step beginner-friendly lab setup** for building a local **Active Directory (AD)** environment using **Oracle VM VirtualBox** and **Windows Server 2019**. This project is perfect for IT students, entry-level professionals, or anyone looking to learn the fundamentals of Windows Server, AD, and networking — all on your local machine.

---

## 📦 What You'll Need

| Tool               | Purpose                                        |
|-------------------|------------------------------------------------|
| Oracle VirtualBox | Free tool to run virtual machines (VMs)        |
| Windows Server 2019 ISO | The OS for the Domain Controller VM |
| (Optional) Windows 10 ISO | For testing domain join as a client |

---

## 🔗 Downloads

### ✅ Step 1: Download Oracle VirtualBox

1. Visit the official Oracle VirtualBox download page:  
   🔗 https://www.virtualbox.org/wiki/Downloads

2. Download the version that matches your operating system (Windows, macOS, Linux).

3. Install it using the setup wizard (default settings are fine).

📸 Add a screenshot of the VirtualBox installation wizard.

---

### ✅ Step 2: Download Windows Server 2019 ISO

1. Visit Microsoft Evaluation Center:  
   🔗 https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019

2. Select **ISO** and fill out the short form (name, email, etc.).

3. Download the ISO file and save it somewhere you can find it later.

📸 Screenshot suggestion: Form filled out, download in progress.

> 📝 This is a trial version valid for 180 days — more than enough for learning.

---

### (Optional) Download Windows 10 ISO

1. Visit the Windows 10 download page:  
   🔗 https://www.microsoft.com/en-us/software-download/windows10ISO

2. Select your version and download the ISO.

> This is useful if you want to test domain join with a client machine.

---

## ⚙️ Step-by-Step Lab Setup

### 🔧 Step 3: Create a Virtual Machine in VirtualBox for Server 2019

1. Open VirtualBox.  
2. Click **New** → Name it `AD-DC` or `DomainController`.  
3. Choose:  
   - Type: `Microsoft Windows`  
   - Version: `Windows 2019 (64-bit)`  
4. Set memory to at least **4096 MB (4 GB)**.  
5. Create a virtual hard disk:  
   - Size: At least **60 GB**  
   - Format: `VDI` → Dynamically allocated  
6. Once VM is created, click **Settings**:  
   - **Storage** → Mount the Server 2019 ISO  
   - **Network** → Change adapter to `Host-only Adapter` (for local lab)

📸 Add screenshots of each step.

---

### 🧩 Step 4: Install Windows Server 2019

1. Start the VM.  
2. Follow the on-screen setup:  
   - Language: English  
   - Edition: Standard (Desktop Experience)  
   - Disk: Use the entire disk (default)  
3. Set a secure **Administrator** password.

📸 Screenshot of language/edition selection, installation progress, first login.

---

### 🌐 Step 5: Configure Static IP Address

1. Log into the Server.  
2. Open **Control Panel** → **Network and Sharing Center** → **Change Adapter Settings**  
3. Right-click **Ethernet** → **Properties** → Select **IPv4** → Click **Properties**  
4. Set static IP:  
   - IP: `192.168.100.10`  
   - Subnet: `255.255.255.0`  
   - Gateway: Leave blank or use `192.168.100.1`  
   - DNS: `127.0.0.1` (localhost)

📸 Screenshot of IPv4 settings window.

---

### 🏗️ Step 6: Install AD DS Role (Active Directory Domain Services)

1. Open **Server Manager** → Click **Add roles and features**.  
2. Select:  
   - Role-based or feature-based installation  
   - Server name (default)  
   - **Active Directory Domain Services** + **DNS Server**  
3. Click Next → Install

📸 Screenshot of roles selected.

---

### 🏁 Step 7: Promote Server to Domain Controller

1. After AD DS installation, click the flag at the top of Server Manager → **Promote this server to a domain controller**.  
2. Select **Add a new forest** → Domain name: `lab.local`  
3. Set DSRM password → Click through default options → Install

📸 Screenshot of each promotion step and final reboot.

---

### ✅ Step 8: Verify AD Setup

1. After reboot, login with domain credentials.  
2. Open **Active Directory Users and Computers** from Server Manager → Tools.  
3. Create:  
   - Organizational Units (OUs)  
   - Test Users (Right-click OU → New → User)  
   - Security Groups

📸 Screenshot of ADUC with new OUs and Users.

---

### (Optional) 🖥️ Step 9: Add Windows 10 Client to Domain

1. Create a second VM → Install Windows 10.  
2. Set static IP (e.g., `192.168.100.20`) and DNS to point to the Domain Controller: `192.168.100.10`  
3. Join Domain:  
   - System Properties → Change Settings → Domain: `lab.local`  
   - Enter domain admin credentials  
   - Reboot when prompted

📸 Screenshot of domain join window and success message.

---

## 🔄 Bonus: PowerShell Automation Scripts

Place these inside the `/scripts` folder.

### `scripts/install_features.ps1`
```powershell
Install-WindowsFeature -Name AD-Domain-Services, DNS -IncludeManagementTools
```

### `scripts/create_users.ps1`
```powershell
Import-Module ActiveDirectory

for ($i = 1; $i -le 10; $i++) {
    $username = "User$i"
    $password = ConvertTo-SecureString "P@ssword123" -AsPlainText -Force
    New-ADUser -Name $username `
               -SamAccountName $username `
               -UserPrincipalName "$username@lab.local" `
               -AccountPassword $password `
               -Enabled $true `
               -Path "OU=Users,DC=lab,DC=local"
}
```

---

## 📸 Screenshots Folder

Place all screenshots in `/screenshots/` and reference them like this:
```markdown
![Step 4 - Static IP Settings](./screenshots/static-ip-settings.png)
```

---

## ✅ Key Learning Outcomes

- Understand VirtualBox VM creation and networking  
- Practice installing and configuring Windows Server 2019  
- Set up and manage Active Directory, users, OUs, and DNS  
- Join clients to a domain  
- Automate AD tasks using PowerShell

---

## 📚 License

This lab is open-source under the MIT License.






