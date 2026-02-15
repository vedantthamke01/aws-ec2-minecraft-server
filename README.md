# aws-ec2-minecraft-server
Deploying and configuring a Minecraft Java server on AWS EC2 (Free Tier)
# 🚀 AWS EC2 Minecraft Server (Free Tier Deployment)

## 📌 Project Overview

This project demonstrates the deployment and configuration of a Minecraft Java Server on AWS EC2 using the Free Tier (t3.micro – 1GB RAM).

The goal was to gain hands-on experience with cloud infrastructure, networking, Linux server management, and performance optimization in a constrained environment.

---

## 🏗 Architecture (Logical Flow)

Client (Minecraft)  
⬇  
Internet  
⬇  
AWS Security Group (Port 22 & 25565)  
⬇  
EC2 Instance (Ubuntu 24.04 LTS)  
⬇  
Minecraft Java Server  

---

## ⚙ Infrastructure Details

- **Cloud Provider:** AWS  
- **Service:** EC2  
- **Instance Type:** t3.micro (Free Tier)  
- **Operating System:** Ubuntu 24.04 LTS  
- **Java Version:** OpenJDK 21  
- **Ports Used:**  
  - 22 → SSH  
  - 25565 → Minecraft Server  

---

## 🔐 Security Configuration

- Configured Security Group rules:
  - SSH access (Port 22)
  - Custom TCP (Port 25565)
- Used SSH key-based authentication (.pem)
- Avoided exposing credentials or sensitive data

---

## 🚀 Deployment Steps (High-Level)

1. Provisioned EC2 instance
2. Connected via SSH
3. Installed Java 21
4. Deployed Minecraft server
5. Modified `server.properties`
6. Optimized JVM memory (`-Xmx550M -Xms550M`)
7. Configured systemd service for auto-start

Detailed commands available in:
- `setup-commands.md`
- `systemd-service.md`

---

## ⚠ Performance Considerations

This server runs on AWS Free Tier (1GB RAM).  
Due to resource constraints:

- Suitable for 1–2 players
- Limited chunk loading performance
- Not intended for production workloads

This deployment was created for learning and experimentation purposes.

---

## 🧠 Key Learning Outcomes

- AWS EC2 provisioning and management  
- Security Group firewall configuration  
- SSH key authentication  
- Linux service management using systemd  
- JVM tuning under limited resources  
- Troubleshooting networking and authentication issues  

---

## 📎 Repository Structure

```
.
├── README.md
├── setup-commands.md
├── systemd-service.md
└── screenshots/
```

---

## 📌 Disclaimer

No private keys, credentials, or sensitive information are included in this repository.
