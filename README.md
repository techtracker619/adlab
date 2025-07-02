# 🧑‍💻 Create and Manage AD Users, Groups, and OUs (GUI-Based Lab)

## 📌 Why This Lab?

This hands-on lab demonstrates a fundamental skill in IT and system administration: managing **Active Directory users, groups, and organizational units (OUs)**. It's designed to be beginner-friendly and use the GUI (Graphical User Interface), making it easy for new learners to follow without needing PowerShell.

---

## 🎯 Lab Objectives

- Create a clean OU structure (`Employees`, `IT`, `HR`)
- Add Active Directory user accounts using the GUI
- Create security groups and manage group membership
- Organize screenshots and documentation for GitHub
- Bonus: Add PowerShell automation (optional)

---

## 🧰 Requirements

- Windows Server 2019 or 2022 (Domain Controller set up)
- Active Directory Domain Services (AD DS role installed)
- Domain example: `corp.local`
- Access to **Active Directory Users and Computers** (`dsa.msc`)

---

## 🗂️ Project Structure



---

## 🪜 Step-by-Step Lab Instructions (GUI)

### 1️⃣ Open Active Directory Users and Computers

- Press `Windows + R` → type `dsa.msc` → hit Enter
- Make sure you're connected to your domain (e.g., `corp.local`)

---

### 2️⃣ Create Organizational Units (OUs)

1. Right-click on your domain name (e.g., `corp.local`)
2. Choose **New > Organizational Unit**
3. Create these OUs:
   - `Employees`
   - `IT` (inside Employees)
   - `HR` (inside Employees)

📸 *Upload screenshot as:* `screenshots/ou-structure.png`

---

### 3️⃣ Create Users in OUs

1. Right-click on the `IT` OU → **New > User**
2. Example:
   - First Name: `Tony`
   - Last Name: `Smith`
   - Username: `tsmith`
   - Password: `P@ssw0rd!` (or your standard test password)
   - Uncheck "User must change password at next logon" (optional)
3. Repeat to add more users

📸 *Upload screenshot as:* `screenshots/create-users.png`

---

### 4️⃣ Create Security Groups

1. Right-click on the `IT` OU → **New > Group**
2. Set group name: `IT_Staff`
   - Group scope: **Global**
   - Group type: **Security**
3. Do the same for `HR_Staff` in the HR OU

📸 *Upload screenshot as:* `screenshots/create-groups.png`

---

### 5️⃣ Add Users to Groups

1. Double-click the group (e.g., `IT_Staff`)
2. Go to the **Members** tab → Click **Add**
3. Enter the username (e.g., `tsmith`) → Click OK

📸 *Upload screenshot as:* `screenshots/add-user-to-group.png`

---

## 💻 Bonus: PowerShell Automation (Optional)

```powershell
# scripts/create-users.ps1

Import-Module ActiveDirectory

# Create a user in the IT OU
New-ADUser -Name "Tony Smith" -GivenName "Tony" -Surname "Smith" `
  -SamAccountName "tsmith" -UserPrincipalName "tsmith@corp.local" `
  -AccountPassword (ConvertTo-SecureString "P@ssw0rd!" -AsPlainText -Force) `
  -Enabled $true -Path "OU=IT,OU=Employees,DC=corp,DC=local"

# Create group if not already created
if (-not (Get-ADGroup -Filter {Name -eq "IT_Staff"})) {
    New-ADGroup -Name "IT_Staff" -GroupScope Global -GroupCategory Security -Path "OU=IT,OU=Employees,DC=corp,DC=local"
}

# Add user to the group
Add-ADGroupMember -Identity "IT_Staff" -Members "tsmith"



