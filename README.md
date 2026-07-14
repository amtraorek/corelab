# ATK CoreLab

> Infraestructura personal de homelab — Proxmox, servicios autoalojados, monitorización y seguridad.

**Estado:** 🟡 En progreso — iniciado el 01/07/2026

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

![Hardware ATK CoreLab](docs/screenshots/hardware/interior-prodesk.png)
*HP ProDesk 600 G4 Mini corriendo Proxmox VE*

![Resumen Proxmox](docs/screenshots/hardware/proxmox-overview.png)
*Uso de recursos actual de todas las LXC*

---

## Arquitectura

![Diagrama](docs/screenshots/network/CORELAB.png)

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
ATK-CoreLab/
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

*Última actualización: 12/07/2026*