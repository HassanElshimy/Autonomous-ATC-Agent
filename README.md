# TRACON-Level AI Agent for Air Traffic Control Simulation

## Project Overview
This project aims to develop a high-fidelity AI agent capable of demonstrating TRACON-level decision-making within a realistic air traffic control simulation environment. The focus is on building core functionality and showcasing intelligence through technical milestones.

## Current Status
**Phase 1: Building the Simulation Sandbox**
**Step 1: Simulator Setup (BlueSky)**
I am currently setting up the foundational simulation environment using BlueSky.

## Motivation
My interest lies in applying advanced AI techniques to critical real-world systems, specifically in enhancing safety and efficiency within air traffic management. This project serves as a practical demonstration of building complex intelligent systems.

## Technologies Used
* **Core:** Python
* **Simulation:** BlueSky Simulator
* **Version Control:** Git, GitHub

## Installation & Setup

To get this project running, follow these steps:

1.  **Clone the Repository:**
    First, clone this main project repository:
    ```bash
    git clone [https://github.com/HassanElshimy/Autonomous-ATC-Agent.git](https://github.com/HassanElshimy/Autonomous-ATC-Agent.git)
    cd Autonomous-ATC-Agent
    ```

2.  **Initialize and Update BlueSky Submodule:**
    This project uses the BlueSky simulator as a Git submodule. Initialize and update it:
    ```bash
    git submodule update --init --recursive
    ```

3.  **Create and Activate Python Virtual Environment (using Python 3.11):**
    It's recommended to use Python 3.11 for compatibility. Create and activate a virtual environment:
    ```bash
    python3.11 -m venv venv
    source venv/bin/activate # On Windows (Command Prompt): .\venv\Scripts\activate.bat
                             # On Windows (PowerShell): .\venv\Scripts\Activate.ps1
    ```

4.  **Install BlueSky Dependencies:**
    Navigate into the BlueSky submodule directory and install its Python requirements. This might take a few minutes.
    ```bash
    cd simulator/bluesky
    pip install -e .[full] --upgrade
    ```

5.  **Apply Compatibility Patch for NumPy:**
    *(Important: BlueSky's network code (specifically `npcodec.py`) uses `np.fromstring` in a way that is deprecated and removed in recent NumPy versions (e.g., NumPy 2.x, which installs with Python 3.11). To ensure compatibility and prevent a crash, a small one-line patch is required.)*
    * Open the file `simulator/bluesky/bluesky/network/npcodec.py` in your preferred text editor.
    * Go to `line 15`.
    * Change `np.fromstring` to `np.frombuffer`.
    * The line should change from:
        ```python
        return np.fromstring(o[b'data'], dtype=np.dtype(o[b'type'])).reshape(o[b'shape'])
        ```
        to:
        ```python
        return np.frombuffer(o[b'data'], dtype=np.dtype(o[b'type'])).reshape(o[b'shape'])
        ```
    * Save the file.
    * (Optional, but recommended for local consistency) After applying the patch, re-install BlueSky in editable mode to ensure the changes are picked up by the Python environment:
        ```bash
        pip install -e .[full] --upgrade --no-deps
        ```
        *(You can now omit the `--no-deps` if you ran `pip install -e .[full] --upgrade` just before this, as dependencies are already installed and the patch is small).*

6.  **Run the Simulator:**
    From the `simulator/bluesky` directory (make sure your `(venv)` is active):
    ```bash
    python3 BlueSky.py
    ```
    Once the BlueSky GUI appears, locate its internal console. In that console, type `IC demo` and press Enter to start a demo simulation.

---

## Follow My Journey
Stay tuned for updates on this project! I'll be documenting progress, challenges, and insights here on GitHub, as well as on Medium.
