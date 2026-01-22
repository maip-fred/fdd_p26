# Navegación y Rutas

![Navegación - Frieren y grupo viajando por un mapa de árbol de directorios](./images/02_navigation_frieren_journey.png)

:::exercise{title="Quiz de rutas (práctica para Bandit)" difficulty="2"}

Responde mentalmente estas preguntas (te servirán en Bandit):

1. Si estás en `/home/usuario/proyectos/python`, ¿cuál es la ruta relativa a `/home/usuario/documentos`?
2. ¿Qué significa `~` y a qué ruta absoluta equivale en tu sistema?
3. Si ejecutas `cd ../..` desde `/home/usuario/a/b/c`, ¿en qué directorio terminas?
4. ¿Cuál es la diferencia entre `cd /home` y `cd home`?
5. ¿Qué comando usas para volver al directorio donde estabas antes?

**Tip:** Estos conceptos aparecen en los niveles de Bandit.

:::

Entender el sistema de archivos y cómo moverte es fundamental. Esta sección cubre uno de los conceptos más importantes: **rutas**.

---

![Sistema de archivos - Árbol de Yggdrasil estilo Serial Experiments Lain](./images/02_filesystem_lain_tree.png)

## El Sistema de Archivos

En Unix (Linux/macOS), todo es un árbol que empieza en `/` (raíz):

```
/                         ← Raíz (root)
├── home/                 ← Carpetas de usuarios
│   ├── maria/            ← Home de maria
│   │   ├── Documents/
│   │   ├── Downloads/
│   │   └── projects/
│   └── juan/             ← Home de juan
├── usr/                  ← Programas del sistema
│   ├── bin/              ← Comandos/ejecutables
│   └── lib/              ← Librerías
├── etc/                  ← Configuración del sistema
├── tmp/                  ← Archivos temporales
└── var/                  ← Datos variables (logs, etc.)
```

### Diferencias con Windows

| Unix/Linux/macOS | Windows |
|------------------|---------|
| `/` | `C:\` |
| `/home/usuario` | `C:\Users\usuario` |
| `/` separador | `\` separador |
| Case sensitive: `Archivo` ≠ `archivo` | Case insensitive |

---

![Rutas - Dos caminos: uno desde el origen (absoluto) y otro desde donde estás (relativo)](./images/02_paths_evangelion_nerv.png)

## Rutas Absolutas vs Relativas

Este es el concepto **más importante** de esta sección.

### Ruta Absoluta

Empieza desde la raíz (`/`). Es la dirección completa.

```bash
/home/maria/Documents/proyecto/archivo.txt
```

- Siempre empieza con `/`
- Funciona desde cualquier ubicación
- Es como dar la dirección completa de una casa

### Ruta Relativa

Empieza desde donde estás. Es relativa a tu ubicación actual.

```bash
# Si estás en /home/maria/
Documents/proyecto/archivo.txt

# Si estás en /home/maria/Documents/
proyecto/archivo.txt
```

- **No** empieza con `/`
- Depende de dónde estés
- Es como decir "a dos cuadras a la derecha"

### Símbolos Especiales para Rutas

| Símbolo | Significado | Ejemplo |
|---------|-------------|---------|
| `/` | Raíz del sistema | `cd /` |
| `~` | Tu directorio home | `cd ~` = `cd /home/tu_usuario` |
| `.` | Directorio actual | `./script.sh` |
| `..` | Directorio padre (uno arriba) | `cd ..` |
| `-` | Directorio anterior | `cd -` |

### Ejemplos Prácticos

```bash
# Estás en: /home/maria/Documents/proyecto

pwd
# /home/maria/Documents/proyecto

# Ir al home (3 formas equivalentes)
cd ~
cd /home/maria
cd

# Ir un nivel arriba (a Documents)
cd ..

# Ir dos niveles arriba (a home/maria)
cd ../..

# Ir a una carpeta hermana
cd ../otra_carpeta

# Volver al directorio anterior
cd -
```

---

## Comandos de Navegación

### `pwd` - Dónde estoy

**P**rint **W**orking **D**irectory

```bash
pwd
# /home/maria/Documents
```

### `ls` - Qué hay aquí

**L**i**s**t - lista el contenido de un directorio.

```bash
# Listar directorio actual
ls

# Listar otro directorio
ls /home

# Listar con detalles
ls -l

# Listar incluyendo archivos ocultos
ls -a

# Listar con detalles + ocultos + tamaños legibles
ls -lah
```

#### Entendiendo `ls -l`

```
drwxr-xr-x  2 maria maria 4096 Jan 20 10:30 Documents
-rw-r--r--  1 maria maria  256 Jan 19 09:15 notas.txt
```

| Parte | Significado |
|-------|-------------|
| `d` o `-` | Directorio o archivo |
| `rwxr-xr-x` | Permisos |
| `2` | Número de enlaces |
| `maria` | Dueño |
| `maria` | Grupo |
| `4096` | Tamaño en bytes |
| `Jan 20 10:30` | Fecha de modificación |
| `Documents` | Nombre |

### `cd` - Cambiar directorio

**C**hange **D**irectory

```bash
# Ir a una ruta absoluta
cd /home/maria/Documents

# Ir a una ruta relativa
cd Documents

# Ir al home
cd ~
cd     # Equivalente

# Ir un nivel arriba
cd ..

# Ir a la raíz
cd /

