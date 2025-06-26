# Astra Setup - Comprehensive Server Infrastructure Automation

![Ansible](https://img.shields.io/badge/ansible-%231A1918.svg?style=for-the-badge&logo=ansible&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)

[![Last Commit](https://img.shields.io/github/last-commit/Enoal-Fauchille-Bolle/Astra-Setup?style=for-the-badge)](https://github.com/Enoal-Fauchille-Bolle/Astra-Setup/commits/master)
![Repo Size](https://img.shields.io/github/repo-size/Enoal-Fauchille-Bolle/Astra-Setup?style=for-the-badge)
![License](https://img.shields.io/github/license/Enoal-Fauchille-Bolle/Astra-Setup?style=for-the-badge)
![Lines of Code](https://tokei.rs/b1/github/Enoal-Fauchille-Bolle/Astra-Setup?style=for-the-badge)
[![wakatime](https://wakatime.com/badge/github/Enoal-Fauchille-Bolle/Astra-Setup.svg?style=for-the-badge)](https://wakatime.com/badge/github/Enoal-Fauchille-Bolle/Astra-Setup)

## 📋 Table of Contents

- [About the Project](#-about-the-project)
- [Features Overview](#-features-overview)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Usage](#-usage)
- [Configuration](#️-configuration)
- [Services Overview](#️-services-overview)
- [Project Structure](#-project-structure)
- [Contributing](#-contributing)
- [License](#-license)
- [Support](#-support)

## 🎯 About the Project

**Astra Setup** is a comprehensive Ansible automation project designed to deploy and manage a complete server infrastructure stack. This project automates the deployment of over 20 different services including databases, monitoring tools, container management platforms, backup solutions, and web applications on a Linux server.

### 🎯 Project Goals

- **Infrastructure as Code**: Maintain server configuration through version-controlled Ansible playbooks
- **Automated Deployment**: Deploy complex multi-service infrastructure with a single command
- **Service Integration**: Seamlessly integrate monitoring, backup, proxy, and application services
- **Security**: Implement secure configurations with encrypted secrets management
- **Scalability**: Design for easy service addition and modification

## ✨ Features Overview

### 🏗️ Base Infrastructure

- **System Configuration**: Timezone, hostname, swap, and system limits setup
- **User Management**: Automated user creation with sudo privileges and SSH key setup
- **Shell Environment**: ZSH configuration with custom aliases and MOTD
- **Package Management**: Essential packages installation and system updates

### 🌐 Proxy & Networking

- **Nginx Proxy Manager**: Web-based reverse proxy management (Port: 81)
- **SSL/TLS Management**: Automated certificate management and renewal

### 🗄️ Database Services

- **MariaDB**: MySQL-compatible database server with user management
- **PostgreSQL 16**: Advanced open-source relational database

### 📦 Storage & Backup Solutions

- **Nextcloud**: Self-hosted cloud storage platform (Port: 8002)
- **Filebrowser**: Web-based file manager (Port: 8001)
- **Duplicati**: Encrypted backup solution with cloud storage support (Port: 8200)

### 🐳 Container Management

- **Crafty Controller**: Minecraft server management platform (Port: 8443)
- **Portainer**: Docker container management interface (Port: 9443)
- **Jenkins**: CI/CD automation server with GitHub integration (Port: 8003)

### 📊 Monitoring & Logging

- **Glances**: System monitoring with web interface (Port: 61208)
- **NTFY**: Push notification service (Port: 7171)
- **Uptime Kuma**: Service uptime monitoring (Port: 3001)
- **Dozzle**: Docker container log viewer (Port: 3002)
- **Netdata**: Real-time system performance monitoring (Port: 19999)

### 🎛️ Dashboard & Utilities

- **OneTimeSecret**: Secure secret sharing platform (Port: 50000)
- **CasaOS**: Personal cloud OS dashboard (Port: 8081)
- **Homer**: Static service dashboard (Port: 8082)
- **Cockpit**: Web-based system administration (Port: 9090)

### 🚀 Applications

- **Discord Redirection**: Custom Discord invitation redirect service (Port: 50006)
- **Status Redirection**: Status page redirect service (Port: 50005)

## 📋 Prerequisites

### System Requirements

- **Target Server**: [Ubuntu 20.04+](https://ubuntu.com/download/server) or [Debian 11+](https://www.debian.org/distrib/) (x64)
- **Ansible Controller**: Linux/macOS machine with Ansible installed
- **Resources**: Minimum 4GB RAM, 20GB storage (recommended: 8GB RAM, 100GB storage)
- **Network**: SSH access to target server with sudo privileges

### Required Software

- **Python 3.8+**: [Download Python](https://www.python.org/downloads/)
- **Ansible 2.10+**: [Install Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- **SSH client**: Built-in on Linux/macOS, [PuTTY](https://www.putty.org/) for Windows
- **Git**: [Download Git](https://git-scm.com/downloads) (for cloning the repository)

## 🚀 Installation

### 1. Install Ansible

#### On Ubuntu/Debian

```bash
sudo apt update
sudo apt install ansible python3-pip
pip3 install ansible-vault
```

#### On CentOS/RHEL

```bash
sudo yum install epel-release
sudo yum install ansible python3-pip
pip3 install ansible-vault
```

#### On macOS

```bash
brew install ansible
pip3 install ansible-vault
```

#### Using pip (Universal)

```bash
pip3 install ansible ansible-vault
```

### 2. Clone the Repository

```bash
git clone <repository-url>
cd Astra-Setup
```

### 3. Configure SSH Access

```bash
# Configure SSH access to your target server
ssh-keygen -R YOUR_SERVER_IP
ssh-keyscan YOUR_SERVER_IP >> ~/.ssh/known_hosts

# Test SSH connection
ssh deploy@YOUR_SERVER_IP
```

### 4. Configure Ansible Vault

```bash
# Create vault password file
echo "your-vault-password" > .vault_pass
chmod 600 .vault_pass
```

## 🎮 Usage

### Quick Start

```bash
# Set up Ansible Vault password
echo "your-vault-password" > .vault_pass
chmod 600 .vault_pass

# Deploy the complete infrastructure
export ANSIBLE_VAULT_PASSWORD_FILE=.vault_pass
ansible-playbook -i inventory.ini playbooks/all.yml

# Deploy specific playbooks
ansible-playbook -i inventory.ini playbooks/databases.yml
ansible-playbook -i inventory.ini playbooks/monitoring_logs.yml
```

### Advanced Usage

#### Deploy Specific Service Categories

```bash
# Deploy only base system configuration
ansible-playbook -i inventory.ini playbooks/base.yml

# Deploy only monitoring services
ansible-playbook -i inventory.ini playbooks/monitoring_logs.yml

# Deploy only databases
ansible-playbook -i inventory.ini playbooks/databases.yml

# You can also use tags
ansible-playbook -i inventory.ini playbooks/all.yml --tags "nextcloud,jenkins"
```

#### Check Deployment Status

```bash
# Run system summary
ansible-playbook -i inventory.ini playbooks/summary.yml
```

#### Vault Management

```bash
# Encrypt new secrets
ansible-vault encrypt_string 'your-secret' --name 'variable_name'

# If you already have a vault file, you can use it directly
ansible-vault encrypt_string 'your-secret' --name 'variable_name' --vault-password-file .vault_pass
```

## ⚙️ Configuration

### 1. Inventory Configuration

Edit `inventory.ini` to specify your target server:

```ini
[astra]
your-server ansible_host=YOUR_SERVER_IP

[all:vars]
ansible_user=deploy
ansible_python_interpreter=/usr/bin/python3
```

### 2. Variables Configuration

Main configuration is in `group_vars/all.yml`. Key sections include:

#### Base Settings

```yaml
timezone: Europe/Paris
hostname: astra-setup
user_name: azerty
user_password_hashed: $1$...  # Generate with: openssl passwd -1
```

#### Service Enablement

```yaml
# Enable/disable services
nextcloud_enabled: true
jenkins_enabled: true
monitoring_enabled: true
```

#### Security Settings

All passwords and secrets are encrypted using Ansible Vault. To add new secrets:

```bash
ansible-vault encrypt_string 'your-password' --name 'service_password'
```

### 3. SSL/TLS Configuration

Services are configured to work with Nginx Proxy Manager for SSL termination. Configure your domains and certificates through the NPM web interface (port 81).

## 🛠️ Services Overview

| Category | Service | Port | Default Credentials | Purpose |
|----------|---------|------|-------------------|---------|
| Proxy | Nginx Proxy Manager | 81 | <admin@example.com> / changeme | Reverse proxy management |
| Storage | Nextcloud | 8002 | Configure on first run | Cloud storage |
| Storage | Filebrowser | 8001 | Configured via Ansible | File management |
| Backup | Duplicati | 8200 | Configured via Ansible | Backup management |
| Container | Portainer | 9443 | Configure on first run | Docker management |
| Container | Crafty | 8443 | Configure on first run | Minecraft servers |
| CI/CD | Jenkins | 8003 | Configured via Ansible | Build automation |
| Monitoring | Glances | 61208 | Configured via Ansible | System monitoring |
| Monitoring | Netdata | 19999 | Configured via Ansible | Performance monitoring |
| Monitoring | Uptime Kuma | 3001 | Configure on first run | Uptime monitoring |
| Logs | Dozzle | 3002 | Configured via Ansible | Container logs |
| Notifications | NTFY | 7171 | Configured via Ansible | Push notifications |
| Dashboard | CasaOS | 8081 | Configure on first run | System dashboard |
| Dashboard | Homer | 8082 | No authentication | Service dashboard |
| Secrets | OneTimeSecret | 50000 | admin@onetimesecret / [vault] | Secure sharing |
| System | Cockpit | 9090 | System users | System administration |

## 📁 Project Structure

```text
Astra-Setup/
├── ansible.cfg                 # Ansible configuration
├── inventory.ini              # Server inventory
├── group_vars/
│   └── all.yml               # Main configuration variables
├── playbooks/              # Ansible playbooks
│   ├── all.yml             # Master playbook
│   ├── base.yml            # Base system setup
│   ├── databases.yml       # Database services
│   ├── storage_backups.yml # Storage and backup
│   ├── container_management.yml # Container platforms
│   ├── monitoring_logs.yml # Monitoring services
│   ├── dashboard_secrets.yml # Dashboards and utilities
│   ├── applications.yml    # Custom applications
│   ├── proxy_networking.yml # Proxy configuration
│   └── summary.yml         # System summary
└── roles/                  # Ansible roles
    ├── base/              # Base system configuration
    ├── databases/         # Database roles
    ├── storage_backups/   # Storage and backup roles
    ├── container_management/ # Container platform roles
    ├── monitoring_logs/   # Monitoring service roles
    ├── dashboard_secrets/ # Dashboard and utility roles
    ├── applications/      # Custom application roles
    ├── proxy_networking/  # Networking roles
    └── summary/          # Summary and reporting roles
```

## 🔧 Troubleshooting

### Common Issues

#### SSH Connection Problems

```bash
# Reset SSH host keys
ssh-keygen -R YOUR_SERVER_IP
ssh-keyscan YOUR_SERVER_IP >> ~/.ssh/known_hosts

# Test SSH connection
ssh -i ~/.ssh/id_rsa deploy@YOUR_SERVER_IP
```

#### Vault Password Issues

```bash
# Ensure vault password file exists and has correct permissions
chmod 600 .vault_pass
```

#### Service Port Conflicts

Check the `group_vars/all.yml` file and modify port assignments if needed.

#### Docker Issues

```bash
# Restart Docker service on target server
ssh deploy@YOUR_SERVER_IP 'sudo systemctl restart docker'
```

### Logs and Debugging

```bash
# Run playbook with verbose output
ansible-playbook -i inventory.ini playbooks/all.yml -vvv

# Check specific service logs
ssh deploy@YOUR_SERVER_IP 'sudo journalctl -u docker'
```

## 🤝 Contributing

We welcome contributions to improve the Astra Setup project!

### How to Contribute

1. **Fork the Repository**

   ```bash
   git fork <repository-url>
   ```

2. **Create a Feature Branch**

   ```bash
   git checkout -b feature/amazing-feature
   ```

3. **Make Changes**
   - Add new services or improve existing ones
   - Update documentation
   - Fix bugs or security issues

4. **Test Your Changes**

   ```bash
   # Test on a development server
   ansible-playbook -i inventory.ini playbooks/all.yml --check
   ```

5. **Submit a Pull Request**
   - Provide a clear description of changes
   - Include testing information
   - Reference any related issues

### Development Guidelines

- **Code Style**: Follow Ansible best practices and YAML formatting
- **Documentation**: Update README.md and role documentation for new features
- **Security**: Ensure all secrets are properly encrypted with Ansible Vault
- **Testing**: Test changes on a clean server before submitting
- **Backwards Compatibility**: Maintain compatibility with existing deployments

### Reporting Issues

Please use the issue tracker to report:

- Bugs and errors
- Feature requests
- Documentation improvements
- Security vulnerabilities (please report privately)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

### Third-Party Licenses

This project deploys various open-source services, each with their own licenses:

- Docker containers and services maintain their respective licenses
- Ansible modules are licensed under GPL v3+
- See individual service documentation for specific licensing information

## 🆘 Support

### Documentation

- [Ansible Documentation](https://docs.ansible.com/)
- [Docker Documentation](https://docs.docker.com/)
- [Individual Service Documentation](#️-services-overview)

### Getting Help

1. **Check the Documentation**: Review this README and service-specific documentation
2. **Search Issues**: Look through existing GitHub issues
3. **Create an Issue**: Report bugs or request features via GitHub issues
4. **Community Support**: Join relevant community forums for the deployed services

---

**⭐ If this project helps you, please give it a star!**
