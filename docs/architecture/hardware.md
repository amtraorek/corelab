# Hardware — CoreLab

## Equipo

| Componente | Detalle |
|---|---|
| **Equipo** | HP ProDesk 600 G4 Mini |
| **CPU** | Intel Core i7-8700T (6 núcleos / 12 hilos) |
| **RAM** | 32 GB DDR4 3200MHz (2x16GB Dual Channel) |
| **Almacenamiento** | ~512 GB NVMe Micron PCIe 3x4 |
| **Hipervisor** | Proxmox VE 9.2 |

## Por qué elegí este hardware

Elegí un **HP ProDesk 600 G4 Mini** principalmente porque, a diferencia de un servidor tradicional, tiene un consumo energético muy bajo (35W), y porque ya tenía experiencia previa trabajando con este modelo durante mis prácticas.

Opté por un **i7-8700T** para aprovechar 6 núcleos y 12 hilos, más potencia que otros modelos equivalentes de mini PC de la misma gama.

Reutilicé un NVMe que ya tenía para aprovechar la máxima velocidad posible como disco principal del servidor. Próximamente añadiré un segundo disco dedicado a guardar datos y archivos, para no sobrecargar el disco principal del sistema con almacenamiento de datos.

Elegí 32GB de RAM pensando en los distintos servicios que tengo previsto ir añadiendo a futuro, dejando margen de crecimiento.

## Imágenes

![Hardware físico — HP ProDesk 600 G4 Mini](../screenshots/hardware/interior-prodesk.png)
*Interior del HP ProDesk 600 G4 Mini*

![Resumen de recursos en Proxmox](../screenshots/hardware/proxmox-overview.png)
*Uso de CPU, RAM y disco del nodo con todos los LXC en marcha*

## Dificultades y problemas

La principal dificultad a la hora de decidir el hardware fue encontrar un modelo con una CPU de 6 núcleos, necesaria para poder correr varios servicios simultáneamente sin quedarme corto de potencia.

La otra gran dificultad fue conseguir 32GB de RAM. Debido a la fuerte demanda de memoria RAM por parte de los centros de datos (CPD) para IA, el precio subió bastante, lo que me obligó a pasar varias semanas buscando en el mercado de segunda mano hasta encontrar un módulo a buen precio.

---

*Última actualización: 14/07/2026*