# Volver al directorio anterior
cd -
```

---

![Home directory - La acogedora habitación de Lain llena de computadoras](./images/02_home_lain_room.png)

## El Directorio Home (`~`)

Tu **home** es tu espacio personal. Es donde:
- Guardas tus archivos
- Están tus configuraciones (archivos que empiezan con `.`)
- Empiezas cuando abres la terminal

```bash
# Ver tu home
echo $HOME
# /home/tu_usuario

# Ir al home (todas equivalentes)
cd
cd ~
cd $HOME
cd /home/tu_usuario
```

### Archivos ocultos (dotfiles)

Los archivos que empiezan con `.` son ocultos:

```bash
ls -a ~
# .bashrc     ← Configuración de Bash
# .profile    ← Configuración de login
# .ssh/       ← Llaves SSH
# .gitconfig  ← Configuración de Git
```

---

## Rutas en WSL2

Si usas WSL2, puedes acceder a los archivos de Windows:

```bash
# Tus archivos de Windows están en:
/mnt/c/Users/TuUsuarioWindows/

# Ejemplo: ir a Documentos de Windows
cd /mnt/c/Users/Juan/Documents

# Tu home de Linux está en:
/home/tu_usuario_linux/
```

> **Recomendación:** Trabaja en tu home de Linux (`~`) para mejor rendimiento. Solo accede a `/mnt/c/` cuando necesites archivos específicos de Windows.

---

## Ejercicios Prácticos

:::exercise{title="Navegación básica" difficulty="1"}

1. Abre tu terminal
2. Ejecuta `pwd` - ¿dónde estás?
3. Ejecuta `ls` - ¿qué hay?
4. Ejecuta `cd /` y luego `ls` - ¿qué ves en la raíz?
5. Ejecuta `cd ~` para volver a tu home

:::

:::exercise{title="Rutas relativas" difficulty="2"}

Desde tu home (`~`):

1. Crea una estructura: `mkdir -p proyectos/python/ejercicio1`
2. Navega a `ejercicio1` usando ruta relativa
3. Ejecuta `pwd` para verificar
4. Vuelve a home usando `cd ../../../`
5. Verifica con `pwd`

:::

:::exercise{title="Diferencia absoluta vs relativa" difficulty="2"}

1. Navega a `/tmp` usando ruta absoluta
2. Desde `/tmp`, intenta ir a tu home de dos formas:
   - Ruta absoluta: `cd /home/tu_usuario`
   - Usando `~`: `cd ~`
3. ¿Cuál es más corta?

:::

---

## Resumen de Rutas

| Tipo | Ejemplo | Cuándo usar |
|------|---------|-------------|
| Absoluta | `/home/maria/docs` | Scripts, configuraciones |
| Relativa | `docs/archivo.txt` | Navegación rápida |
| Home | `~/projects` | Acceder a tus archivos |
| Padre | `../` | Subir niveles |
| Actual | `./script.sh` | Ejecutar archivos locales |

---

## Más Ejercicios

:::exercise{title="Mapa mental del sistema" difficulty="2"}

Explora estas rutas y anota qué contienen:

```bash
ls /
ls /home
ls /usr/bin | head -20
ls /etc | head -20
ls /tmp
```

**Pregunta:** ¿Para qué crees que sirve cada directorio?

:::

:::exercise{title="Carrera de navegación" difficulty="2"}

Cronometra cuánto tardas en:

1. Ir a `/var/log`
2. Volver a tu home
3. Ir a `/etc`
4. Volver al directorio anterior (`cd -`)
5. Crear `~/prueba/nivel1/nivel2/nivel3` con un solo comando

**Objetivo:** Hazlo en menos de 30 segundos.

:::

:::exercise{title="Encuentra tu archivo de configuración de bash" difficulty="2"}

1. Ve a tu home: `cd ~`
2. Lista archivos ocultos: `ls -la`
3. Encuentra `.bashrc` o `.zshrc`
4. Muestra su contenido: `cat ~/.bashrc`

**Pregunta:** ¿Qué tipo de configuraciones tiene?

:::

---

## Prompts para LLM

:::prompt{title="Convertir ruta Windows a Linux" for="ChatGPT/Claude"}

Tengo esta ruta de Windows:

```
C:\Users\MiUsuario\Documents\proyecto\archivo.txt
```

¿Cómo accedo a este archivo desde WSL2? Explícame cómo funcionan las rutas en /mnt/c/

:::

:::prompt{title="Entender estructura de directorios" for="ChatGPT/Claude"}

Soy nuevo en Linux. Explícame para qué sirven estos directorios del sistema:
- /home
- /etc
- /var
- /usr
- /tmp
- /bin

Dame ejemplos prácticos de cuándo usaría cada uno.

:::

:::prompt{title="Practicar rutas" for="ChatGPT/Claude"}

Dame 5 ejercicios de práctica para convertir rutas absolutas a relativas y viceversa en Linux. Incluye las respuestas para que pueda verificar.

Estoy en el directorio: /home/usuario/proyectos/python

:::

---

## Resumen de Comandos

| Comando | Descripción |
|---------|-------------|
| `pwd` | Muestra directorio actual |
| `ls` | Lista contenido |
| `ls -la` | Lista con detalles y ocultos |
| `cd ruta` | Cambia a directorio |
| `cd` o `cd ~` | Va al home |
| `cd ..` | Sube un nivel |
| `cd -` | Vuelve al anterior |
