### Beginner-Friendly Guide: Installing Miniconda with Mamba on Windows 11

#### **Step 1: Download Miniconda Installer**
1. Open your web browser and go to the [Miniconda download page](https://docs.conda.io/en/latest/miniconda.html).
2. Download the **64-bit Windows installer** for Python 3.x (the latest version).  
   ![Miniconda download page](https://docs.conda.io/en/latest/_images/download-miniconda.png)

---

#### **Step 2: Run the Installer**
1. Double-click the downloaded `.exe` file (e.g., `Miniconda3-latest-Windows-x86_64.exe`).
2. Follow these steps in the installer:
   - Click **Next**.
   - Accept the license terms → **I Agree**.
   - Choose **Install for: Just Me (recommended)** → **Next**.
   - Set the **Install Location** (default is fine) → **Next**.
   - **Advanced Options**:  
     ✅ **Add Miniconda3 to my PATH environment variable** (important!).  
     ✅ **Register Miniconda3 as my default Python 3.x**.  
     → **Install**.
   - Wait for the installation to finish → **Next** → **Finish**.

⚠️ **Note**: Ignore warnings about "adding to PATH." This is required for Mamba to work.

---

#### **Step 3: Open Anaconda Prompt**
- Press `Win` key → Type **"Anaconda Prompt"** → Open it as **Administrator** (right-click → "Run as administrator").  
  ![Open Anaconda Prompt](https://docs.conda.io/en/latest/_images/anaconda-prompt.png)

---

#### **Step 4: Install Mamba**
In the **Anaconda Prompt**, run:
```bash
conda install mamba -n base -c conda-forge
```
- Type `y` and press **Enter** to confirm.  
- Wait for the installation (this may take 2-5 minutes).

---

#### **Step 5: Verify Installation**
Check if Mamba works:
```bash
mamba --version
```
You should see something like: `mamba 1.5.1` (version may vary).

---

#### **Step 6: Test Mamba**
Create a test environment:
```bash
mamba create -n test_env python=3.10
```
Activate the environment:
```bash
conda activate test_env
```
Deactivate it after testing:
```bash
conda deactivate
```

---

#### **Troubleshooting**
- **"Command not found"**?  
  → Reopen the **Anaconda Prompt** or restart your computer.
- **Installation errors**?  
  → Run `conda clean --all` and retry installing Mamba.
- **Slow downloads**?  
  → Use [Mamba mirrors](https://mamba.readthedocs.io/en/latest/user_guide/configuration.html#channels) or try:
  ```bash
  mamba install -c conda-forge mamba --no-update-deps
  ```

---

#### **Key Commands Cheatsheet**
| Command                          | Description                     |
|----------------------------------|---------------------------------|
| `mamba create -n env_name python=3.10` | Create a new environment        |
| `mamba activate env_name`        | Activate environment            |
| `mamba install package_name`     | Install a package              |
| `mamba list`                     | List installed packages        |
| `mamba deactivate`               | Exit environment               |

---

✅ **Done!** You now have Miniconda with Mamba installed. Use `mamba` instead of `conda` for faster package management.  
→ Learn more: [Mamba Documentation](https://mamba.readthedocs.io/en/latest/)
