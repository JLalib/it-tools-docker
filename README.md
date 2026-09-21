# 🛠️ IT-Tools Docker

[![GitHub Stars](https://img.shields.io/github/stars/corentinth/it-tools?style=for-the-badge&logo=github)](https://github.com/corentinth/it-tools)
[![Docker Pulls](https://img.shields.io/docker/pulls/corentinth/it-tools?style=for-the-badge&logo=docker)](https://hub.docker.com/r/corentinth/it-tools)
[![License](https://img.shields.io/github/license/corentinth/it-tools?style=for-the-badge)](https://github.com/corentinth/it-tools/blob/main/LICENSE)
[![GitHub Release](https://img.shields.io/github/v/release/corentinth/it-tools?style=for-the-badge&logo=github)](https://github.com/corentinth/it-tools/releases)

## 📋 Descripción general

**IT-Tools** es una colección autohospedada de **100+ herramientas web para developers e IT professionals** que centraliza todos esos pequeños utilitarios que normalmente buscarías en sitios random por internet. Convertidores, formateadores, generadores, parseadores, validadores — todo en un solo lugar, todo corriendo en tu navegador, todo client-side sin backend.

**Ventaja crucial:** NO envía datos a ningún servidor. Todo procesa localmente en tu navegador. Esto significa puedes pegar de forma segura credenciales, keys privadas, SQL queries, tokens — sin miedo a que alguien esté capturando datos.

Desarrollado con **Vue 3 + TypeScript**, imagen Docker ultra-ligera (~20 MB), multilingüe (30+ idiomas), dark mode nativo y responsive para mobile/tablet/desktop.

## ✨ Características principales

- 🔐 **Crypto/Security (15+ tools):** Hash, Bcrypt, Encrypt/Decrypt, UUID, ULID, Token Gen, BIP39, Argon2, HMAC
- 🔄 **Converters (25+ tools):** Base64, Color, Roman Numerals, Case, Binary, Unicode, YAML/JSON/TOML, XML/JSON, Markdown→HTML
- 🌐 **Web Development (20+ tools):** URL Encoder/Decoder, JWT Parser, OTP Generator, HTML Entities, Basic Auth Gen, QR Code, HTTP Status Codes, Safelink Decoder
- ⚙️ **Dev Tools (20+ tools):** Docker Run→Compose, SQL Prettify, JSON Diff, Crontab Gen, Regex Tester, YAML Viewer, Git Memo
- 📝 **Text/Strings (15+ tools):** Lorem Ipsum, Text Stats, Emoji Picker, ASCII Art, String Obfuscator, Text Diff, Numeronym
- 🌍 **Network/Utilities (10+ tools):** IP Calculator, IBAN Parser, Phone Parser, Email Normalizer, Slug Generator, Device Info
- 📊 **Math/Science (5+ tools):** Unit Converter, Temperature Converter, Percentage Calculator, Benchmark Builder
- 🔒 **Client-side only:** Todo procesa en tu navegador. Cero backend. Cero tracking. Cero data sent anywhere
- 🔍 **Búsqueda instantánea:** Escribe para filtrar 100+ tools en tiempo real
- ⭐ **Favoritos:** Marca tools que usas frecuentemente. Aparecen al tope de la lista
- 🌐 **Multi-idioma (30+):** Español, inglés, francés, alemán, chino, japonés, portugués, ucraniano, vietnamita, etc.
- 🌙 **Responsive + Dark mode:** Desktop, tablet, móvil. Dark/Light mode. Clean UI

## 📋 Requisitos del sistema

- **Docker** instalado y funcionando
- **RAM:** 128 MB mínimo (casi nada)
- **Espacio:** Imagen ~20 MB
- **Puerto:** 80 o 8080 (configurable)
- **Internet:** Para acceder al dashboard (no requiere conectividad hacia afuera)
- **Navegador moderno** (cualquiera)
- **Ultra-ligero:** Perfecto para Raspberry Pi, máquinas viejas, VPS $2/mes. Sin overhead

## 🐳 Instalación

### Opción 1: Docker run simple

```bash
docker run -d \
  --name it-tools \
  --restart unless-stopped \
  -p 8080:80 \
  corentinth/it-tools:latest
```

### Opción 2: Docker Compose (recomendado)

```bash
cat > docker-compose.yml << 'EOF'
version: '3.8'

services:
  it-tools:
    image: corentinth/it-tools:latest
    # image: ghcr.io/corentinth/it-tools:latest  # GitHub Container Registry
    container_name: it-tools
    restart: unless-stopped
    ports:
      - "8080:80"
EOF

docker compose up -d
```

## ⚙️ Configuración

1. **Puerto host:** Modifica `"8080:80"` en `docker-compose.yml` si necesitas otro puerto (ej: `"3000:80"`)
2. **Registry alternativo:** Descomenta `ghcr.io/corentinth/it-tools:latest` para usar GitHub Container Registry
3. **Red personalizada:** Añade `networks:` si usas reverse proxy (Caddy, Nginx Proxy Manager, Traefik)
4. **Variables de entorno:** No requiere variables obligatorias — todo se configura desde la UI
5. **Persistencia:** **NO requiere volúmenes** — IT-Tools es stateless, cero datos que persistir

## 🚀 Primeros pasos

1. **Clona o crea** el archivo `docker-compose.yml` con el contenido de arriba
2. **Levanta el contenedor:** `docker compose up -d`
3. **Verifica logs:** `docker logs -f it-tools` (debe mostrar servidor nginx en puerto 80)
4. **Accede al dashboard:** Abre `http://localhost:8080` en tu navegador
5. **¡Listo!** Sin login, sin setup. Empieza a usar cualquiera de las 100+ herramientas inmediatamente

## 💡 Casos de uso

- **Developers diarios:** Stop buscando herramientas online. Todo en IT-Tools
- **DevOps/SRE:** Debugging Docker commands, parsing logs, encoding secrets
- **Security professionals:** Hash generation, encryption, JWT validation, todo offline
- **Homelabbers:** Run localmente. No confíes en herramientas web random
- **Edu/Teams:** Deploy en intranet. Todos acceden sin permisos internet
- **Offline-first:** Funciona sin conexión a internet una vez cargado (PWA ready)

## 🔒 Acceso remoto seguro

### Con Caddy (recomendado - HTTPS automático)

```caddyfile
tools.tudominio.com {
    reverse_proxy localhost:8080
}
```

### Con Nginx Proxy Manager

1. Añade Proxy Host → `tools.tudominio.com` → `http://it-tools:80`
2. Habilita SSL → Let's Encrypt → Force SSL
3. Accede via `https://tools.tudominio.com`

> **Nota:** Todo sigue siendo client-side. Datos nunca llegan al servidor. El reverse proxy solo sirve los assets estáticos.

## 🛠️ Gestión y mantenimiento

```bash
# Ver logs en tiempo real
docker logs -f it-tools

# Reiniciar contenedor
docker restart it-tools

# Actualizar a versión más reciente
docker pull corentinth/it-tools:latest
docker compose down
docker compose up -d

# Monitorear consumo de recursos
docker stats it-tools
# Verás: mínimo CPU, ~20-50MB RAM
```

### Notas de storage

**IT-Tools NO requiere persistencia de datos.** Es stateless. Borra el contenedor = todo igual. Perfecto para immutable infrastructure.

## 📝 Licencia

Este proyecto es un wrapper de despliegue para **IT-Tools** (Copyright © Corentin Thomasset), licenciado bajo **GPL-3.0**.

- [Licencia original](https://github.com/corentinth/it-tools/blob/main/LICENSE)
- [Repositorio oficial](https://github.com/corentinth/it-tools)

---

> 📖 **Guía completa y tutorial:** [Cómo instalar IT-Tools - Colección de herramientas para developers autohospedada en Docker](https://genbyte.blogspot.com/2026/07/como-instalar-it-tools-coleccion-de.html)