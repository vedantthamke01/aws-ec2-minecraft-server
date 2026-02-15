⚙️ Setup & Deployment Commands
This document outlines the core commands used to configure and deploy the Minecraft server on AWS EC2 (Ubuntu 24.04 LTS).

1️⃣ System Preparation
Update package lists to ensure the latest repositories are available:

sudo apt update && sudo apt upgrade -y
2️⃣ Install Java Runtime (Required for Minecraft 1.21+)
Minecraft 1.21 requires Java 21.

sudo apt install openjdk-21-jre -y
Verify installation:

java -version
3️⃣ Create Server Directory
mkdir ~/minecraft
cd ~/minecraft
4️⃣ Start Minecraft Server (Manual Execution)
Optimized for AWS Free Tier (1GB RAM):

java -Xmx550M -Xms550M -jar server.jar nogui
JVM Memory Configuration:
-Xmx550M → Maximum heap memory

-Xms550M → Initial heap memory

This allocation ensures stable performance within constrained resources.

5️⃣ Enable Auto-Start Using systemd
Reload systemd:

sudo systemctl daemon-reload
Enable service at boot:

sudo systemctl enable minecraft
Start service manually:

sudo systemctl start minecraft
Check service status:

sudo systemctl status minecraft
6️⃣ Stop Server Safely
Inside server console:

stop
Or via systemd:

sudo systemctl stop minecraft