## Quick start guide for Windows 10

Note #1: If you have an existing Python 3.6+ installation (on any operating system or virtual machine), you can use that. Optionally use a virtual environment, anaconda or such in order to not mess with existing packages.

Note #2: Instructions might work on Windows 11 as well, but they haven't been tested.

 
## Option 1: Windows 10 using Windows Subsystem for Linux

1. If you are using Windows 10, it is recommended to use the Windows Subsystem for Linux (scroll down the page for install instructions, or watch the video below). Ubuntu versions 18.04 LTS or 20.04 LTS should both work (22.04 LTS might work, but it has not been tested). WSL1 is enough for our purposes.

2. Then use the Ubuntu terminal to install Python3 and pip with: sudo apt update && sudo apt install python3 python3-pip
   - You need to input the password you set up during the initial installation here.

3. Install required Python packages in Ubuntu terminal with: python3 -m pip install ed25519 Crypto pycryptodome sortedcontainers flask flask-cors

4. Download the project files (link) and extract them to a folder of your choice, e.g., C:\blockchain

5. In a terminal, navigate to the folder where you extracted the project files. Example: if the files are located in C:\blockchain, then use cd /mnt/c/blockchain (WSL) or cd c:\blockchain (Windows terminal)
   - Note that the miner is located in the blockchain subfolder and the client is in the blockchain_client subfolder.

6. Run the scripts as described in the instructions .pdf
 

Video tutorial for step 1 and basic usage:   
https://youtu.be/5RTSlby-l9w



## Option 2: Windows 10 using Python and C++ Build Tools

Note, this is not officially supported, so there are only rough guidelines if you want to attempt this route.

Install Python 3

Try to install required modules (pip install ed25519 Crypto pycryptodome sortedcontainers flask flask-cors)  
If module installation fails and asks for C++ Build Tools, install Microsoft C++ Build Tools ("Desktop development with C++" with default settings should work). Try installing modules again.

Continue from step 4 of option 1.

 

## Option 3: Install or use a Linux virtual machine of your choice and run the scripts there

If you are choosing this option, we trust you can adapt the above instructions to your needs.
