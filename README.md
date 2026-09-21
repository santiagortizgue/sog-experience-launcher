# 🚀 SOG Experience Launcher

Repositorio de sincronización y distribución automática del modpack para el servidor **SOG Experience** mediante **Packwiz** integrado en **Prism Launcher**.

Permite que tú y tus amigos tengan siempre sincronizada la lista exacta de mods (incluyendo el mod propio `cobbleadditions.jar` y todos los mods de Modrinth/CurseForge) cada vez que inicien el juego, sin alterar sus configuraciones personales, shaders, waypoints ni controles locales.

---

## 🛠️ Especificaciones Técnicas

- **Versión de Minecraft**: `1.21.1`
- **Mod Loader**: `NeoForge` (Versión `21.1.250`)
- **Gestor de Sincronización**: `Packwiz` (`pack.toml` e `index.toml`)
- **Cliente Recomendado**: `Prism Launcher` (mediante `packwiz-installer-bootstrap.jar`)
- **Total de Mods**: 83 mods (82 públicos + 1 mod propio interno)

---

## 📦 Guía de Exportación e Instalación para Amigos

### Paso 1: Exportar la Instancia Base desde Prism Launcher (Para ti, el Admin)

1. En tu **Prism Launcher**, haz clic derecho sobre tu instancia configurada (`Pokecubos(1)`).
2. Selecciona **Exportar instancia** (Export Instance).
3. Asegúrate de incluir las carpetas base (`config/`, `resourcepacks/`, `kubejs/` si aplica, etc.).
4. Guarda el archivo `.zip` generado (por ejemplo `SOG-Experience-Base.zip`) y compártelo con tus amigos (vía Drive, Discord, etc.).

---

### Paso 2: Instalación y Configuración (Para tus Amigos)

Cada amigo solo debe hacer este paso una única vez:

1. **Abrir Prism Launcher**:
   - Arrastra y suelta el archivo `SOG-Experience-Base.zip` dentro de Prism Launcher (o pulsa *Añadir instancia > Importar desde zip*).
2. **Descargar el actualizador Packwiz**:
   - Descarga el archivo [`packwiz-installer-bootstrap.jar`](https://github.com/packwiz/packwiz-installer-bootstrap/releases/latest/download/packwiz-installer-bootstrap.jar).
   - Abre la carpeta de la instancia (*Clic derecho en la instancia > Carpeta de la instancia* o *Instance folder*).
   - Coloca `packwiz-installer-bootstrap.jar` en la raíz de la instancia (en la misma carpeta donde está `instance.cfg` y la subcarpeta `minecraft/`).
3. **Configurar el Comando Pre-Launch**:
   - En Prism Launcher, haz clic derecho sobre la instancia > **Editar** (Edit).
   - Ve a la sección **Comandos personalizados** (Custom Commands).
   - Marca la casilla **Comando previo al inicio** (Pre-launch command).
   - Pega exactamente el siguiente comando:
     ```bash
     "$INST_JAVA" -jar packwiz-installer-bootstrap.jar -bootstrap https://raw.githubusercontent.com/santiagortizgue/sog-experience-launcher/main/pack.toml
     ```
4. **¡Listo!**:
   - Cada vez que tus amigos pulsen **Jugar**, Packwiz verificará automáticamente el repositorio, descargará mods nuevos o actualizará mods existentes en milisegundos antes de arrancar Minecraft.

---

## 🔄 Cómo Actualizar Mods en el Servidor (Para ti, el Admin)

### 1. Actualizar tu Mod Propio (`cobbleadditions.jar`)
Cuando compiles una nueva versión en `sog-cobblemon-additions`:
```powershell
# Compilar el mod
cd ..\sog-cobblemon-additions
.\gradlew build

# Copiar el jar reemplazando el anterior
Copy-Item build\libs\cobbleadditions.jar ..\sog-launcher\mods\cobbleadditions.jar -Force

# Actualizar el índice de Packwiz
cd ..\sog-launcher
.\packwiz.exe refresh

# Subir a GitHub
git add .
git commit -m "Update cobbleadditions.jar"
git push
```

### 2. Añadir un Nuevo Mod desde Modrinth
```powershell
.\packwiz.exe modrinth add <slug-o-url> -y
git add .
git commit -m "Add new mod: <nombre>"
git push
```

### 3. Eliminar un Mod
```powershell
.\packwiz.exe remove <nombre-del-mod>
git add .
git commit -m "Remove mod: <nombre>"
git push
```

---

## 🔒 Privacidad y Visibilidad del Repositorio

Como tus amigos descargan los metadatos a través del enlace directo `raw.githubusercontent.com`, el repositorio requiere acceso de lectura HTTP sin credenciales complejas:

### Para reducir la visibilidad y evitar que sea indexado:
1. **No indexar en motores de búsqueda**: GitHub no indexa repositorios públicos en Google si no reciben estrellas/tráfico masivo, pero puedes ir a los ajustes del repositorio en GitHub:
   - Ve a **Settings** de tu repositorio `sog-experience-launcher`.
   - En la sección **General**, desmarca **Include in the home page** / Social preview si estuviera activo.
   - En la descripción del repo, deja el campo vacío y no añadas etiquetas ni topics.
2. **Nombre discreto**: Si lo prefieres, puedes cambiar el nombre del repo a algo neutro (ejemplo: `sog-dist` o `cb-assets`) actualizando luego la URL en el comando pre-launch de tus amigos.
