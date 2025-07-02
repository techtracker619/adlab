
---

## 🔧 Lab Setup Instructions

### 1️⃣ Download ISOs
- [ ] Windows Server 2019 ISO (Evaluation): https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019
- [ ] (Optional) Windows 10 ISO: https://www.microsoft.com/en-us/software-download/windows10

📸 screenshots/WINDOWSERVER #2.PNG

---

### 2️⃣ Create Virtual Machines in VirtualBox

**VM 1: Domain Controller**
- Name: `AD-DC`
- Type: Windows Server 2019
- RAM: 4GB
- Disk: 60GB
- Network: Host-only Adapter

📸 _screenshots/Step2-Create-VM.png_

---

### 3️⃣ Install and Configure Server 2019

- Boot into ISO, complete installation
- Rename PC to `AD-DC`
- Set Admin password

📸 _screenshots/Step3-Install-Server2019.png_

---

### 4️⃣ Set Static IP

- IP: `192.168.1.10`
- Subnet: `255.255.255.0`
- Gateway: `192.168.1.1` (or blank)
- DNS: `127.0.0.1`

📸 _screenshots/Step4-Set-IP.png_

---

### 5️⃣ Install AD DS Role

- Server Manager → Add Roles → AD DS
- Promote to Domain Controller
- Domain: `lab.local`

📸 _screenshots/Step5-Install-AD-DS.png_

---

### 6️⃣ Verify AD Setup

- Open **Active Directory Users and Computers**
- Create Organizational Units (OUs)
- Add user accounts and groups

📸 _screenshots/Step6-AD-Verified.png_

---

### 7️⃣ (Optional) Add Windows 10 Client

- Configure IP: `192.168.1.20`
- DNS: `192.168.1.10` (DC)
- Join Domain: `lab.local`

📸 _screenshots/Step7-Win10-JoinDomain.png_

---

## 💡 Bonus PowerShell Scripts

| Script | Description |
|--------|-------------|
| `install_features.ps1` | Install AD DS and DNS roles |
| `create_users.ps1`     | Create bulk users in OU     |

---

## 📜 Scripts

### `scripts/install_features.ps1`

```powershell
Install-WindowsFeature -Name AD-Domain-Services, DNS -IncludeManagementTools





