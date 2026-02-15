# ⚙️ Setup & Deployment Commands

This document outlines the commands used to configure and deploy a Minecraft Java Server on AWS EC2 (Ubuntu 24.04 LTS).

---

## 1️⃣ System Update

Update package repositories:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## 2️⃣ Install Java 21 (Required for Minecraft 1.21+)

Install OpenJDK 21:

```bash
sudo apt install openjdk-21-jre -y
```

Verify installation:

```bash
java -version
```

> Minecraft 1.21+ requires Java 21 or newer.

---

## 3️⃣ Create Server Directory

```bash
mkdir ~/minecraft
cd ~/minecraft
```

Place your `server.jar` file inside this directory.

---

## 4️⃣ Start Minecraft Server (Manual Mode)

Optimized for AWS Free Tier (1GB RAM):

```bash
java -Xmx550M -Xms550M -jar server.jar nogui
```

### 🧠 JVM Memory Configuration

- `-Xmx550M` → Maximum heap memory  
- `-Xms550M` → Initial heap memory  

This allocation ensures stable performance within constrained AWS Free Tier resources.

---

## 5️⃣ Enable Auto-Start Using systemd

Create a systemd service file:

```bash
sudo nano /etc/systemd/system/minecraft.service
```

Paste the following configuration:

```ini
[Unit]
Description=Minecraft Server
After=network.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/minecraft
ExecStart=/usr/bin/java -Xmx550M -Xms550M -jar server.jar nogui
Restart=on-failure
KillSignal=SIGINT

[Install]
WantedBy=multi-user.target
```

Reload systemd configuration:

```bash
sudo systemctl daemon-reload
```

Enable service at boot:

```bash
sudo systemctl enable minecraft
```

Start the service:

```bash
sudo systemctl start minecraft
```

Check service status:

```bash
sudo systemctl status minecraft
```

---

## 6️⃣ Stop Server Safely

From inside the Minecraft console:

```bash
stop
```

Or using systemd:

```bash
sudo systemctl stop minecraft
```

---

## 7️⃣ Accept Minecraft EULA (Required)

After first run, edit the EULA file:

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

Save and restart the server.

---

## 8️⃣ (Optional) Open Port 25565

If using UFW firewall:

```bash
sudo ufw allow 25565
```

Also ensure port **25565** is open in your AWS EC2 Security Group.

---

✅ Your Minecraft Java server is now configured for AWS EC2 deployment.
