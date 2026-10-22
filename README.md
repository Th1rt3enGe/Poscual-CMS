# Poscual-CMS

## Descripción
Poscual Joyería requiere una solución que permita:
- Organizar un catálogo que actualmente cuenta con aproximadamente 80 productos.
- Mantener actualizada la disponibilidad de las piezas.
- Facilitar la consulta de productos por parte de los clientes.
- Separar la información pública de las funciones internas.
- Consultar información de inventario mediante acceso restringido.

## Propuesta
Sitio web dinámico basado en un CMS (Drupal)

1. Catálogo público de productos.
2. Clasificación mediante categorías.
3. Fichas individuales de las piezas.
4. Gestión de productos y existencias.
5. Acceso privado según el tipo de usuario.
6. Reporte de inventario.

---

## Requisitos previos

- Git
- Cuenta de GitHub
- Docker (Docker Desktop o Docker Engine)
- DDEV

---

## Opción 1: Desarrollo local (recomendado)

### Windows (WSL2 + Docker Desktop)

1. **Instalar WSL2 y Ubuntu**
   ```powershell
   wsl --install
   ```
   Reinicia el equipo si es necesario y abre Ubuntu.

2. **Instalar Docker Desktop**
  - Descarga e instala desde: https://docs.docker.com/desktop/setup/install/windows-install/
  - Durante la instalación asegúrate de activar la integración con WSL2.
  - Ve a **Settings -> Resources -> WSL Integration** y activa tu distribución de Ubuntu.

3. **Instalar DDEV dentro de Ubuntu**
   ```bash
   # Dentro de la terminal de Ubuntu (WSL)
   sudo apt-get update && sudo apt-get install -y curl
   sudo install -m 0755 -d /etc/apt/keyrings
   curl -fsSL https://packages.ddev.com/public/gpg.key | sudo tee /etc/apt/keyrings/ddev.asc > /dev/null
   sudo chmod a+r /etc/apt/keyrings/ddev.asc
   printf "Types: deb\nURIs: https://packages.ddev.com/public/deb/ubuntu\nSuites: stable\nComponents: main\nSigned-By: /etc/apt/keyrings/ddev.asc\n" | sudo tee /etc/apt/sources.list.d/ddev.sources > /dev/null
   sudo apt-get update && sudo apt-get install -y ddev
   mkcert -install
   ```

4. **Clonar el repositorio**
   ```bash
   cd ~
   git clone https://github.com/Th1rt3enGe/Poscual-CMS.git
   cd Poscual-CMS
   ```

5. **Iniciar el proyecto**
   ```bash
   ddev start
   ddev composer install
   ddev drush site:install -y   # sólo la primera vez (o cuando se necesite reinstalar)
   ddev launch
   ```

El sitio estará disponible en:
`https://poscual.ddev.site`

---

## Opción 2: GitHub Codespaces (sin instalar nada local)

1. Entra al repositorio en GitHub.
2. Haz clic en el botón verde **Code** -> pestaña **Codespaces** -> **Create codespace on main**.
3. Espera a que el Codespace termine de construir (puede tardar unos minutos la primera vez).
4. Una vez abierto el terminal dentro del Codespace, ejecuta:

   ```bash
   ddev start
   ddev composer install
   ddev drush site:install -y
   ddev launch
   ```

> **Nota**: Codespaces tiene un límite de horas gratuitas al mes. Úsalo principalmente para probar o cuando no tengas tu máquina configurada.

---

## Comandos útiles de DDEV

| Comando              | Descripción                              |
|----------------------|------------------------------------------|
| `ddev start`         | Inicia el entorno                        |
| `ddev stop`          | Detiene el entorno                       |
| `ddev restart`       | Reinicia el entorno                      |
| `ddev launch`        | Abre el sitio en el navegador            |
| `ddev drush cr`      | Limpia la caché de Drupal                |
| `ddev drush uli`     | Genera un enlace de acceso de administrador |
| `ddev ssh`           | Entra al contenedor web                  |
| `ddev describe`      | Muestra información del proyecto         |
| `ddev logs`          | Muestra los logs                         |

---

## Estructura del proyecto

- `web/` -> Código de Drupal (docroot)
- `.ddev/` -> Configuración de DDEV
- `.ddev/` -> Configuración de Codespaces
- `composer.json` / `composer.lock` -> Dependencias de PHP
- `config/sync/` -> Configuración exportada de Drupal (cuando se use)

---

## Flujo de trabajo recomendado

1. Crea una rama nueva para cada tarea:
   `git checkout -b feature/nombre-de-la-tarea`
2. Realiza los cambios.
3. Exporta la configuración si modificaste algo en Drupal:
   `ddev drush cex -y`
4. Haz commit y push.
5. Abre un Pull Request.

---

## Credenciales por defecto (después de `site:install`)

- **Usuario**: `admin`
- **Contraseña**: `se genera automáticamente`

> Cambia la contraseña en cuanto entres la primera vez.

---

## Ayuda y recursos

- Documentación oficial de DDEV: https://docs.ddev.com
- Documentación de Drupal: https://www.drupal.org/docs
