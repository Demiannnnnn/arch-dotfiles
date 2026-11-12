# arch-dotfiles

Archivos de configuración (*dotfiles*) para el compositor **Hyprland** y la barra de estado **Waybar** en **Arch Linux**.

---

## Contenido del repositorio

El repositorio contiene las configuraciones modulares organizadas en los siguientes directorios y archivos:

- `hypr/hyprland.conf`: Archivo principal de configuración del gestor de ventanas / compositor Wayland Hyprland.
  - **Monitor**: Configuración de pantalla por defecto (`montior=,preferred,auto,1`).
  - **Teclado**: Distribución de teclado en español latinoamericano (`latam` en `input { kb_layout = latam }`).
  - **Terminal**: Definido como `$terminal = kitty`.
  - **Atajos de teclado (`bind`)**: Combinaciones para control de ventanas, espacios de trabajo, portapapeles y lanzadores (ver tabla detallada abajo).
  - **Procesos al inicio (`exec-once`)**:
    - `waybar`: Inicia la barra de estado.
    - `blueman-applet`: Applet en bandeja para gestión de Bluetooth.
    - `wl-paste --type text --watch cliphist store`: Monitor de portapapeles para texto.
    - `wl-paste --type image --watch cliphist store`: Monitor de portapapeles para imágenes.
    - `dbus-update-activation-environment --systemd WAYLAND_DISPLAY XDG_CURRENT_DESKTOP`: Exportación de variables al entorno DBus y systemd.
    - `systemctl --user import-environment WAYLAND_DISPLAY XDG_CURRENT_DESKTOP`: Importación de variables de sesión en systemd de usuario.

- `waybar/config.jsonc`: Configuración en formato JSONC de la barra Waybar (altura: 30px, espaciado: 4px).
  - **Módulos a la izquierda (`modules-left`)**:
    - `sway/workspaces`: Espacios de trabajo.
    - `sway/mode`: Modo actual del compositor.
    - `sway/scratchpad`: Ventanas en el scratchpad.
    - `custom/media`: Visualizador multimedia mediante script externo (`$HOME/.config/waybar/mediaplayer.py`).
  - **Módulos al centro (`modules-center`)**:
    - `sway/window`: Título de la ventana activa.
  - **Módulos a la derecha (`modules-right`)**:
    - `mpd`: Estado y reproducción de Music Player Daemon.
    - `idle_inhibitor`: Inhibidor de suspensión/inactividad.
    - `pulseaudio`: Nivel y estado de volumen/micrófono (al pulsar abre `pavucontrol`).
    - `network`: Información de conexión WiFi o Ethernet e IP.
    - `power-profiles-daemon`: Perfil de energía actual (rendimiento, balanceado, ahorro).
    - `cpu`: Porcentaje de uso del procesador.
    - `memory`: Porcentaje de consumo de memoria RAM.
    - `temperature`: Temperatura del equipo con aviso crítico a 80 °C.
    - `backlight`: Nivel de brillo de la pantalla.
    - `keyboard-state`: Indicadores de estado para NumLock y CapsLock.
    - `sway/language`: Idioma/distribución de teclado activa.
    - `battery` y `battery#bat2`: Nivel de carga de batería principal y secundaria.
    - `clock`: Reloj con fecha y calendario desplegable.
    - `tray`: Bandeja del sistema.
    - `custom/power`: Menú de apagado, reinicio, suspensión e hibernación (`$HOME/.config/waybar/power_menu.xml`).
    - `custom/spotify`: Módulo para visualización y control de `spotifyd` mediante `playerctl`.

- `waybar/style.css`: Hoja de estilos en cascada (CSS) para la personalización estética de Waybar (colores, márgenes, bordes, efectos de hover y animaciones de parpadeo para batería baja). Requiere fuentes de iconos como `FontAwesome` y tipografía `Roboto`.

---

## Atajos de teclado (Hyprland)

A continuación se listan todos los atajos de teclado extraídos literalmente de las directivas `bind` de `hypr/hyprland.conf`:

### Atajos generales y de gestión de ventanas

| Modificadores | Tecla | Acción / Comando | Descripción |
|---|---|---|---|
| `CTRL ALT` | `T` | `exec, $terminal` | Abre el terminal predeterminado (`kitty`) |
| `SUPER` | `V` | `exec, cliphist list \| wofi --dmenu \| cliphist decode \| wl-copy` | Abre el historial de portapapeles y copia la selección |
| `SUPER` | `Q` | `killactive` | Cierra la ventana activa |
| `SUPER` | `F` | `fullscreen, 0` | Alterna pantalla completa |
| `SUPER SHIFT` | `left` | `movewindow, l` | Mueve la ventana activa a la izquierda |
| `SUPER SHIFT` | `right` | `movewindow, r` | Mueve la ventana activa a la derecha |
| `SUPER SHIFT` | `up` | `movewindow, u` | Mueve la ventana activa hacia arriba |
| `SUPER SHIFT` | `down` | `movewindow, d` | Mueve la ventana activa hacia abajo |
| `SUPER` | `R` | `submap, resize` | Activa el submapa para redimensionar ventanas |
| `SUPER` | `left` | `movefocus, l` | Mueve el foco hacia la ventana de la izquierda |
| `SUPER` | `right` | `movefocus, r` | Mueve el foco hacia la ventana de la derecha |
| `SUPER` | `up` | `movefocus, u` | Mueve el foco hacia la ventana de arriba |
| `SUPER` | `down` | `movefocus, d` | Mueve el foco hacia la ventana de abajo |
| `SUPER` | `D` | `exec, wofi --show drun` | Abre el lanzador de aplicaciones (`wofi`) |
| `SUPER SHIFT` | `D` | `exec, wofi --show run` | Abre el ejecutor de comandos (`wofi`) |
| `SUPER SHIFT` | `E` | `exit` | Sale de la sesión de Hyprland |

