# ROS 2 Humble Dev Container Starter

A complete, reproducible development environment for ROS 2 Humble Hawksbill, powered by VS Code Dev Containers and Docker.

This template is optimized for **WSLg (Windows Subsystem for Linux GUI)** but works on native Linux hosts as well.

## 🚀 Features

* **ROS 2 Humble Desktop Full** pre-installed.
* **GUI Support:** Pre-configured for WSLg/X11 forwarding (rviz2, gazebo, rqt).
* **Modern Tools Included:**
    * **Foxglove Bridge:** Connect [Foxglove Studio](https://foxglove.dev/) directly to your container.
    * **PlotJuggler:** The best time-series visualization tool for ROS.
* **Safe Defaults:**
    * Non-root user (`ros`) setup.
    * `ROS_LOCALHOST_ONLY=1` enabled by default for isolated simulations.
* **VS Code Integration:** Pre-configured extensions (C++, Python, CMake, ROS) and build tasks.

## 📋 Prerequisites

1.  **Docker Desktop** (Windows/Mac) or Docker Engine (Linux).
2.  **Visual Studio Code**.
3.  **Dev Containers** extension for VS Code.

> **Windows Users:** Ensure you are using WSL 2. WSLg is included in Windows 10 build 19044+ or Windows 11.

## 🛠️ Quick Start

1.  Clone this repository:
    ```bash
    git clone <your-repo-url> ros2_ws
    cd ros2_ws
    ```
2.  Open the folder in VS Code (`code .`).
3.  When prompted, click **"Reopen in Container"** (or press `F1` -> `Dev Containers: Reopen in Container`).
4.  Wait for the image to build.
5.  Open a terminal inside VS Code. It is ready to use!

## 📦 Workspace Setup

Once inside the container, create your workspace structure (if not present):

```bash
mkdir -p src
colcon build
source install/setup.bash
```

### Useful Commands

* **Build Workspace:** Press `Ctrl+Shift+B` (runs `colcon build --symlink-install`).
* **Launch PlotJuggler:**
```bash
ros2 run plotjuggler plotjuggler

```


* **Enable Foxglove Studio:**
Run the VS Code Task "foxglove: start bridge" or run manually:
```bash
ros2 launch foxglove_bridge foxglove_bridge_launch.xml

```


Then open Foxglove Studio on your host and connect to `ws://localhost:8765`.

## ⚙️ Configuration Notes

### Network Isolation

By default, the container is set to **Localhost Only**.

* `ROS_LOCALHOST_ONLY=1`: Nodes only talk within the container.
* `ROS_DOMAIN_ID=0`: Default domain.

To connect to a **physical robot** on your network:

1. Open `.devcontainer/devcontainer.json`.
2. Set `"ROS_LOCALHOST_ONLY": "0"`.
3. Change `ROS_DOMAIN_ID` to match your robot's ID.
4. Rebuild the container.

### User Permissions

The container runs as a non-root user (`ros`) with `sudo` privileges. Files created in the mounted workspace will belong to your host user ID (mapped automatically), preventing permission issues on your host machine.
