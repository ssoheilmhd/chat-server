🚀 Features
Team Collaboration: Full-featured Mattermost team edition

Voice & Video Calls: Integrated calling functionality

Screen Sharing: Desktop screen sharing capabilities

Thread Conversations: Advanced threading for organized discussions

Self-Contained: Works without external dependencies in restricted networks

Secure: TLS-enabled reverse proxy with proper network isolation

🏗️ Architecture
This deployment uses Docker Compose with the following services:

PostgreSQL: Database backend

Mattermost App: Main application server

Coturn: TURN/STUN server for WebRTC calls

Nginx: Reverse proxy with SSL termination

📋 Prerequisites
Docker and Docker Compose

Domain names pointing to your server:

chat.hpds.ir (for Mattermost)

turn.hpds.ir (for TURN server)

⚙️ Configuration
Environment Variables
Key configurations include:

Database: PostgreSQL with custom credentials

Calls: WebRTC configuration with STUN/TURN servers

Site URL: https://chat.hpds.ir

Network: Isolated Docker networks for security

Ports Configuration
8065: Mattermost web interface (localhost only)

443/80: Nginx HTTPS/HTTP

3478: Coturn STUN/TURN (TCP/UDP)

5349: Coturn TLS

49152-49200: Media ports for WebRTC

8443: Calls signaling and media

🚀 Quick Start
Clone the repository

bash
git clone <your-repo-url>
cd mattermost-selfhosted
Configure domain names
Update all instances of chat.hpds.ir and turn.hpds.ir with your actual domains.

Set up SSL certificates
Place your SSL certificates in the appropriate nginx configuration directory.

Deploy

bash
docker-compose up -d
Access the application
Navigate to https://your-domain.com in your browser.

🔧 Customization
TURN Server Configuration
Edit the Coturn environment variables in docker-compose.yml:

yaml
environment:
  - TURN_REALM=your-turn-domain.com
  - TURN_SECRET=your-shared-secret
Mattermost Configuration
Additional Mattermost settings can be modified in the environment variables or via the config.json volume mount.

🌐 Network Configuration
The setup uses two Docker networks:

mattermost-net: Internal communication between services

nginx: External-facing network for the reverse proxy

🔒 Security Features
Database credentials isolated from application

Internal-only Mattermost port binding

SSL termination at reverse proxy

Isolated Docker networks

Custom TURN server authentication

📁 Volume Structure
db-data: PostgreSQL database files

app-data: Mattermost application data

app-config: Mattermost configuration

app-plugins: Installed plugins

app-client-plugins: Client-side plugins

🛠️ Troubleshooting
Common Issues
Calls not working

Verify TURN server is accessible

Check firewall rules for UDP ports

Validate TURN shared key configuration

SSL issues

Ensure certificates are properly mounted in nginx

Verify domain names match certificate SANs

Database connection problems

Check PostgreSQL container status

Verify network connectivity between containers

Logs Inspection
bash
docker-compose logs app      # Mattermost logs
docker-compose logs coturn   # TURN server logs
docker-compose logs db       # Database logs
🔄 Maintenance
Backups
Regularly backup the Docker volumes:

bash
docker-compose stop
docker run --rm -v mattermost_db-data:/source -v $(pwd)/backups:/backup alpine tar czf /backup/db-backup-$(date +%Y%m%d).tar.gz -C /source .
docker-compose start
Updates
To update Mattermost version, modify the image tag in docker-compose.yml and redeploy.
