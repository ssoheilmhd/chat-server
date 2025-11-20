# Mattermost Self-Hosted with Voice Calls and Screen Sharing

A complete self-hosted Mattermost deployment with voice/video calling, screen sharing, and meeting capabilities, optimized for environments with restricted internet access (like Iran).

## 🚀 Features

- **Team Collaboration**: Full-featured Mattermost team edition
- **Voice & Video Calls**: Integrated calling functionality
- **Screen Sharing**: Desktop screen sharing capabilities
- **Thread Conversations**: Advanced threading for organized discussions
- **Self-Contained**: Works without external dependencies in restricted networks
- **Secure**: TLS-enabled reverse proxy with proper network isolation

## 🏗️ Architecture

This deployment uses Docker Compose with the following services:

- **PostgreSQL**: Database backend
- **Mattermost App**: Main application server
- **Coturn**: TURN/STUN server for WebRTC calls
- **Nginx**: Reverse proxy with SSL termination

## 📋 Prerequisites

- Docker and Docker Compose
- Domain names pointing to your server:
  - `chat.hpds.ir` (for Mattermost)
  - `turn.hpds.ir` (for TURN server)

## ⚙️ Configuration

### Environment Variables

Key configurations include:

- **Database**: PostgreSQL with custom credentials
- **Calls**: WebRTC configuration with STUN/TURN servers
- **Site URL**: `https://chat.hpds.ir`
- **Network**: Isolated Docker networks for security

### Ports Configuration

- `8065`: Mattermost web interface (localhost only)
- `443/80`: Nginx HTTPS/HTTP
- `3478`: Coturn STUN/TURN (TCP/UDP)
- `5349`: Coturn TLS
- `49152-49200`: Media ports for WebRTC
- `8443`: Calls signaling and media

## 🚀 Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/ssoheilmhd/chat-server.git
   cd mattermost-selfhosted
