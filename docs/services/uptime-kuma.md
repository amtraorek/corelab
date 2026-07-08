# Uptime Kuma

## ¿Qué es?

Uptime Kuma es una herramienta de monitorización de disponibilidad que
comprueba periódicamente si mis servicios están activos y accesibles,
avisando cuando alguno se cae.

## ¿Por qué lo elegí?

Lo elegí porque es una herramienta ligera, con interfaz web muy clara, y
pensada específicamente para monitorización de disponibilidad (uptime), a
diferencia de Prometheus + Grafana, que está más orientado a métricas de
rendimiento (CPU, RAM, disco). Quería tener una respuesta rápida y visual a
la pregunta "¿está caído o no?", sin depender de dashboards más complejos
para eso.

## Cómo encaja en mi infraestructura

- Desplegado en LXC 103 (Debian 12)
- Monitoriza cada servicio del laboratorio mediante comprobaciones HTTP(S)
  periódicas contra su URL (`*.traore.home`)
- Complementa a Prometheus + Grafana: Uptime Kuma responde a "¿está vivo?",
  Prometheus + Grafana responden a "¿cómo de bien está funcionando?"
- Accesible en `uptime.traore.home` vía Nginx Proxy Manager (HTTPS)

## Configuración relevante

- **Monitores configurados:** uno por cada servicio activo del laboratorio
  (AdGuard Home, BIND9, Nginx Proxy Manager, Vaultwarden, Prometheus/Grafana)
- **Intervalo de comprobación:** cada 60 segundos
- **Tipo de comprobación:** HTTP(S) contra la URL pública interna de cada servicio

## Capturas

![Panel de monitores en Uptime Kuma](../screenshots/uptime-kuma/dashboard.png)
*Panel principal mostrando el estado de todos los servicios monitorizados*

## Próximos pasos

- [ ] Configurar notificaciones (vía ntfy, una vez esté desplegado) cuando un servicio se caiga
- [ ] Añadir monitores para los nuevos servicios a medida que se vayan desplegando
- [ ] Configurar una página de estado pública (status page) para el laboratorio