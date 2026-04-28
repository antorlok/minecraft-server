# 🎮 Antorlok's Minecraft Server

![Minecraft Version](https://img.shields.io/badge/Minecraft-1.20.1-brightgreen?style=flat-square&logo=minecraft) ![Server Type](https://img.shields.io/badge/Type-Forge-orange?style=flat-square) ![Docker](https://img.shields.io/badge/Powered_by-Docker-blue?style=flat-square&logo=docker)

A fully containerized, high-performance Minecraft Forge server running on Docker. This project is configured to automatically download required mods and recommend a custom resource pack upon player connection.

---

## ✨ Features

- **🐳 Dockerized:** Isolated, clean, and easily reproducible environment.
- **⚙️ Forge 1.20.1:** Mod-ready out of the box.
- **📥 Auto-Mod Download:** Automatically fetches mods from Modrinth on startup.
- **🎨 Auto-Resource Pack:** Prompts players to download the Faithful 32x texture pack.
- **🛡️ Automated Backups:** Includes a custom bash script for easy world preservation.
- **🔓 Offline Mode:** Configured for non-premium access (`ONLINE_MODE=FALSE`).
---

## Author

- **Name:** Andrés Tortolero(antorlok)
- **Email:** andres.tortolero06@gmail.com
- **Instagram:** [andress.tor](https://www.instagram.com/andress.tor?igsh=enRtNXVpNDkxNHNx&utm_source=qr)

---

## 📂 Project Structure

Make sure your project directory looks like this before running the server:

```text
📦 minecraft-server
 ┣ 📂 scripts
 ┃ ┗ 📜 backup.sh          # Backup automation script
 ┣ 📜 docker-compose.yml   # Docker orchestration file
 ┣ 📜 server.properties    # Minecraft server configuration
 ┗ 📜 README.md
```

(Note: The data and backups folders will be generated automatically).

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

- Docker & Docker Compose
- ngrok (Only if you want to host over the internet without port forwarding).
- Minecraft Forge 1.20.1 Client (All players must have this installed on their computers).

---

## 🚀 How to Run the Server

1. **Initialization**

Open your terminal in the project's root directory and run the following command to build and start the server in the background:

```bash
docker-compose up -d
```

The first startup will take a few minutes as Docker downloads Java, the Minecraft server files, Forge, and the specified mods.

2. **Monitor the Logs**

To ensure everything is loading correctly or to troubleshoot, you can watch the server console in real-time:

```bash
docker logs -f minecraft_server
```

(Press `Ctrl + C` to exit the logs view).

3. **Stopping the Server**

To safely stop the server, run:

```bash
docker-compose down
```

---

## 🔌 How to Connect

Depending on where your players are located, they will connect differently.

> ⚠️ CRITICAL REQUIREMENT: Every player MUST have the exact same mods installed in their local `.minecraft/mods` folder to join the server.

Required mods:

- Simply Swords
- AppleSkin
- Waystones
- Architectury API
- Cloth Config
- Balm

### Option A: Local Connection (You playing on the host machine)

1. Open Minecraft (Forge 1.20.1).
2. Go to `Multiplayer` > `Add Server`.

Server Address: `localhost:25565`

### Option B: LAN Connection (Players on your same Wi‑Fi/Network)

1. Find your local IPv4 address (e.g., `192.168.1.50`).
2. Give this IP to your friends on the same network.

Server Address: `192.168.1.50:25565`

### Option C: Internet Connection via ngrok (Players anywhere in the world)

If you cannot open ports on your router, ngrok creates a secure tunnel to your local server.

Install ngrok and authenticate your account using the token provided on their website.

Open a new terminal window and start a TCP tunnel on the Minecraft port:

```bash
ngrok tcp 25565
```

ngrok will display a Forwarding URL that looks like:

```
tcp://0.tcp.ngrok.io:12345
```

Give this address to your friends. They must enter everything after `tcp://` into Minecraft.

Server Address: `0.tcp.ngrok.io:12345`

(Note: Every time you restart ngrok, the address and port will change).

---

## 💾 Backups

Never lose your world! A custom shell script is provided to back up your data folder.

Make the script executable (You only need to do this once):

```bash
chmod +x scripts/backup.sh
```

Run the backup:

```bash
./scripts/backup.sh
```

This will compress your entire world and configuration into a `.tar.gz` file inside a newly created `backups` directory, tagged with the current date and time.

