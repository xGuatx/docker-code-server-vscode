# Code-Server - VS Code in Browser

Docker deployment of [code-server](https://github.com/coder/code-server), enabling Visual Studio Code to run in a web browser.

## Description

Run VS Code on any machine and access it from a browser. Perfect for remote development, Chromebooks, tablets, or when you need a consistent development environment.

## Prerequisites

- Docker
- Docker Compose

## Installation

```bash
# Start code-server
docker-compose up -d
```

## Usage

Access code-server at: `http://localhost:8443`

### Default Configuration

```yaml
services:
  code-server:
    image: lscr.io/linuxserver/code-server:latest
    ports:
      - "8443:8443"
    volumes:
      - /path/to/code-server/config:/config
    environment:
      - PASSWORD=${CODE_SERVER_PASSWORD}
```

### Password Setup

Set password via environment variable:
```bash
CODE_SERVER_PASSWORD=your_secure_password docker-compose up -d
```

Or configure in `.env` file (copy from `.env.example`):
```env
CODE_SERVER_PASSWORD=your_secure_password
CODE_SERVER_SUDO_PASSWORD=your_secure_sudo_password
```

## Environment Variables

| Variable | Description |
|----------|-------------|
| `CODE_SERVER_PASSWORD` | Main password for web interface |
| `CODE_SERVER_HASHED_PASSWORD` | Optional: Hashed password (overrides PASSWORD) |
| `CODE_SERVER_SUDO_PASSWORD` | Sudo password for terminal |
| `CODE_SERVER_SUDO_PASSWORD_HASH` | Optional: Hashed sudo password |
| `CODE_SERVER_PROXY_DOMAIN` | Custom domain for proxy |

## Features

- Full VS Code experience in browser
- Extension support
- Integrated terminal
- Git integration
- Multi-user support (with authentication)

## Configuration

### Custom Extensions

Mount extensions directory:
```yaml
volumes:
  - ./extensions:/config/extensions
```

### Persistent Settings

User settings persist in the `/config` directory.

## Security Notes

**Important**:
- Always set a strong password
- Use HTTPS in production (reverse proxy recommended)
- Restrict access via firewall/VPN
- Keep code-server image updated

## Common Commands

```bash
# Start
docker-compose up -d

# Stop
docker-compose down

# View logs
docker-compose logs -f

# Restart
docker-compose restart
```

## Troubleshooting

### Permission Issues
```bash
# Fix permissions on volumes
sudo chown -R $(id -u):$(id -g) ./config
```

### Port Already in Use
Change port in `docker-compose.yml`:
```yaml
ports:
  - "9443:8443"  # Use port 9443 instead
```

## Use Cases

- Remote development
- Consistent dev environment across devices
- Teaching/training environments
- Development on low-powered devices
- Pair programming

## Resources

- [Official Repository](https://github.com/coder/code-server)
- [LinuxServer.io Image](https://docs.linuxserver.io/images/docker-code-server)
- [Documentation](https://coder.com/docs/code-server)

## License

Personal project - Private use

---

**Note**: code-server is developed by Coder. This is just a deployment configuration.