### Espacios de trabajo (*Workspaces*)

| Modificadores | Tecla | Acción / Comando | Descripción |
|---|---|---|---|
| `SUPER` | `1` | `workspace, 1` | Cambia al espacio de trabajo 1 |
| `SUPER` | `2` | `workspace, 2` | Cambia al espacio de trabajo 2 |
| `SUPER` | `3` | `workspace, 3` | Cambia al espacio de trabajo 3 |
| `SUPER` | `4` | `workspace, 4` | Cambia al espacio de trabajo 4 |
| `SUPER` | `5` | `workspace, 5` | Cambia al espacio de trabajo 5 |
| `SUPER` | `6` | `workspace, 6` | Cambia al espacio de trabajo 6 |
| `SUPER` | `7` | `workspace, 7` | Cambia al espacio de trabajo 7 |
| `SUPER` | `8` | `workspace, 8` | Cambia al espacio de trabajo 8 |
| `SUPER` | `9` | `workspace, 0` | Cambia al espacio de trabajo 0 |
| `SUPER` | `0` | `workspace, 10` | Cambia al espacio de trabajo 10 |
| `SUPER SHIFT` | `1` | `movetoworkspace, 1` | Mueve la ventana al espacio de trabajo 1 |
| `SUPER SHIFT` | `2` | `movetoworkspace, 2` | Mueve la ventana al espacio de trabajo 2 |
| `SUPER SHIFT` | `3` | `movetoworkspace, 3` | Mueve la ventana al espacio de trabajo 3 |
| `SUPER SHIFT` | `4` | `movetoworkspace, 4` | Mueve la ventana al espacio de trabajo 4 |
| `SUPER SHIFT` | `5` | `movetoworkspace, 5` | Mueve la ventana al espacio de trabajo 5 |
| `SUPER SHIFT` | `6` | `movetoworkspace, 6` | Mueve la ventana al espacio de trabajo 6 |
| `SUPER SHIFT` | `7` | `movetoworkspace, 7` | Mueve la ventana al espacio de trabajo 7 |
| `SUPER SHIFT` | `8` | `movetoworkspace, 8` | Mueve la ventana al espacio de trabajo 8 |
| `SUPER SHIFT` | `9` | `movetoworkspace, 0` | Mueve la ventana al espacio de trabajo 0 |
| `SUPER SHIFT` | `0` | `movetoworkspace, 10` | Mueve la ventana al espacio de trabajo 10 |
| `SUPER ALT` | `1` | `movetoworkspacesilent, 1` | Mueve la ventana silenciosamente al workspace 1 |
| `SUPER ALT` | `2` | `movetoworkspacesilent, 2` | Mueve la ventana silenciosamente al workspace 2 |
| `SUPER ALT` | `3` | `movetoworkspacesilent, 3` | Mueve la ventana silenciosamente al workspace 3 |
| `SUPER ALT` | `4` | `movetoworkspacesilent, 4` | Mueve la ventana silenciosamente al workspace 4 |
| `SUPER ALT` | `5` | `movetoworkspacesilent, 5` | Mueve la ventana silenciosamente al workspace 5 |
| `SUPER ALT` | `6` | `movetoworkspacesilent, 6` | Mueve la ventana silenciosamente al workspace 6 |
| `SUPER ALT` | `7` | `movetoworkspacesilent, 7` | Mueve la ventana silenciosamente al workspace 7 |
| `SUPER ALT` | `8` | `movetoworkspacesilent, 8` | Mueve la ventana silenciosamente al workspace 8 |
| `SUPER ALT` | `9` | `movetoworkspacesilent, 0` | Mueve la ventana silenciosamente al workspace 0 |
| `SUPER ALT` | `0` | `movetoworkspacesilent, 10` | Mueve la ventana silenciosamente al workspace 10 |
| `SUPER` | `mouse_down` | `workspace, e+1` | Cambia al siguiente espacio de trabajo |
| `SUPER` | `mouse_up` | `workspace, e-1` | Cambia al espacio de trabajo anterior |

### Modo redimensionamiento (`submap = resize`)

