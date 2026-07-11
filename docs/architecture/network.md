# Arquitectura de red — CoreLab

## Diagrama

![Diagrama de arquitectura de red](../screenshots/network/CORELAB.png)

## Esquema de IPs

| Dispositivo / LXC | IP | Función |
|---|---|---|
| Router Xiaomi BE3600 | 192.168.1.1 | Puerta de enlace |
| Proxmox Node - server | 192.168.1.200 | Host de virtualización |
| LXC 100 — AdGuard Home | 192.168.1.201 | DNS + filtrado de publicidad |
| LXC 101 — BIND9 | 192.168.1.202 | Resolución DNS interna |
| LXC 102 — Nginx Proxy Manager | 192.168.1.203 | Proxy inverso + TLS |
| LXC 103 — Uptime Kuma | 192.168.1.204 | Monitorización de disponibilidad |
| LXC 104 — Vaultwarden | 192.168.1.205 | Gestor de contraseñas |
| LXC 105 — Prometheus + Grafana | 192.168.1.206 | Métricas y dashboards |

## Acceso remoto

- **WireGuard VPN**, IP interna del túnel: `10.0.0.1`
- Acceso vía DDNS + puerto no estándar (dato ofuscado en la documentación pública por seguridad)
- No se exponen puertos de servicios directamente a internet; todo el acceso remoto pasa por el túnel VPN

## Resolución DNS interna

- Dominio local: `*.traore.home`
- AdGuard Home actúa como DNS principal de la red, filtrando publicidad y trackers
- Las consultas del dominio interno (`traore.home`) se reenvían desde AdGuard Home a BIND9, que resuelve los registros internos
- El resto de tráfico DNS sale filtrado normalmente hacia internet

## Certificados TLS

- CA propia creada manualmente para el laboratorio
- Certificado wildcard para `*.traore.home`, gestionado y renovado desde Nginx Proxy Manager
- HTTPS forzado en todos los servicios expuestos vía proxy

## Monitorización de la red

- **Prometheus + Grafana** (LXC 105): recolecta métricas de cada LXC mediante `node_exporter`, instalado individualmente en cada contenedor
- **Uptime Kuma** (LXC 103): realiza checks periódicos de disponibilidad (ping/HTTP) sobre todos los servicios de la red

## Decisiones de diseño

- **Red plana (192.168.1.x)** en vez de VLANs segmentadas: [explica aquí el motivo — simplicidad para el tamaño actual del lab, facilidad de gestión con un único router doméstico, etc.]
- **WireGuard** sobre otras VPN (Tailscale, OpenVPN): [explica el motivo de tu elección]
- **Nginx Proxy Manager** como capa de acceso en vez de exponer puertos directamente: reduce superficie de ataque, centraliza la gestión de certificados y el control de acceso

## Problemas encontrados

- [Aquí documenta algún problema real: por ejemplo, la configuración del certificado wildcard, algún conflicto de puertos, la configuración del reenvío condicional en AdGuard, etc.]