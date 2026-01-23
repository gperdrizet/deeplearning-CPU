# Containerized TensorFlow CPU development environment

A containerized TensorFlow AI/ML development environment for CPU-only systems. This repository provides a consistent development environment using VS Code Dev Containers, eliminating the need for manual environment setup. It provides the following:

- Python 3.10
- TensorFlow 2.16 (CPU)
- Keras 3.3
- NumPy 1.24
- Pandas 2.2
- Scikit-learn 1.4
- SciPy 1.13
- Matplotlib 3.10
- JupyterLab 2.3

This container is ideal for users without NVIDIA GPUs, including MacOS users, or anyone who wants a lightweight TensorFlow environment for learning, prototyping, or CPU-based inference.

## 1. Prerequisites

Before you can use this development container, you need to have:

1. **Docker** (see platform-specific instructions below)
2. **Visual Studio Code** - [Download here](https://code.visualstudio.com)
3. **Dev Containers extension** - Install from the VS Code Extensions marketplace (`ms-vscode-remote.remote-containers`)

---

## 2. Docker installation instructions

### 2.1. Windows

Full installation documentation here: [Install Docker Desktop on Windows](https://docs.docker.com/desktop/setup/install/windows-install)

1. **Check system requirements**
   - Windows 10 64-bit: Pro, Enterprise, or Education (Build 19041 or higher), or Windows 11
   - Windows 11 64-bit: Enterprise, Pro, or Education version 23H2 (build 22631) or higher
   - WSL 2.1.5 or later
   - 64-bit processor with Second Level Address Translation (SLAT)
   - 4GB system RAM
   - Enable hardware virtualization in BIOS/UEFI. For more information, see Virtualization.

2. **Install or update WSL**

    Full documentation here: [WSL: Verification and setup](https://docs.docker.com/desktop/setup/install/windows-install#wsl-verification-and-setup)

    - To check your WSL version, open PowerShell as Administrator and run:

    ```powershell
    wsl --version
    ```

    - Then install or update as needed:

    ```powershell
    wsl --install
    ```

    ```powershell
    wsl --update
    ```
   - Restart your computer when prompted

3. **Download and install Docker Desktop**
   - Download Docker Desktop from [https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)
   - Run the installer and follow the prompts
   - Ensure "Use WSL 2 instead of Hyper-V" is selected during installation

4. **Start Docker Desktop**
   - Launch Docker Desktop from the Start menu
   - Wait for Docker to fully start (the whale icon in the system tray will stop animating)

5. **Verify installation**
   - Open a terminal (PowerShell or Command Prompt) and run:
     ```powershell
     docker --version
     ```

    The command should complete without error.

---

### 2.2. MacOS

Full installation documentation here: [Install Docker Desktop on Mac](https://docs.docker.com/desktop/setup/install/mac-install)

1. **Check system requirements**
   - macOS 12 (Monterey) or later
   - At least 4GB of RAM
   - Apple Silicon (M1/M2/M3) or Intel processor

2. **Download Docker Desktop**
   - Visit [https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)
   - Download the appropriate version for your Mac:
     - **Apple Silicon (M1/M2/M3):** Download the Apple Silicon version
     - **Intel:** Download the Intel version

3. **Install Docker Desktop**
   - Open the downloaded `.dmg` file
   - Drag Docker to the Applications folder
   - Open Docker from the Applications folder
   - Accept the service agreement when prompted

4. **Configure Docker Desktop (recommended)**
   - Click the Docker icon in the menu bar → Preferences
   - Under **Resources**, adjust memory and CPU limits as needed for your workload
   - Click **Apply & Restart**

5. **Verify installation**
   - Open Terminal and run:
     ```bash
     docker --version
     ```

    The command should complete without error.

> **Note:** This CPU-only TensorFlow container works natively on both Intel and Apple Silicon Macs. TensorFlow will use CPU for all computations.

---

### 2.3. Linux

Full installation documentation here: [Install Docker Desktop on Linux](https://docs.docker.com/desktop/setup/install/linux)

Alternatively, you can install Docker Engine directly: [Install Docker Engine](https://docs.docker.com/engine/install/)

1. **Verify installation**
   - Open a terminal and run:
     ```bash
     docker --version
     ```

    The command should complete without error.

> **Note:** On Linux, you may need to add your user to the `docker` group to run Docker without `sudo`:
 ```bash
 sudo usermod -aG docker $USER
 ```
 Log out and back in for this change to take effect.

---

## 3. Getting started

Once you have Docker installed, starting a TensorFlow development environment from this repository is easy. Use it like a template to start new projects:

1. **Fork this repository** to create your own copy:
   - Click the **"Fork"** button in the top-right corner of this repository's GitHub page
   - Select your GitHub account as the destination
   - This creates your own copy where you can save your work and push changes

2. **Clone your forked repository:**

   On your local machine run:
   
   ```bash
   git clone https://github.com/<your-username>/tensorflow-CPU.git
   cd tensorflow-CPU
   ```
   > Replace `<your-username>` with your GitHub username

3. **Open the folder in VS Code:**
   ```bash
   code .
   ```

4. **Launch the dev container:**
   - When prompted, click **"Reopen in Container"**
   - Or press `F1` → Type "Dev Containers: Reopen in Container" → Press Enter

5. **Wait for the container to build** (this may take a few minutes on first run)

6. **Start coding!** Open and run `notebooks/test.ipynb` to verify your environment is working.

---

## 4. Keeping your fork updated

To sync your fork with the latest changes from this original repository:

```bash
# Add the original repo as an upstream remote (only needed once)
git remote add upstream https://github.com/gperdrizet/tensorflow-CPU.git

# Fetch and merge updates
git fetch upstream
git merge upstream/main
```

---

## TensorBoard

When the container starts, TensorBoard will start and port 6006 will be published automatically via Docker so that you can access it in a web browser on the host machine. The TensorBoard VS Code extension is also installed by default, so you can access TensorBoard from inside the container by finding `Python: Launch TensorBoard` in the command palette.

---

## Troubleshooting

- **Docker not starting:** Ensure virtualization is enabled in your BIOS settings (Windows/Linux) or that you have the correct Docker Desktop version for your Mac architecture
- **Permission denied errors on Linux:** Make sure you've added your user to the docker group and logged out/in
- **Container build fails:** Ensure you have a stable internet connection for downloading the TensorFlow image
- **Slow performance on MacOS:** Increase Docker Desktop's allocated memory and CPU in Preferences → Resources
- **Apple Silicon compatibility issues:** Ensure you're using the latest version of Docker Desktop which includes improved ARM64 support