| Modificadores | Tecla | Tipo de enlace | Acción / Comando | Descripción |
|---|---|---|---|---|
| *(ninguno)* | `right` | `binde` | `resizeactive, 10 0` | Aumenta el ancho en 10px |
| *(ninguno)* | `left` | `binde` | `resizeactive, -10 0` | Disminuye el ancho en 10px |
| *(ninguno)* | `up` | `binde` | `resizeactive, 0 -10` | Disminuye el alto en 10px |
| *(ninguno)* | `down` | `binde` | `resizeactive, 0 10` | Aumenta el alto en 10px |
| *(ninguno)* | `l` | `binde` | `resizeactive, 10 0` | Aumenta el ancho en 10px |
| *(ninguno)* | `h` | `binde` | `resizeactive, -10 0` | Disminuye el ancho en 10px |
| *(ninguno)* | `k` | `binde` | `resizeactive, 0 -10` | Disminuye el alto en 10px |
| *(ninguno)* | `j` | `binde` | `resizeactive, 0 10` | Aumenta el alto en 10px |
| *(ninguno)* | `escape` | `bind` | `submap, reset` | Sale del modo redimensionamiento |

---

## Dependencias

A continuación se listan únicamente los paquetes y herramientas que aparecen explícitamente en los archivos de configuración:

### Gestor de ventanas y barra
- **`hyprland`**: Compositor Wayland dinámico sobre el que opera la configuración.
- **`waybar`**: Barra de estado personalizable para entornos Wayland (`hyprland.conf:105`).

### Aplicaciones y utilidades de usuario
- **`kitty`**: Emulador de terminal configurado como predeterminado (`hyprland.conf:8, 11`).
- **`wofi`**: Lanzador de menús y aplicaciones en Wayland, usado para selección de aplicaciones y menú del portapapeles (`hyprland.conf:14, 100, 101`).
- **`cliphist`**: Utilidad de gestión de historial del portapapeles (`hyprland.conf:14, 111, 112`).
- **`wl-clipboard`** (proporciona `wl-copy` y `wl-paste`): Herramientas de portapapeles para Wayland (`hyprland.conf:14, 111, 112`).
- **`blueman`** (proporciona `blueman-applet`): Applet de bandeja para control de Bluetooth (`hyprland.conf:108`).

### Módulos de Waybar y servicios
- **`pulseaudio`** y **`pavucontrol`**: Servidor de audio y panel de control gráfico de volumen (`config.jsonc:174, 191`).
- **`mpd`**: Music Player Daemon para el reproductor de audio (`config.jsonc:73-98`).
- **`playerctl`**: Control de reproductores multimedia por CLI en el módulo de Spotify (`config.jsonc:220, 223-225`).
- **`spotifyd`**: Demonio ligero de Spotify referenciado en el módulo `custom/spotify` (`config.jsonc:220, 223-225`).
- **`power-profiles-daemon`**: Demonio para perfiles de consumo energético (`config.jsonc:154`).
- **`dbus`** y **`systemd`**: Utilidades del sistema para sincronización del entorno Wayland (`dbus-update-activation-environment`, `systemctl`) y acciones de energía (`shutdown`, `reboot`, `systemctl suspend`, `systemctl hibernate`) (`hyprland.conf:117, 118`; `config.jsonc:211-214`).

### Fuentes y tipografías
- **`otf-font-awesome`** (o `ttf-font-awesome`): Paquete de iconos requerido para Waybar (`style.css:2-3`).
- **`ttf-roboto`**: Familia tipográfica Roboto especificada en los estilos (`style.css:3`).

---

## Instalación

> [!WARNING]
> **Copia de seguridad requerida**: Antes de realizar cualquier enlace o copia, asegúrese de respaldar cualquier configuración previa existente en su directorio de usuario para evitar la pérdida accidental de configuraciones anteriores.

### 1. Realizar copia de seguridad previa

Ejecute los siguientes comandos para respaldar sus directorios actuales si existen:

```bash
[ -d ~/.config/hypr ] && cp -r ~/.config/hypr ~/.config/hypr.bak.$(date +%Y%m%d_%H%M%S)
[ -d ~/.config/waybar ] && cp -r ~/.config/waybar ~/.config/waybar.bak.$(date +%Y%m%d_%H%M%S)
```

### 2. Instalar las configuraciones

Puede optar por enlazar simbólicamente los directorios (recomendado para mantener cambios reflejados en el repositorio) o realizar una copia directa.

#### Opción A: Enlaces simbólicos (`ln -s`)

Desde el directorio raíz de este repositorio:

```bash
# Crear el directorio base de configuración si no existe
mkdir -p ~/.config

# Enlazar las carpetas hypr y waybar
ln -s "$(pwd)/hypr" ~/.config/hypr
ln -s "$(pwd)/waybar" ~/.config/waybar
```

#### Opción B: Copia directa de archivos

Si prefiere copiar los archivos sin mantener un enlace con el repositorio git:

```bash
# Crear directorios de destino
mkdir -p ~/.config/hypr ~/.config/waybar

# Copiar archivos
cp -r hypr/* ~/.config/hypr/
cp -r waybar/* ~/.config/waybar/
```
