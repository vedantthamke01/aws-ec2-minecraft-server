# 🚀 AWS EC2 Minecraft Server Deployment (Free Tier)

## 📌 Overview
Deployment of a Minecraft Java Server on AWS EC2 (Ubuntu 24.04 LTS) using Free Tier (t3.micro – 1GB RAM) for hands-on cloud infrastructure practice.

---

## 🏗 Infrastructure Details

- **Cloud Provider:** AWS  
- **Service:** EC2  
- **Instance Type:** t3.micro (Free Tier)  
- **OS:** Ubuntu 24.04 LTS  
- **Java Version:** OpenJDK 21  
- **Ports:** 22 (SSH), 25565 (Minecraft)

---

# ⚙ Setup & Deployment Commands

## 1️⃣ Update System

```bash
sudo apt update && sudo apt upgrade -y
```

---

## 2️⃣ Install Java 21

```bash
sudo apt install openjdk-21-jre -y
java -version
```

> Minecraft 1.21+ requires Java 21 or newer.

---

## 3️⃣ Create Server Directory

```bash
mkdir ~/minecraft
cd ~/minecraft
```

Place `server.jar` inside this directory.

---

## 4️⃣ Start Server (Manual Mode)

```bash
java -Xmx550M -Xms550M -jar server.jar nogui
```

### JVM Memory Configuration
- `-Xmx550M` → Maximum heap memory  
- `-Xms550M` → Initial heap memory  

Optimized for AWS Free Tier (1GB RAM).

---

## 5️⃣ Accept Minecraft EULA

```bash
nano eula.txt
```

Change:

```
eula=false
```

To:

```
eula=true
```

Restart the server after saving.

---

## 6️⃣ Open Port 25565 (If Needed)

If using UFW:

```bash
sudo ufw allow 25565
```

Also ensure port **25565** is open in AWS Security Group.

---

# ⚙ systemd Service Configuration

## 1️⃣ Create Start Script

```bash
nano /home/ubuntu/minecraft/start.sh
```

```bash
#!/bin/bash
cd /home/ubuntu/minecraft
/usr/bin/java -Xmx550M -Xms550M -jar server.jar nogui
```

Make executable:

```bash
chmod +x /home/ubuntu/minecraft/start.sh
```

---

## 2️⃣ Create Service File

```bash
sudo nano /etc/systemd/system/minecraft.service
```

```ini
[Unit]
Description=Minecraft Java Server
After=network.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/minecraft
ExecStart=/home/ubuntu/minecraft/start.sh
Restart=on-failure
RestartSec=10
KillSignal=SIGINT

[Install]
WantedBy=multi-user.target
```

---

## 3️⃣ Enable & Start Service

```bash
sudo systemctl daemon-reload
sudo systemctl enable minecraft
sudo systemctl start minecraft
sudo systemctl status minecraft
```

---

## 4️⃣ Manage Service

Stop server:

```bash
sudo systemctl stop minecraft
```

Restart server:

```bash
sudo systemctl restart minecraft
```

---

## 🧠 Key Learning Outcomes

- EC2 provisioning and configuration  
- Security Group firewall management  
- SSH key-based authentication  
- Linux service management (systemd)  
- JVM memory optimization under constrained resources  
- Network and authentication troubleshooting  

---

⚠ This deployment was performed on AWS Free Tier (1GB RAM).  
Suitable for learning and light usage (1–2 players), not production workloads.
