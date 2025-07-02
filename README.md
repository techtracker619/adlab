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

![imagealt](https://github.com/techtracker619/adlab/blob/eac0c1f3fb8af6e02fd8fda0c31079bf11e3aa2f/screenshots/VL%232.PNG)

---

### ✅ Step 2: Download Windows Server 2019 ISO

1. Go to Microsoft Evaluation Center:  
   🔗 https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019

2. Choose **ISO** as the download format and fill in the basic form.

3. Download the ISO and store it where you'll mount it in VirtualBox.

![imagealt](https://github.com/techtracker619/adlab/blob/1762fad05ecb56aeaf280315e8e951280477db80/screenshots/WINDOWSERVER%20%232.PNG)

---

## ⚙️ Step-by-Step Lab Setup

### 🔧 Step 3: Create Virtual Machine with ISO Attached (Recommended Beginner Method)

1. Open **Oracle VirtualBox** and click the **New (Add +)** button.
2. In the **Create Virtual Machine** window, configure the following:
   - **Name**: `AC-DC-SERVER` or `AD-DC`
   - **Folder**: Leave as default (or select a custom location)
   - **ISO Image**: Click the 📂 folder icon → Browse to your downloaded `Windows Server 2019` ISO file
   - **Edition**: Auto-detects (e.g., *Windows Server 2019 Standard Evaluation*)
   - **Type**: Microsoft Windows  
   - **Version**: Windows Server 2019 (64-bit)

3. ✅ **Check** the option: **Skip Unattended Installation**  
   > This gives you full control of the Windows installation process and avoids automation.

4. Click **Next**, then continue:
   - **Memory Size**: Set to at least **4096 MB (4 GB)**
   - **Hard Disk**: Create a new virtual hard disk
     - Type: VDI (VirtualBox Disk Image)
     - Storage: Dynamically allocated
     - Size: At least **60 GB**

5. Click **Finish** to create the virtual machine with the ISO already attached.

![imagealt](https://github.com/techtracker619/adlab/blob/b8beccfe17a19ad0bd616ff773b176346e30c8aa/screenshots/VL%234B.PNG)

---

### 🧩 Step 4: Boot and Install Windows Server 2019 from ISO

1. In VirtualBox, select the new VM (`AC-DC-SERVER`) and click **Start**.
2. The VM will boot directly into the Windows Server 2019 installation wizard.
3. Follow the installer:
   - Language: English (United States)
   - Edition: **Windows Server 2019 Standard (Desktop Experience)**
   - Accept license terms
   - Choose **Custom: Install Windows Only (Advanced)**
   - Select the virtual hard disk → Click **Next**

4. Installation will begin and the VM will restart once complete.
5. After reboot, you’ll be asked to create an **Administrator password**.
6. Login with your credentials — you’re now inside Windows Server 2019!

![imagealt](https://github.com/techtracker619/adlab/blob/5e49b80554ece83c3290068228cf322de46c2945/screenshots/VirtualBox_AC-DC-SERVER_23_06_2025_22_15_16.png)
![imagealt](https://github.com/techtracker619/adlab/blob/eae1ac477b3f9971e2e5f74676b5cbf1a9b098ed/screenshots/VirtualBox_AC-DC-SERVER_23_06_2025_22_12_55.png)
- Installation wizard screen  
- Edition selection  
- Disk selection  
- Password setup  
- First login

---

✅ This method matches the newer VirtualBox workflow and is easier for first-time users since it bundles the ISO setup with VM creation.  


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

![imagealt](https://github.com/techtracker619/adlab/blob/0c78c95163f282859a77ddb7b39f26c659897e94/screenshots/VirtualBox_AC-DC-SERVER_23_06_2025_23_32_25.png)
![imagealt](https://github.com/techtracker619/adlab/blob/c7e5d8bad6cbe57b1f6cd093e17b5c9542b3f282/screenshots/VirtualBox_AC-DC-SERVER_23_06_2025_23_43_39.png)
![imagealt](https://github.com/techtracker619/adlab/blob/7c35181286bd058efc7bb2436063337f4c05968e/screenshots/VirtualBox_AC-DC-SERVER_23_06_2025_23_46_05.png)

---

### 🏗️ Step 6: Install Active Directory Domain Services (AD DS)

1. Open **Server Manager**
2. Click **Add roles and features**
3. Choose:
   - Role-based or feature-based installation
   - Select this server
   - Add **AD DS** and **DNS Server**

![imagealt](https://github.com/techtracker619/adlab/blob/212f176521ab5d14f5461df343e42866b9e1e409/screenshots/VirtualBox_AC-DC-SERVER_23_06_2025_22_57_46.png)
![imagealt](https://github.com/techtracker619/adlab/blob/be6c10af7cfdb0e89553a596a594df49c59dff09/screenshots/VirtualBox_AC-DC-SERVER_23_06_2025_22_58_31.png)
![imagealt](https://github.com/techtracker619/adlab/blob/f0d1b700d9b9bb4668ff0629b3eafa9487161a05/screenshots/VirtualBox_AC-DC-SERVER_23_06_2025_22_59_36.png)
![imagealt](https://github.com/techtracker619/adlab/blob/d56239b0a786603d925c05a547b16a4a21cb9aee/screenshots/VirtualBox_AC-DC-SERVER_23_06_2025_23_01_41.png)

---

### 🏁 Step 7: Promote Server to Domain Controller

1. After installation, click the flag in Server Manager
2. Choose **Promote this server to a domain controller**
3. Options:
   - Create a new forest
   - Domain name: `lab.local`
   - Set DSRM password
   - Leave defaults and click Install

![imagealt](https://github.com/techtracker619/adlab/blob/a615c03962db0254bd2a5ce6283bc420d3c4c126/screenshots/VirtualBox_AC-DC-SERVER_23_06_2025_23_08_52.png)
![imagealt](https://github.com/techtracker619/adlab/blob/8b50438cd0c7a1814ba66db50528603f57befebe/screenshots/VirtualBox_AC-DC-SERVER_23_06_2025_23_09_41.png)

---

### ✅ Step 8: Verify Active Directory

1. After reboot, login and open:
   - **Server Manager** → Tools → **Active Directory Users and Computers**




## ✅ Key Skills Practiced

- VirtualBox VM setup and networking
- Windows Server 2019 installation and configuration
- Active Directory setup (AD DS, DNS)
- Organizational structure in AD
- Real-world IT lab simulation
- PowerShell-based automation for sysadmin tasks

---


## 🤝 Author

Anthony Jenkins  
Follow for more labs on AD, Cybersecurity, and Systems Administration




