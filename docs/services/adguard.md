# AdGuard Home

## ¿Qué es?

AdGuard Home es un servidor DNS que bloquea publicidad, rastreadores y
dominios maliciosos a nivel de red, sin necesidad de instalar nada en cada
dispositivo individualmente. Todos los dispositivos de mi red doméstica pasan
por él para resolver dominios.

## ¿Por qué lo elegí?

Lo elegí por encima de Pi-hole (la alternativa más conocida) principalmente
porque tiene una interfaz más moderna y cuidada, y porque incluye soporte
para DNS-over-HTTPS/DNS-over-TLS de serie, sin depender de plugins o
configuración adicional. Además, funciona como servidor DNS propio sin
depender de `dnsmasq` como hace Pi-hole, lo que simplifica la integración con
mi DNS interno (BIND9).

## Cómo encaja en mi infraestructura

- Desplegado en LXC 100 (Debian 12)
- Actúa como servidor DNS primario de toda la red doméstica
- Las consultas de dominios internos (`*.traore.home`) se reenvían a BIND9
- El resto de consultas se resuelven contra DNS upstream público
- Accesible en `adguard.traore.home` vía Nginx Proxy Manager (HTTPS)

```text
Clientes de la red
       │
       ▼
AdGuard Home (bloqueo + filtrado)
       │
       ├── *.traore.home → BIND9 (DNS interno)
       └── resto de dominios → DNS upstream (Internet)
```

## Configuración relevante

- **Consultas DNS gestionadas:** en torno a 49.000 consultas/24h en la red doméstica
- **Bloqueo por filtros:** ~17% de las consultas totales bloqueadas (publicidad y rastreadores)
- **Tiempo medio de procesamiento:** 10 ms
- **Dominios más bloqueados:** dominios de telemetría y tracking (analytics, logs de apps de streaming)
- **Clientes monitorizados:** cada dispositivo de la red aparece identificado por IP, con estadísticas individuales de peticiones

## Capturas

![Panel de control de AdGuard Home](../screenshots/adguard/dashboard.png)
*Panel principal con estadísticas de consultas DNS, filtros aplicados y clientes más frecuentes*

## Próximos pasos

- [ ] Añadir DNS-over-HTTPS (DoH) para cifrar las consultas salientes
- [ ] Integrar autenticación con Authelia cuando esté desplegado
- [ ] Revisar y ajustar listas de bloqueo según falsos positivos detectados
- [ ] Configurar clientes con perfiles distintos (móvil, TV, IoT)