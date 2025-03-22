# manage-mariadb

A simple Bash interface for installing and configuring MariaDB with SSL support on Debian-based systems.

## Description

`manage-mariadb` is a lightweight Bash utility that simplifies common MariaDB server administration tasks, including:

- Secure server configuration with SSL/TLS (via Let's Encrypt)
- User and database lifecycle management
- Remote access control
- Enforced SSL policies
- Smart certificate renewal with change detection

## Installation

1. Download the script:
   ```bash
   sudo curl -o /usr/sbin/manage-mariadb https://raw.githubusercontent.com/cselzer/manage-mariadb/main/manage-mariadb
   ```

2. Make it executable:
   ```bash
   sudo chmod +x /usr/sbin/manage-mariadb
   ```

---

## Usage

```bash
manage-mariadb [command] [options]
```

### Available Commands

- `configure` — Install and configure MariaDB with SSL
- `users` — Manage MariaDB users
- `renew-ssl` — Renew and apply new SSL certificates if they've changed
- `toggle-remote` — Enable or disable remote access
- `toggle-force-ssl` — Enforce or disable SSL-only connections
- `install-renewal-hook` — Set up automatic cert renewal for MariaDB
- `update` — Download and replace with the latest version from GitHub

---

### 🔧 Initial Setup

```bash
sudo manage-mariadb configure
```

This will:

- Install MariaDB server if not already present
- Obtain and configure Let's Encrypt SSL certificates
- Set up secure default config
- Generate a secure root password
- Store credentials safely in `/root/.my.cnf`

---

### 👤 User Management

```bash
# View all user options
sudo manage-mariadb users help

# Create user + matching database
sudo manage-mariadb users create myuser

# Reset user's password
sudo manage-mariadb users reset myuser

# List users
sudo manage-mariadb users list

# View user privileges
sudo manage-mariadb users grants myuser

# Drop user and database (with prompt)
sudo manage-mariadb users drop myuser

# Force drop without prompt
sudo manage-mariadb users drop myuser --force
```

---

### 🔐 SSL Management

```bash
# Update SSL certs if they've changed and restart MariaDB
sudo manage-mariadb renew-ssl

# Install Let's Encrypt renewal hook for auto-renewal
sudo manage-mariadb install-renewal-hook

# Toggle SSL enforcement (require_secure_transport)
sudo manage-mariadb toggle-force-ssl
```

---

### 🌐 Remote Access

```bash
# Toggle between local-only (127.0.0.1) and remote access (0.0.0.0)
sudo manage-mariadb toggle-remote
```

---

### 📦 Updating

```bash
# Download the latest version of the script
sudo manage-mariadb update
```

---

## Requirements

- Debian 12 (Bookworm) or higher (including Raspberry Pi OS based on Debian 12)
- Root/sudo privileges
- Hostname resolving to the server's public IP (e.g., `dbserver.example.com`)

---

## License

MIT License © 2025 [Cody Selzer](https://github.com/cselzer)
