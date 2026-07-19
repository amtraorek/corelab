# ATK CoreLab

> Infraestructura personal de homelab — Proxmox, servicios autoalojados, monitorización y seguridad.

**Estado:** 🟡 En progreso — iniciado el 01/07/2026

![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![Proxmox](https://img.shields.io/badge/Proxmox-E57000?style=flat&logo=proxmox&logoColor=white)
![AdGuard Home](https://img.shields.io/badge/AdGuard_Home-68BC71?style=flat&logo=adguard&logoColor=white)
![BIND9](https://img.shields.io/badge/BIND9-CB2D2D?style=flat)
![NPM](https://img.shields.io/badge/Nginx_Proxy_Manager-269639?style=flat&logo=nginxproxymanager&logoColor=white)
![Uptime Kuma](https://img.shields.io/badge/Uptime_Kuma-5CDD8B?style=flat&logo=uptimekuma&logoColor=white)
![Vaultwarden](https://img.shields.io/badge/Vaultwarden-175DDC?style=flat&logo=vaultwarden&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat&logo=grafana&logoColor=white)
---

## ¿En que consiste?

CoreLab es mi homelab personal, donde diseño, despliego y mantengo una
infraestructura self-hosted (local) sobre mi propio hardware. El objetivo es construir
infraestructura real cubriendo administración de
sistemas, redes, monitorización y seguridad — documentando cada decisión
que voy tomando por el camino.


---

## Hardware

| Componente | Detalle |
|---|---|
| Equipo | HP ProDesk 600 G4 Mini |
| CPU | Intel Core i7-8700T |
| RAM | 32 GB DDR4 |
| Almacenamiento | ~440 GB NVMe |
| Hipervisor | Proxmox VE 9.2 |

<p align="center">
  <img src="screenshots/hardware/prodesk-exterior.png" width="45%" />
  <img src="screenshots/hardware/interior-prodesk.png" width="45%" />
</p>



![Resumen Proxmox](screenshots/hardware/proxmox-overview.png)
*Uso de recursos actual de todas las LXC*

---

## Arquitectura

![Diagrama](screenshots/network/corelab-diagram.png)

Todos los servicios están detrás de un dominio interno (`traore.home`) con
certificado wildcard autofirmado, resuelto localmente mediante AdGuard Home +
BIND9 y expuestos mediante Nginx Proxy Manager con HTTPS forzado.

Más detalle en [`docs/architecture/network.md`](docs/architecture/network.md).

---

## Servicios actuales

| Servicio | Función | Estado |
|---|---|---|
| AdGuard Home | DNS + bloqueo de publicidad/trackers | ✅ |
| BIND9 | Resolución DNS interna (`traore.home`) | ✅ |
| Nginx Proxy Manager | Proxy inverso + HTTPS | ✅ |
| Uptime Kuma | Monitorización de disponibilidad | ✅ |
| Vaultwarden | Gestor de contraseñas autoalojado | ✅ |
| Prometheus + Grafana | Métricas y dashboards | ✅ |

Cada servicio tiene su propia documentación en [`docs/services/`](docs/services/),
explicando por qué se eligió, cómo se integra con el resto del laboratorio, y
la utilidad dentro de la infraestructura.

---

## Estructura del repositorio

```text
CoreLab/
├── README.md
├── docs/
│   ├── architecture/
│   │   ├── network.md
│   │   └── hardware.md
│   └── services/
│       ├── adguard.md
│       ├── bind9.md
│       ├── nginx-proxy-manager.md
│       ├── uptime-kuma.md
│       ├── vaultwarden.md
│       └── prometheus-grafana.md
├── screenshots/
│   ├── hardware/
│   ├── network/
│   ├── adguard/
│   ├── bind9/
│   ├── nginx-proxy-manager/
│   ├── uptime-kuma/
│   ├── vaultwarden/
│   └── prometheus-grafana/
└── LICENSE
```

---

## Roadmap

### 🌐 Red y acceso
- [x] AdGuard Home — DNS + bloqueo de publicidad
- [x] BIND9 — DNS interno (`traore.home`)
- [x] Nginx Proxy Manager — proxy inverso + HTTPS
- [x] WireGuard — VPN (en el nodo Proxmox)
- [ ] Headscale — VPN mesh de contigencia

### 🔑 Identidad y seguridad
- [x] Vaultwarden
- [ ] Authelia
- [ ] Wazuh
- [ ] CrowdSec
- [ ] Suricata

### 📊 Monitorización
- [x] Uptime Kuma 
- [x] Prometheus + Grafana 
- [ ] ntfy — notificaciones push

### ⚙️ Automatización
- [ ] Ansible 
- [ ] AWX 

### 💾 Almacenamiento y multimedia
- [ ] TrueNAS SCALE 
- [ ] Nextcloud 
- [ ] Immich 
- [ ] Jellyfin 

### 🖥️ Panel central
- [ ] Homarr — dashboard 
---

*Última actualización: 19/07/2026*