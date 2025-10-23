# Bitcoin Purple Website

Updated and improved version of the Bitcoin Purple website: https://bitcoinpurpleblockchain.com

## 📋 Description

This is a static website for Bitcoin Purple, a decentralized Proof of Work cryptocurrency. The site is built with vanilla HTML, CSS, and JavaScript and is served using Caddy web server in a Docker container.

## 🚀 Local Development

### Prerequisites

Before getting started, make sure you have installed:

**For Docker-based development:**
- [Docker](https://www.docker.com/get-started) (version 20.10 or higher)
- [Docker Compose](https://docs.docker.com/compose/install/) (usually included with Docker Desktop)

**For Python-based development:**
- [Python](https://www.python.org/downloads/) (version 3.6 or higher recommended)

**General:**
- A code editor (VS Code, Sublime Text, etc.)

### Step-by-Step Guide

#### 1. Clone the Repository

```bash
git clone <repository-url>
cd purple-web-site
```

#### 2. Start the Development Server

There are two ways to start the local server:

##### Option A: With Docker Compose (Recommended)

```bash
# Build and start the container
docker-compose up --build

# Or run in background
docker-compose up -d --build
```

The site will be available at:
- **HTTP**: http://localhost
- **HTTPS**: https://localhost (with self-signed certificate)

##### Option B: Python HTTP Server (Simple Development)

For quick development without Docker, you can use Python's built-in HTTP server:

```bash
python -m http.server 8000
```

The site will be available at:
- **HTTP**: http://localhost:8000

**Note**: This method serves static files only and doesn't include HTTPS or the advanced features provided by Caddy (like security headers, compression, etc.).

#### 3. Development and File Modification

1. **Edit files**: You can modify any HTML, CSS, or JS file in the project directory

2. **Reload changes**:

   **For Docker-based development:**
   ```bash
   # Stop the container
   docker-compose down
   
   # Rebuild and restart
   docker-compose up --build
   ```

   **For Python HTTP server:**
   ```bash
   # Simply refresh your browser - changes are reflected immediately
   # No server restart needed for static file changes
   ```


#### 4. Useful Development Commands

**For Docker-based development:**
```bash
# View container logs
docker-compose logs -f

# Stop all services
docker-compose down

# Remove containers and volumes
docker-compose down -v

# Access running container
docker-compose exec web sh

# Check container status
docker-compose ps
```

**For Python HTTP server:**
```bash
# Start server on different port
python -m http.server 3000

# Start server and bind to specific address
python -m http.server 8000 --bind 127.0.0.1

# Check if Python is installed and version
python --version

# Stop server: Ctrl+C in the terminal
```

#### 5. Configuration Modification

- **Server**: Modify `Caddyfile` to change server configuration
- **Domains**: To test with custom domains, add entries to the system hosts file
- **Ports**: Modify `docker-compose.yml` to change exposed ports

#### 6. Debug and Troubleshooting

**Docker-related issues:**

**Issue**: Site doesn't load
```bash
# Check if container is running
docker ps

# Check logs for errors
docker-compose logs web
```

**Issue**: Changes not visible
```bash
# Rebuild image forcing cache refresh
docker-compose build --no-cache
docker-compose up
```

**Issue**: Permission errors (Linux/Mac)
```bash
# Ensure Docker has necessary permissions
sudo chown -R $USER:$USER .
```

**Python-related issues:**

**Issue**: Python command not found
```bash
# Try different Python commands
python3 -m http.server 8000
py -m http.server 8000

# Check Python installation
python --version
python3 --version
```

**Issue**: Port already in use
```bash
# Use a different port
python -m http.server 8080

# Or find and kill process using the port (Windows)
netstat -ano | findstr :8000
taskkill /PID <process_id> /F
```

**Issue**: Permission denied on port 80/443
```bash
# Use ports above 1024 (no admin rights needed)
python -m http.server 8000
```

### 🔧 Advanced Configuration

#### Development with Live Reload

For a better development experience with automatic reloading, you can mount local files:

```yaml
# Add to docker-compose.yml under volumes:
- .:/srv:ro  # Mount current directory as read-only
```

#### Environment Variables

You can customize behavior using environment variables:

```bash
# Set custom domain
export CADDY_HOST=localhost

# Start with custom configuration
docker-compose up
```

## 🌐 Production Deployment

For production deployment, the site is configured to:
- Serve on `bitcoinpurpleblockchain.net`
- Automatic redirect from `www.bitcoinpurpleblockchain.net`
- Automatic SSL certificates via Let's Encrypt
- Configured security headers

## 📝 Developer Notes

- The site is completely static, requires no database
- Uses Caddy to serve files and handle HTTPS
- File changes require container rebuild
- For optimal production performance, consider using a CDN

## 🤝 Contributing

1. Fork the project
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Test changes locally following this guide
4. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
5. Push to the branch (`git push origin feature/AmazingFeature`)
6. Open a Pull Request
