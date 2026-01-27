# TensorFlow CPU development environment

A ready-to-use TensorFlow environment for CPU-only systems in VS Code. Designed for cross-platform support including MacOS, Linux, and Windows users who want a lightweight TensorFlow environment for learning, prototyping, or CPU-based inference.

## What's included

| Category | Versions |
|----------|----------|
| **ML** | TensorFlow 2.16 (CPU), Keras 3.3, Scikit-learn 1.4 |
| **Python** | Python 3.10, NumPy 1.24, Pandas 2.2, Matplotlib 3.10 |
| **Science** | SciPy 1.13 |
| **Tools** | JupyterLab, TensorBoard (auto-starts on port 6006) |

> **Have an NVIDIA GPU?** Use the GPU version instead: [gperdrizet/tensorflow-GPU](https://github.com/gperdrizet/tensorflow-GPU)

## Project structure

```
tensorflow-CPU/
├── .devcontainer/
│   └── devcontainer.json       # Dev container configuration
├── data/                       # Store datasets here
├── logs/                       # TensorBoard logs (auto-watched)
├── models/                     # Saved model files
├── notebooks/
│   ├── environment_test.ipynb  # Verify your setup
│   └── functions/              # Helper modules for notebooks
├── .gitignore
├── LICENSE
└── README.md
```

## Requirements

- **Docker** ([Windows](https://docs.docker.com/desktop/setup/install/windows-install) | [MacOS](https://docs.docker.com/desktop/setup/install/mac-install) | [Linux](https://docs.docker.com/desktop/setup/install/linux))
- **VS Code** with the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

> **Note:** This CPU-only TensorFlow container works natively on Intel, AMD, and Apple Silicon processors.

## Quick start

1. **Fork** this repository (click "Fork" button above)

2. **Clone** your fork:
   ```bash
   git clone https://github.com/<your-username>/tensorflow-CPU.git
   ```

3. **Open VS Code**

4. **Open Folder in Container** from the VS Code command pallet (Ctrl+shift+p), start typing `Open Folder in`...

5. **Verify** by running `notebooks/environment_test.ipynb`

## TensorBoard

TensorBoard starts automatically and is available at **http://localhost:6006**. Place your logs in the `logs/` directory.

## Adding Python packages

### Using pip directly

Install packages in the container terminal:

```bash
pip install <package-name>
```

> **Note:** Packages installed this way will be lost when the container is rebuilt.

### Using requirements.txt (recommended)

For persistent packages that survive container rebuilds:

1. **Create** a `requirements.txt` file in the repository root:
   ```
   scikit-image==0.22.0
   seaborn>=0.13.0
   plotly
   ```

2. **Update** `.devcontainer/devcontainer.json` to install packages on container creation by adding a `postCreateCommand`:
   ```json
   "postCreateCommand": "pip install -r requirements.txt"
   ```

3. **Rebuild** the container (`F1` → "Dev Containers: Rebuild Container")

Now your packages will be automatically installed whenever the container is created.

## Using as a template for new projects

You can use your fork as a starting point for new TensorFlow projects:

1. **Clone** your fork:
   ```bash
   git clone https://github.com/<your-username>/tensorflow-CPU.git
   ```

2. **Rename** the directory to your new project name:
   ```bash
   mv tensorflow-CPU my-new-project
   cd my-new-project
   ```

3. **Create a new repository** on GitHub for your project (don't initialize with README)

4. **Update the git remote** to point to your new repository:
   ```bash
   git remote set-url origin https://github.com/<your-username>/my-new-project.git
   ```

5. **Push** to your new repository:
   ```bash
   git push -u origin main
   ```

6. **Clean up** (optional): Remove the example notebooks, then add your own code:
   ```bash
   rm -rf notebooks/*.ipynb
   git add -A && git commit -m "Initial project setup"
   git push
   ```

Now you have a fresh TensorFlow CPU project with the dev container configuration ready to go!

## Keeping your fork updated

```bash
# Add upstream (once)
git remote add upstream https://github.com/gperdrizet/tensorflow-CPU.git

# Sync
git fetch upstream
git merge upstream/main
```

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Docker won't start | Enable virtualization in BIOS |
| Permission denied (Linux) | Add user to docker group, then log out/in |
| Container build fails | Check internet connection |
| Slow performance on MacOS | Increase Docker Desktop memory/CPU in Preferences → Resources |
