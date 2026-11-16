
# Node.js Development Environment Setup (Windows)

A step-by-step guide to preparing Windows, installing Node.js, configuring PATH, fixing PowerShell execution policy issues, and verifying your development environment.

This guide is intended for Windows 10/11 computers with administrator access.

---

## 1. Prerequisites

Before starting, make sure you have:

- Windows 10 or Windows 11
- Administrator access to the computer
- Visual Studio Code (VS Code)
- Internet connection

## 2. Prepare Windows PowerShell

Before installing Node.js, configure PowerShell to allow locally created scripts to run.

### Step 1: Open PowerShell as Administrator

1. Press `Windows + S`.
2. Search for `PowerShell`.
3. Right-click Windows PowerShell.
4. Select **Run as Administrator**.

### Step 2: Configure Execution Policy

Execute:

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
```

This allows locally created PowerShell scripts to run while restricting unsigned downloaded scripts.

**Note:** This setting applies to the current Windows user. Organization-managed policies may override it.

## 3. Install Node.js

### Step 1: Download Node.js

Visit the official website:

https://nodejs.org/en/download

Select:

- Operating System: Windows
- Architecture: x64
- Installer: Windows Installer (.msi)
- Version: LTS (Long-Term Support)

### Step 2: Run the Installer

1. Locate the downloaded `.msi` file.
2. Run the installer.
3. Accept the license agreement.
4. Keep the default installation directory:

```text
C:\Program Files\nodejs\
```

5. Ensure the following components are selected:
   - Node.js runtime
   - npm package manager
   - Add to PATH
6. Complete the installation.

## 4. Configure Windows PATH (If Necessary)

Normally, the Node.js installer automatically adds Node.js to PATH.

If Windows cannot recognize `node`, `npm`, or `npx`, check the PATH configuration.

### Step 1: Open Environment Variables

1. Press `Windows + S`.
2. Search for `Environment Variables`.
3. Select **Edit the system environment variables**.
4. Click **Environment Variables**.

### Step 2: Edit PATH

Under **System variables**:

1. Find `Path`.
2. Click **Edit**.
3. Click **New**.
4. Add:

```text
C:\Program Files\nodejs\
```

5. Click OK on all windows.

### Step 3: Restart Your Terminal

Close and reopen VS Code to refresh the environment variables.

## 5. Verify Node.js Installation

Open a new VS Code terminal.

Execute these commands individually:

### Check Node.js

```powershell
node -v
```

### Check npm

```powershell
npm -v
```

### Check npx

```powershell
npx -v
```

All three commands should display their respective version numbers.

### Check Installation Paths

```powershell
where.exe node
where.exe npm
where.exe npx
```

Expected installation directory:

```text
C:\Program Files\nodejs\
```

## 6. Fix Common PowerShell Errors

### Error: npm.ps1 cannot be loaded

Example:

```text
npm.ps1 cannot be loaded because running scripts is disabled on this system.
```

**Solution:**

Open PowerShell and execute:

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
```

If the error specifically indicates that a downloaded script is blocked, inspect the file and, if trusted, unblock it:

```powershell
Unblock-File "C:\Program Files\nodejs\npm.ps1"
Unblock-File "C:\Program Files\nodejs\npx.ps1"
```

If an organization policy blocks the change, contact the administrator.

### Alternative: Use Command Prompt

If PowerShell continues to cause script execution problems, use Command Prompt instead.

In VS Code:

1. Open Terminal.
2. Click the dropdown arrow beside the `+` button.
3. Select Command Prompt.

Then execute:

```cmd
node -v
npm -v
npx -v
```

Command Prompt uses the `.cmd` launchers and avoids PowerShell's `.ps1` execution policy restrictions.

### Error: 'node' is not recognized

**Solution:**

Check whether this directory exists:

```text
C:\Program Files\nodejs\
```

If it exists, add it to Windows PATH using Section 4.

If it does not exist, reinstall Node.js using the official MSI installer.

### Error: Missing script: dev

**Solution:**

Check whether your `package.json` contains a development script.

Example:

```json
{
  "scripts": {
    "start": "node server/server.js",
    "dev": "nodemon server/server.js"
  }
}
```

### Error: Cannot find module

**Solution:**

Navigate to your project directory and execute:

```powershell
npm install
```

## 7. Create Your First Node.js Project

Once Node.js is installed and verified, create a project.

```powershell
mkdir SkillsTest
cd SkillsTest
```

Initialize your Node.js project:

```powershell
npm init -y
```

Install Express and MySQL dependencies:

```powershell
npm install express mysql2 cors dotenv
```

Install Nodemon:

```powershell
npm install --save-dev nodemon
```

## 8. Important Reminders

1. Always use the official Node.js website to download Node.js.
2. Prefer the LTS version for development.
3. Do not repeatedly reinstall Node.js if the problem is only PATH configuration.
4. Restart VS Code after modifying environment variables.
5. Configure PowerShell only once per Windows user account unless its settings are reset or managed by an administrator.
6. Do not disable PowerShell security restrictions globally.
7. Keep your Node.js installation directory unchanged unless you update PATH accordingly.

**Official Resources:**

- Node.js: https://nodejs.org/
- Node.js Documentation: https://nodejs.org/docs/
- npm Documentation: https://docs.npmjs.com/
- Express.js: https://expressjs.com/
