<<<<<<< HEAD
# H1 Locomotion: Standalone IsaacLab Extension for Unitree H1 on Rough Terrain

![Demo: H1 Locomotion in Rough Terrain](demos/h1_rough_play.gif)

---

## Overview

This repository is a **standalone extension based on IsaacLab** for simulating and training locomotion of the Unitree H1 humanoid robot in rough terrain. It leverages IsaacLab's modular, manager-based environment design, enabling advanced reinforcement learning (RL) workflows and flexible robot control.

**Key Features:**
- Standalone, modular extension for IsaacLab
- Focused on Unitree H1 humanoid locomotion in challenging environments
- Manager-based environment design for easy customization and RL integration
- Ready-to-use RL training and evaluation scripts

---

## Installation

### 1. System Requirements

> **System Requirements:**  
> Please review the [IsaacLab System Requirements](https://isaac-sim.github.io/IsaacLab/main/source/setup/installation/index.html) to ensure your system is compatible.

![System Requirements](demos/sys_req.png)

### 2. Install Isaac Sim

Follow the official [Isaac Sim installation guide](https://docs.isaacsim.omniverse.nvidia.com/latest/installation/quick-install.html).

### 3. Install IsaacLab

Follow the [IsaacLab installation guide](https://isaac-sim.github.io/IsaacLab/main/source/setup/installation/index.html).  
Conda installation is recommended for ease of use.

### 4. Install this Extension

Clone this repository **outside** your IsaacLab directory, then install in editable mode:

```bash
python -m pip install -e source/h1_locomotion
```

---

## Manager-Based Environments

Environments in IsaacLab bring together different aspects of the simulation—such as the scene, observation and action spaces, and reset events—to create a coherent interface for various applications.  
Manager-based environments are implemented as `envs.ManagerBasedEnv` and `envs.ManagerBasedRLEnv` classes.  
- `ManagerBasedRLEnv` is tailored for RL tasks and includes rewards, terminations, curriculum, and command generation.
- `ManagerBasedEnv` is for traditional robot control and does not include RL-specific features.

Learn more in the [IsaacLab Manager-Based Environment Tutorial](https://isaac-sim.github.io/IsaacLab/main/source/tutorials/03_envs/create_manager_base_env.html).

---

## Quick Start

### 1. List Available Environments

```bash
python scripts/list_envs.py
```

### 2. Train a Policy

Example (RSL-RL, 4096 environments, headless):

```bash
python3 scripts/rsl_rl/train.py --task Template-H1-Locomotion-v0 --num_envs 4096 --headless
```

### 3. Play a Trained Policy

```bash
python3 scripts/rsl_rl/play.py --task Template-H1-Locomotion-Play-v0 --num_envs 16 
```

---

## Author

Niraj Pudasaini  
nirajpudasaini13@gmail.com
=======
# Template for Isaac Lab Projects

## Overview

This project/repository serves as a template for building projects or extensions based on Isaac Lab.
It allows you to develop in an isolated environment, outside of the core Isaac Lab repository.

**Key Features:**

- `Isolation` Work outside the core Isaac Lab repository, ensuring that your development efforts remain self-contained.
- `Flexibility` This template is set up to allow your code to be run as an extension in Omniverse.

**Keywords:** extension, template, isaaclab

## Installation

- Install Isaac Lab by following the [installation guide](https://isaac-sim.github.io/IsaacLab/main/source/setup/installation/index.html).
  We recommend using the conda installation as it simplifies calling Python scripts from the terminal.

- Clone or copy this project/repository separately from the Isaac Lab installation (i.e. outside the `IsaacLab` directory):

- Using a python interpreter that has Isaac Lab installed, install the library in editable mode using:

    ```bash
    # use 'PATH_TO_isaaclab.sh|bat -p' instead of 'python' if Isaac Lab is not installed in Python venv or conda
    python -m pip install -e source/h1_locomotion

- Verify that the extension is correctly installed by:

    - Listing the available tasks:

        Note: It the task name changes, it may be necessary to update the search pattern `"Template-"`
        (in the `scripts/list_envs.py` file) so that it can be listed.

        ```bash
        # use 'FULL_PATH_TO_isaaclab.sh|bat -p' instead of 'python' if Isaac Lab is not installed in Python venv or conda
        python scripts/list_envs.py
        ```

    - Running a task:

        ```bash
        # use 'FULL_PATH_TO_isaaclab.sh|bat -p' instead of 'python' if Isaac Lab is not installed in Python venv or conda
        python scripts/<RL_LIBRARY>/train.py --task=<TASK_NAME>
        ```

    - Running a task with dummy agents:

        These include dummy agents that output zero or random agents. They are useful to ensure that the environments are configured correctly.

        - Zero-action agent

            ```bash
            # use 'FULL_PATH_TO_isaaclab.sh|bat -p' instead of 'python' if Isaac Lab is not installed in Python venv or conda
            python scripts/zero_agent.py --task=<TASK_NAME>
            ```
        - Random-action agent

            ```bash
            # use 'FULL_PATH_TO_isaaclab.sh|bat -p' instead of 'python' if Isaac Lab is not installed in Python venv or conda
            python scripts/random_agent.py --task=<TASK_NAME>
            ```

### Set up IDE (Optional)

To setup the IDE, please follow these instructions:

- Run VSCode Tasks, by pressing `Ctrl+Shift+P`, selecting `Tasks: Run Task` and running the `setup_python_env` in the drop down menu.
  When running this task, you will be prompted to add the absolute path to your Isaac Sim installation.

If everything executes correctly, it should create a file .python.env in the `.vscode` directory.
The file contains the python paths to all the extensions provided by Isaac Sim and Omniverse.
This helps in indexing all the python modules for intelligent suggestions while writing code.

### Setup as Omniverse Extension (Optional)

We provide an example UI extension that will load upon enabling your extension defined in `source/h1_locomotion/h1_locomotion/ui_extension_example.py`.

To enable your extension, follow these steps:

1. **Add the search path of this project/repository** to the extension manager:
    - Navigate to the extension manager using `Window` -> `Extensions`.
    - Click on the **Hamburger Icon**, then go to `Settings`.
    - In the `Extension Search Paths`, enter the absolute path to the `source` directory of this project/repository.
    - If not already present, in the `Extension Search Paths`, enter the path that leads to Isaac Lab's extension directory directory (`IsaacLab/source`)
    - Click on the **Hamburger Icon**, then click `Refresh`.

2. **Search and enable your extension**:
    - Find your extension under the `Third Party` category.
    - Toggle it to enable your extension.

## Code formatting

We have a pre-commit template to automatically format your code.
To install pre-commit:

```bash
pip install pre-commit
```

Then you can run pre-commit with:

```bash
pre-commit run --all-files
```

## Troubleshooting

### Pylance Missing Indexing of Extensions

In some VsCode versions, the indexing of part of the extensions is missing.
In this case, add the path to your extension in `.vscode/settings.json` under the key `"python.analysis.extraPaths"`.

```json
{
    "python.analysis.extraPaths": [
        "<path-to-ext-repo>/source/h1_locomotion"
    ]
}
```

### Pylance Crash

If you encounter a crash in `pylance`, it is probable that too many files are indexed and you run out of memory.
A possible solution is to exclude some of omniverse packages that are not used in your project.
To do so, modify `.vscode/settings.json` and comment out packages under the key `"python.analysis.extraPaths"`
Some examples of packages that can likely be excluded are:

```json
"<path-to-isaac-sim>/extscache/omni.anim.*"         // Animation packages
"<path-to-isaac-sim>/extscache/omni.kit.*"          // Kit UI tools
"<path-to-isaac-sim>/extscache/omni.graph.*"        // Graph UI tools
"<path-to-isaac-sim>/extscache/omni.services.*"     // Services tools
...
```
>>>>>>> a3698ff0ae82105ade49d2d0912b32f2a1a976b6
