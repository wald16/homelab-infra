# 🏠 Homelab Infrastructure

This repository documents my **self-hosted homelab**, fully managed with Docker Compose.  
It includes applications, monitoring, automation, dashboards, file sharing, and secure remote access via VPN.

---

## 🚀 Services Included

- **WireGuard VPN** → Secure remote access to internal services  
- **Portainer** → Docker management UI  
- **Netdata** → Monitoring & metrics  
- **Dashy** → Central dashboard for all apps  
- **Samba** → File sharing service  
- **ROMM + MariaDB** → Media/game manager  
- **n8n + Cloudflare Tunnel** → Workflow automation & secure webhooks  
- **ntfy** → Push notifications  
- **Nginx** → Privacy and redirect pages  
- **Entradas System** → Ticketing system (backend, frontend, Postgres DB)  

---

## 📂 Repository Structure

```
apps.compose.yml   # Applications stack
vpn.compose.yml    # WireGuard VPN setup
.env.example       # Example environment variables (placeholders only)
README.md          # Documentation
screenshots/       # UI captures
```

---

## 🔑 Environment Variables

All sensitive values are externalized in `.env`.  
See `.env.example` for placeholders and required variables.


## 🖼️ Architecture

### 🔒 Access & Security
```mermaid
flowchart TB
    %% ==== Acceso Externo ====
    subgraph EXT[🌍 External Access]
        U[Users / Clients]
        CF1[Cloudflare Tunnel → Entradas]
        CF2[Cloudflare Tunnel → n8n]
        CF3[Cloudflare Tunnel → Instagram Bot]
        WG[WireGuard VPN]
    end

    U -->|VPN| WG
    U -->|HTTPS| CF1
    U -->|HTTPS| CF2
    U -->|HTTPS| CF3

    %% ==== Red Interna ====
    subgraph NET[🏠 Internal Network]
        subgraph APPS[🛠️ Applications]
            R[ROMM] --> MDB[(MariaDB)]
            EB[Entradas Backend] --> PG[(Postgres DB)]
            EB --> FE[Frontend Apps]
        end

        subgraph MON[📊 Monitoring]
            D[Dashy Dashboard]
            P[Portainer]
            ND[Netdata]
        end

        subgraph EXP[🌐 Services Exposed]
            N8N[n8n Automation]
            NG[Nginx Page - Instagram Bot]
            FE2[Entradas Frontend / Backend]
        end
    end

    %% Conexiones túneles
    CF1 --> FE2
    CF2 --> N8N
    CF3 --> NG

    %% Conexión interna
    WG --> NET

```


## 📸 Screenshots

### Dashy Dashboard
![Dashy](screenshots/dashy.png)

### Portainer
![Portainer](screenshots/portainer.png)

### Netdata Metrics
![Netdata](screenshots/netdata.png)

### n8n Workflow
![n8n](screenshots/n8n.png)

---

## ⚠️ Security Notes

- This repository does **not** include real configs or credentials.  
- `.env` with sensitive values is ignored via `.gitignore`.  
- `.env.example` is provided as a safe template.  

---

## 📚 Skills Demonstrated

- **Infrastructure as Code** with Docker Compose  
- **VPN setup** with WireGuard  
- **Secure tunneling** with Cloudflare  
- **Monitoring & observability** with Netdata & healthchecks  
- **Service orchestration** across databases, apps, and dashboards  
- **Workflow automation** with n8n
- **Workflow automation** with n8n  
