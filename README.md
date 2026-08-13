# 🛠️ IT-Tools Docker

[![GitHub Stars](https://img.shields.io/github/stars/corentinth/it-tools?style=for-the-badge&logo=github)](https://github.com/CorentinTh/it-tools)
[![Docker Pulls](https://img.shields.io/docker/pulls/corentinth/it-tools?style=for-the-badge&logo=docker)](https://hub.docker.com/r/corentinth/it-tools)
[![License](https://img.shields.io/github/license/corentinth/it-tools?style=for-the-badge)](https://github.com/CorentinTh/it-tools/blob/main/LICENSE)
[![GitHub Release](https://img.shields.io/github/v/release/corentinth/it-tools?style=for-the-badge&logo=github)](https://github.com/CorentinTh/it-tools/releases)

---

## 📋 Descripción general

**IT-Tools** es una colección autohospedada de **100+ herramientas web para developers e IT professionals** que centraliza todos esos pequeños utilitarios que normalmente buscarías en sitios random por internet. Convertidores, formateadores, generadores, parseadores, validadores — todo en un solo lugar, todo corriendo en tu navegador, todo client-side sin backend.

**Ventaja crucial:** NO envía datos a ningún servidor. Todo procesa localmente en tu navegador. Esto significa que puedes pegar de forma segura credenciales, keys privadas, SQL queries, tokens — sin miedo a que alguien esté capturando datos.

Desarrollado con **Vue 3 + TypeScript**, imagen Docker ultra-ligera (~20 MB), multilingüe (30+ idiomas), dark mode nativo y responsive.

---

## ✨ Características principales

- 🔐 **Crypto/Security (15+ tools):** Hash, Bcrypt, Encrypt/Decrypt, UUID, ULID, Token Gen, BIP39, Argon2, HMAC
- 🔄 **Converters (25+ tools):** Base64, Color, Roman Numerals, Case, Binary, Unicode, YAML/JSON/TOML, XML/JSON, Markdown→HTML
- 🌐 **Web Development (20+ tools):** URL Encoder/Decoder, JWT Parser, OTP Generator, HTML Entities, Basic Auth Gen, QR Code, HTTP Status Codes, Safelink Decoder
- ⚙️ **Dev Tools (20+ tools):** Docker Run→Compose, SQL Prettify, JSON Diff, Crontab Generator, Regex Tester, YAML Viewer, Git Memo
- 📝 **Text/Strings (15+ tools):** Lorem Ipsum, Text Stats, Emoji Picker, ASCII Art, String Obfuscator, Text Diff, Numeronym
- 🌍 **Network/Utilities (10+ tools):** IP Calculator, IBAN Parser, Phone Parser, Email Normalizer, Slug Generator, Device Info
- 📊 **Math/Science (5+ tools):** Unit Converter, Temperature Converter, Percentage Calculator, Benchmark Builder
- 🔒 **100% Client-side:** Cero backend, cero tracking, cero datos enviados a servidores
- 🔍 **Búsqueda instantánea:** Filtra 100+ tools en tiempo real
- ⭐ **Favoritos:** Marca tools que usas frecuentemente, aparecen al tope
- 🌐 **Multi-idioma (30+):** Español, inglés, francés, alemán, chino, japonés, portugués, ucraniano, vietnamita, etc.
- 🌙 **Responsive + Dark mode:** Desktop, tablet, móvil. Dark/Light mode automático

---

## 📋 Requisitos del sistema

- **Docker** instalado y funcionando
- **RAM:** 128 MB mínimo (casi nada)
- **Espacio en disco:** Imagen ~20 MB
- **Puerto:** 80 o 8080 (configurable)
- **Internet:** Solo para acceder al dashboard (no requiere conectividad hacia afuera)
- **Navegador moderno** (cualquiera)
- **Ultra-ligero:** Perfecto para Raspberry Pi, máquinas viejas, VPS $2/mes. Sin overhead

---

## 🐳 Instalación

### Opción 1: Docker Run simple

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

---

## ⚙️ Configuración

1. **Puerto host:** Modifica `"8080:80"` en `docker-compose.yml` si necesitas otro puerto (ej: `"3000:80"`)
2. **Registry alternativo:** Descomenta `ghcr.io/corentinth/it-tools:latest` para usar GitHub Container Registry
3. **Reverse proxy:** Configura Caddy/Nginx/Traefik apuntando a `localhost:8080` para HTTPS
4. **Dominio personalizado:** Añade entrada DNS tipo A/CNAME apuntando a tu servidor
5. **Sin variables de entorno requeridas:** IT-Tools es stateless y no necesita configuración adicional

---

## 🚀 Primeros pasos

1. **Clona o crea el directorio del proyecto:**
   ```bash
   mkdir it-tools && cd it-tools
   ```

2. **Crea el archivo `docker-compose.yml`** con el contenido de la sección Instalación

3. **Levanta el contenedor:**
   ```bash
   docker compose up -d
   ```

4. **Verifica que está corriendo:**
   ```bash
   docker ps | grep it-tools
   ```

5. **Accede al dashboard:** Abre `http://localhost:8080` (o tu puerto configurado)

6. **¡Listo!** Sin login, sin setup. Empieza a usar cualquiera de las 100+ herramientas inmediatamente

---

## 💡 Casos de uso

- **Developers diarios:** Deja de buscar herramientas online. Todo en IT-Tools
- **DevOps/SRE:** Debugging Docker commands, parsing logs, encoding secrets
- **Security professionals:** Hash generation, encryption, JWT validation, todo offline
- **Homelabbers:** Ejecuta localmente. No confíes en herramientas web random
- **Edu/Teams:** Despliega en intranet. Todos acceden sin permisos de internet

---

## 🔒 Acceso remoto seguro

### Con Caddy (recomendado - HTTPS automático)

```caddyfile
tools.tudominio.com {
    reverse_proxy localhost:8080
}
```

### Con Nginx Proxy Manager

1. Añade Proxy Host: `tools.tudominio.com` → `http://tu-ip:8080`
2. Activa SSL con Let's Encrypt
3. Accede via `https://tools.tudominio.com`

> **Nota:** Todo sigue siendo client-side. Los datos nunca llegan al servidor, solo se sirven los assets estáticos.

---

## 🛠️ Gestión y mantenimiento

### Ver logs en tiempo real
```bash
docker logs -f it-tools
```

### Reiniciar servicio
```bash
docker restart it-tools
```

### Actualizar a versión más reciente
```bash
docker pull corentinth/it-tools:latest
docker compose down
docker compose up -d
```

### Monitorear consumo de recursos
```bash
docker stats it-tools
# Verás: mínimo CPU, ~20-50MB RAM
```

### Notas de storage
- IT-Tools **NO requiere persistencia de datos**. Es stateless
- Borra el contenedor = todo igual al recrearlo
- Perfecto para **immutable infrastructure**

---

## 📝 Licencia

Este proyecto está licenciado bajo **GPL-3.0** - ver el archivo [LICENSE](https://github.com/CorentinTh/it-tools/blob/main/LICENSE) para detalles.

---

> 📖 **Artículo original:** [Cómo instalar IT-Tools - Colección de herramientas para developers autohospedada en Docker](https://genbyte.blogspot.com/2026/07/como-instalar-it-tools-coleccion-de.html)
>
> 🐙 **Repositorio oficial:** [CorentinTh/it-tools](https://github.com/CorentinTh/it-tools)  
> 🐳 **Docker Hub:** [corentinth/it-tools](https://hub.docker.com/r/corentinth/it-tools)  
> 📦 **GHCR:** [ghcr.io/corentinth/it-tools](https://github.com/CorentinTh/it-tools/pkgs/container/it-tools)  
> 🌐 **Demo online:** [it-tools.tech](https://it-tools.tech)