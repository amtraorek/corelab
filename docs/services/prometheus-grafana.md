# Prometheus + Grafana

## ¿Qué es?

Prometheus es un sistema de monitorización que recolecta y almacena datos
(CPU, RAM, disco, red...) de los servidores de mi infraestructura. Grafana se
conecta a esos datos y los consigue transformar en dashboards visuales, permitiendo visualizar el estado de cada servidor con sus mètricas correspondientes.

## ¿Por qué lo elegí?
Uno de los principales dilemas a la hora del monitoraje fue elegir la herramienta correcta. Lo elegí principalmente por encima de **Zabbix** porque actualmente es la
herramienta más usada para monitorización en entornos cloud y Kubernetes,
tecnologías que están muy demandas a día de hoy. Tambíen cuenta con más soporte y una
comunidad más activa que esta en crecimiento, lo que también facilita encontrar
documentación y resolver problemas. 


## Cómo encaja en mi infraestructura

Desplegado en la LXC 105 (Debian 12), junto a los tres componentes del stack:

- **Node Exporter** corre en la propia LXC y expone las métricas del sistema
  (CPU, RAM, disco, red) en el puerto 9100.
- **Prometheus** recoge esas métricas cada 15 segundos  y las
  almacena en su base de datos interna, disponible en el puerto 9090.
- **Grafana** se conecta a Prometheus (puerto 9090) como fuente de datos y los convierte en
  dashboards, disponibles en el puerto 3000.

El servicio está publicado a través de Nginx Proxy Manager con HTTPS, accesible
en la direccion `monitor.traore.home`, usando el mismo certificado  interno que el
resto de servicios del homelab.

Actualmente monitoriza únicamente la propia LXC 105 mediante Node Exporter, y el nodo prinicpal `server`; aún falta añadir Node Exporter al resto de LXCs para tener visibilidad de toda la infraestructura, y un exporter específico para el propio nodo Proxmox (PVE Exporter).

## Configuración importante

- **Dashboard importado:** [Node Exporter Full (ID 1860)](https://grafana.com/grafana/dashboards/1860),
  el dashboard de referencia de la comunidad para visualizar métricas de
  Node Exporter — incluye CPU, memoria, disco, red y presión del sistema
- **Acceso:** `monitor.traore.home` (HTTPS vía Nginx Proxy Manager)



## Ejemplos

![Dashboard de Node Exporter Full en Grafana](../../screenshots/prometheus-grafana/dashboard.png)
*Dashboard "Node Exporter Full" mostrando CPU, RAM, disco y red en tiempo real*

#