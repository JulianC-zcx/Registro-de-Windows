## Definición:

El Registro de Windows es una base de datos jerárquica centralizada que almacena todas las configuraciones y opciones del sistema operativo Windows. Funciona como el cerebro de configuraciones del sistema, donde se guarda información crítica sobre:

- Configuraciones del sistema operativo.
- Programas instalados y sus preferencias.
- Perfiles de usuario.
- Configuraciones de hardware y dispositivos.
- Opciones de arranque del sistema.

**Historia**: Introducido en Windows 3.1 (1992) y consolidado en Windows 95, reemplazando al antiguo sistema de archivos .INI que era desorganizado y limitado.

## Estructura:

El Registro de Windows utiliza una estructura jerárquica similar a un sistema de archivos:

### Elementos principales:

- **Claves (Keys)**: Contenedores principales, como carpetas.
- **Subclaves (Subkeys)**: Claves dentro de otras claves, como subcarpetas.
- **Valores (Values)**: Los datos reales que se almacenan, como archivos.

### Características importantes:

- Las rutas son absolutas y siempre comienzan desde una clave raíz.
- Se utiliza la barra invertida `\` como separador.
- No distingue entre mayúsculas y minúsculas.
- Funciona como una base de datos transaccional con propiedades ACID.

## Claves Raíz:

Las cinco claves raíz principales (HKEYs) del Registro:

### HKEY_CLASSES_ROOT (HKCR):

Almacena asociaciones de tipos de archivo. Define qué programa abre cada tipo de archivo.

### HKEY_CURRENT_USER (HKCU):

Contiene las configuraciones específicas del usuario que está actualmente conectado (fondo de pantalla, preferencias personales, etc.).

### HKEY_LOCAL_MACHINE (HKLM):

Guarda configuraciones globales del equipo que aplican para todos los usuarios (hardware, software instalado, configuración del sistema).

### HKEY_USERS (HKU):

Contiene los perfiles de configuración de todos los usuarios del equipo. HKCU es un acceso directo al perfil del usuario actual dentro de HKU.

### HKEY_CURRENT_CONFIG (HKCC):

Muestra la configuración actual del hardware activo. Es un alias que apunta al perfil de hardware en uso.

## Tipos de Datos:

Los valores del Registro pueden contener diferentes tipos de datos:

| Tipo         | Descripción                | Ejemplo de uso                         |
| ------------ | -------------------------- | -------------------------------------- |
| REG_SZ       | Cadena de texto simple     | Nombres, rutas de archivos             |
| REG_DWORD    | Número entero de 32 bits   | Valores 0/1, configuraciones numéricas |
| REG_BINARY   | Datos binarios             | Configuraciones de hardware            |
| REG_MULTI_SZ | Múltiples cadenas de texto | Listas de valores                      |
| REG_QWORD    | Número entero de 64 bits   | Valores numéricos grandes              |

## Ejemplo de Aplicación:

### Ejemplo: Cambiar el fondo de pantalla:

Ruta en el Registro:

```
HKEY_CURRENT_USER\Control Panel\Desktop
```

Valor a modificar: `Wallpaper` (tipo REG_SZ).

### Precauciones importantes:

- **Siempre hacer backup antes de editar**
- Cambios incorrectos pueden impedir que Windows arranque.
- Requiere permisos de administrador.
- No eliminar claves sin saber su función.

### Herramientas de acceso:

- **Regedit.exe**: Editor gráfico del Registro (Win+R, regedit).
- **PowerShell**: `Get-WinEvent`, `Set-ItemProperty`.
- **Archivos .REG**: Para importar/exportar configuraciones.
- **CMD**: Comando `reg` para operaciones por lotes.

---
## Tabla Comparativa: Claves de Usuario vs Claves de Equipo Local:

| Aspecto                   | HKEY_CURRENT_USER (Usuario)                         | HKEY_LOCAL_MACHINE (Equipo)                            |
| ------------------------- | --------------------------------------------------- | ------------------------------------------------------ |
| **Alcance**               | Solo afecta al usuario actual                       | Afecta a todos los usuarios del equipo                 |
| **Tipo de configuración** | Preferencias personales (fondos, temas)             | Configuraciones globales (hardware, drivers, software) |
| **Permisos necesarios**   | Usuario estándar puede modificar sus propias claves | Requiere permisos de administrador                     |
| **Persistencia**          | Se carga o descarga con cada sesión de usuario      | Permanece cargada mientras Windows esté activo         |
| **Ejemplo de uso**        | Cambiar el idioma del teclado personal              | Instalar un driver de impresora para todos             |
| **Ubicación física**      | `C:\Users\[Usuario]\NTUSER.DAT`                     | `C:\Windows\System32\config\`                          |

---
## Archivos de Registro (Logs):

### Diferencia importante:

No confundir el Registro de Windows con el Historial de eventos.

### Tipos principales de logs:

- **Application**: Eventos de programas.
- **Security**: Seguridad.
- **System**: Eventos del sistema operativo.
- **Setup**: Instalaciones y actualizaciones.
- **Forwarded Events**: Eventos de red centralizados.

### Acceso a logs:

- Herramienta: **Visor de eventos** (eventvwr.msc).
- Ubicación física: `C:\Windows\System32\winevt\Logs\`.
- PowerShell:

```
wevtutil qe System /c:20 /f:text  
wevtutil qe Application /c:50 /f:text  
wevtutil gli System**
```

---
## Referencias y fuentes

-  [Documentación oficial de Microsoft - Registro de Windows](https://learn.microsoft.com/en-us/windows/win32/sysinfo/registry)
-  [Microsoft Learn - Estructura del Registro](https://learn.microsoft.com/en-us/windows/win32/sysinfo/structure-of-the-registry)
-  [Obsidian Markdown Guide](https://help.obsidian.md/Editing+and+formatting/Basic+formatting+syntax)
-  [Tutorial de Markdown - IONOS](https://www.ionos.com/es-us/digitalguide/paginas-web/desarrollo-web/tutorial-de-markdown/)

---
