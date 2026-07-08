# Nginx Proxy Manager

## ¿Qué es?

Nginx Proxy Manager (NPM) es un proxy inverso con interfaz web que gestiona
el acceso a todos los servicios de mi laboratorio a través de un único punto
de entrada, aplicando HTTPS a cada uno de ellos.

## ¿Por qué lo elegí?

Lo elegí por encima de configurar Nginx a mano porque ofrece una interfaz web
sencilla para gestionar certificados y hosts proxy, sin tener que editar
ficheros de configuración manualmente cada vez que añado un servicio nuevo.
Esto acelera mucho el proceso de publicar un nuevo servicio: solo necesito
crear un host proxy nuevo desde la interfaz y asociarle su certificado.

## Cómo encaja en mi infraestructura

- Desplegado en LXC 102 (Debian 12)
- Es el punto de entrada único para acceder a todos los servicios mediante
  subdominios del dominio interno (`*.traore.home`)
- Cada servicio tiene un "Proxy Host" configurado en NPM, con "Force SSL"
  activado
- Usa un certificado wildcard autofirmado, generado con una CA interna propia,
  válido para `*.traore.home`
- BIND9 resuelve cada subdominio a la IP de NPM, que redirige internamente al
  puerto correspondiente de cada LXC

```text
Cliente (navegador)
       │
       ▼
BIND9 resuelve *.traore.home → IP de Nginx Proxy Manager
       │
       ▼
Nginx Proxy Manager (HTTPS, certificado wildcard)
       │
       ├── adguard.traore.home    → LXC 100
       ├── vaultwarden.traore.home → LXC 104
       ├── monitor.traore.home     → LXC 105
       └── ...
```

## Configuración relevante

- **Certificado:** wildcard autofirmado (`*.traore.home`), emitido por una CA interna propia
- **Force SSL:** activado en todos los proxy hosts
- **Un proxy host por servicio**, cada uno apuntando a la IP interna y puerto de su LXC correspondiente

## Capturas

![Listado de proxy hosts](../screenshots/nginx-proxy-manager/hosts.png)
*Listado de servicios publicados a través de Nginx Proxy Manager*

## Problemas encontrados

Al generar el certificado wildcard inicial tuve problemas de confianza del
navegador porque el SAN (Subject Alternative Name) no incluía correctamente
todos los subdominios necesarios. Tuve que regenerar el certificado con la CA
interna, asegurándome de incluir el wildcard completo en el SAN.

## Próximos pasos

- [ ] Integrar autenticación centralizada vía Authelia para los servicios que lo requieran
- [ ] Revisar reglas de acceso/cortafuegos para servicios sensibles (Vaultwarden, etc.)