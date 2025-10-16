# 💡 Presentación: Flujo de Trabajo con Git y GitHub

## Introducción y Objetivos

El objetivo de esta presentación es comprender y aplicar el flujo de trabajo completo con Git, desde la configuración inicial hasta la colaboración en equipo, utilizando GitHub como plataforma remota.

---

## 1. Configuración Inicial

### ¿Qué es Git y GitHub? 💾🌐

| Característica | **Git** | **GitHub** |
| :--- | :--- | :--- |
| **Definición** | **Sistema de Control de Versiones Distribuido** (VCS) de código abierto. | Plataforma web de **alojamiento de repositorios** que utiliza Git. |
| **Función Principal** | Rastrea y gestiona los cambios en el código **localmente**. | Proporciona una interfaz gráfica, gestión de proyectos y herramientas de **colaboración** (Pull Requests, Issues). |
| **Naturaleza** | Software de línea de comandos, herramienta **local**. | Servicio en la nube, plataforma **remota**. |
| **Relación** | Git es la **tecnología subyacente** (el motor). | GitHub es un **servicio** que aloja y facilita el uso de Git. |

### Instalación de Git y Configuración del Usuario

1.  **Instalación de Git:**
    * Descarga el instalador desde el sitio oficial (git-scm.com).
    * Verifica la instalación: `git --version`

2.  **Configuración de Usuario (Identidad Global):**
    * Es fundamental para que tus *commits* se registren correctamente.
    ```bash
    git config --global user.name "Tu Nombre"
    git config --global user.email "tu.email@ejemplo.com"
    ```

### Autenticación y Verificación de Conexión 🔐

* **Autenticación (Para operaciones remotas: `push`, `pull`, `clone` HTTPS):**
    * **Opción 1: Token de Acceso Personal (PAT):** Reemplaza la contraseña para el protocolo HTTPS. Genera uno en la configuración de GitHub y úsalo como contraseña.
    * **Opción 2: Claves SSH:** Método más seguro y común entre desarrolladores. Requiere generar una clave SSH local y registrarla en tu cuenta de GitHub. (Si usas SSH, no necesitas el token).
* **Verificación de Configuración:**
    ```bash
    git config --list
    ```

---

## 2. Gestión de Repositorios

Un **repositorio (repo)** es la carpeta raíz de tu proyecto rastreada por Git.

### Flujo 1: Cargar un Proyecto Local a GitHub

Para inicializar Git y enlazarlo con un repositorio remoto vacío:

| Comando | Propósito | Ejemplo Práctico |
| :--- | :--- | :--- |
| `git init` | Inicializa el repositorio Git local en el directorio actual. | `cd mi-proyecto` $\rightarrow$ `git init` |
| `git add .` $\rightarrow$ `git commit -m "Initial commit"` | Prepara y guarda la primera versión del proyecto local. | |
| `git remote add origin <url_remota>` | Enlaza el repositorio local con el repositorio remoto de GitHub. `origin` es el alias por defecto. | `git remote add origin https://github.com/user/project.git` |
| `git branch -M main` | (Opcional) Renombra la rama principal a `main`. | |
| `git push -u origin main` | Sube los commits locales a la rama `main` del remoto (`origin`). | `git push -u origin main` |

### Flujo 2: Clonar un Repositorio Existente

Para descargar una copia completa de un proyecto ya alojado en GitHub:

| Comando | Propósito | Ejemplo Práctico |
| :--- | :--- | :--- |
| `git clone <url>` | Descarga el repositorio remoto, incluyendo todo el historial de versiones, y configura el remoto automáticamente. | `git clone https://github.com/user/project.git` |

### 🧠 Recomendaciones Prácticas

* **`.gitignore`:** Crea este archivo en la raíz del proyecto para excluir archivos que no deben ser rastreados (ej: credenciales, archivos compilados, `node_modules`).

---

## 3. Control de Versiones

El **Control de Versiones** permite rastrear, comparar y recuperar versiones específicas de tu código.

### Ciclo de Commit (Guardar Cambios Localmente) 📝

Un **commit** es una instantánea lógica de tu proyecto.

1.  **Verificar el Estado:**
    ```bash
    git status
    ```
    (Muestra archivos modificados, staged o sin rastrear.)

2.  **Añadir Archivos al Staging Area (Índice):**
    * El *staging area* es el área de preparación para el próximo *commit*.
    ```bash
    git add archivo_modificado.js # Añade un archivo
    git add .                    # Añade todos los archivos modificados
    ```

3.  **Realizar el Commit:**
    ```bash
    git commit -m "Mensaje descriptivo del cambio"
    ```
    * **Buena Práctica:** El mensaje debe ser un resumen conciso y descriptivo del **qué** y **por qué** del cambio.

### Visualizar y Gestionar el Historial 🕰️

| Comando | Propósito |
| :--- | :--- |
| `git log` | Muestra el historial completo de *commits* (hash, autor, fecha, mensaje). |
| `git log --oneline` | Muestra el historial de forma concisa. |
| `git checkout <hash>` | Te mueve a un punto específico del historial para inspeccionar el código. |
| `git revert <hash>` | Crea un **nuevo commit** que deshace los cambios del *commit* especificado (seguro). |
| `git reset <hash> --hard` | Elimina commits de tu historial **local** y borra los cambios en tu directorio de trabajo (peligroso para cambios compartidos). |

---

## 4. Ramas (Branches)

Las **Ramas** permiten desarrollar funcionalidades en aislamiento de forma segura.

### Fundamentos y Propósito 🌳

* **¿Qué es?** Un puntero ligero a un *commit*.
* **¿Por qué usar ramas?**
    * Aislar desarrollos (nuevas funcionalidades, corrección de errores).
    * Mantener la rama `main` (o `master`) **estable** y libre de código a medias o defectuoso.

### Comandos Esenciales de Ramas 🛠️

| Comando | Propósito | Ejemplo Práctico |
| :--- | :--- | :--- |
| `git branch` | Lista todas las ramas locales. | |
| `git switch -c <nombre>` | Crea una nueva rama y se cambia a ella (combina `branch` y `checkout`). | `git switch -c feature/login-page` |
| `git switch <nombre>` | Cambia a una rama existente. | `git switch main` |
| `git merge <nombre>` | Fusiona el historial de la rama especificada en la rama actual. | `git merge feature/login-page` |
| `git branch -d <nombre>` | Elimina la rama local (si ya se fusionó). | `git branch -d feature/login-page` |

### Flujo de Trabajo con Ramas (Ejemplo)

1.  **Asegurarse de estar en la rama base (`main`):** `git switch main` $\rightarrow$ `git pull`
2.  **Crear y cambiar a la rama de desarrollo:** `git switch -c fix/101-broken-link`
3.  **Desarrollar, hacer commits y subir:** `git add .` $\rightarrow$ `git commit -m "fix: Corregido el enlace roto del footer"` $\rightarrow$ `git push -u origin fix/101-broken-link`
4.  **(Colaboración):** Crear un **Pull Request** en GitHub para revisión (ver Sección 5).
5.  **Fusionar (después de la revisión/aprobación):** `git switch main` $\rightarrow$ `git merge fix/101-broken-link`

### Resolución de Conflictos al Fusionar 💥

* Un **conflicto** ocurre cuando Git no puede decidir qué cambio mantener en la misma línea o sección de un archivo (cambios contradictorios en ramas distintas).
* **Pasos:**
    1.  Git detiene la fusión.
    2.  Edita manualmente el archivo con el conflicto, eliminando las marcas (`<<<<<<<`, `=======`, `>>>>>>>`) y dejando la versión correcta.
    3.  Finaliza la fusión: `git add .` $\rightarrow$ `git commit`

### 🏆 Buenas Prácticas en Ramas

* **Nombres Descriptivos:** Usa prefijos (`feature/`, `fix/`, `hotfix/`) seguidos de una descripción.
* **Ramas Lógicas:** Una rama = una tarea, una funcionalidad o una corrección de error.
* **Mantener `main` protegida:** Configurar en GitHub para evitar *pushes* directos.

---

## 5. Trabajo Colaborativo con GitHub

La colaboración se facilita a través de la plataforma remota de GitHub, usando **Pull Requests**.

### Roles y Permisos 🧑‍💻

| Rol | Descripción | Permisos Clave |
| :--- | :--- | :--- |
| **Administrador** | Control total. Define la configuración de seguridad y roles. | Todos. |
| **Colaborador** | Puede crear ramas, subir código (*push*), crear Issues y Pull Requests. | Leer, escribir. |

### Flujo de Trabajo en Equipo (GitHub Flow) 🌐

1.  **Desarrollo en Rama Aislada:** El colaborador crea una rama local, hace `commits` y la sube al repositorio remoto.
    ```bash
    git push -u origin feature/mi-tarea
    ```
2.  **Creación de Pull Request (PR):**
    * El colaborador va a GitHub y abre una PR.
    * La PR es una **propuesta de fusión** de su rama (`feature/mi-tarea`) en la rama principal (`main`).
3.  **Revisión y Comentarios:**
    * El equipo revisa el código en la PR, dejando comentarios y solicitando cambios si es necesario.
    * El autor del PR realiza los cambios solicitados localmente y hace `git push`. La PR se actualiza automáticamente.
4.  **Aprobación y Fusión:**
    * Una vez que el código es revisado y aprobado, un *maintainer* o administrador fusiona (hace *merge*) el código en la rama `main` de GitHub.
    * **Squash and Merge:** Opción popular que combina todos los *commits* de la rama en un único *commit* limpio en `main`.

### Herramientas Clave de Colaboración

* **Issues:** Mecanismo para **rastrear tareas, bugs, o discusiones** dentro del proyecto. Cada Issue puede vincularse a una PR.
* **Forks:** Una **copia personal** de un repositorio que un usuario hace en su propia cuenta. Se usa en proyectos de código abierto donde el colaborador no tiene acceso directo de escritura.

### 🤝 Buenas Prácticas de Colaboración

* **Sincronización:** Haz `git pull` en `main` antes de crear una rama y con frecuencia.
* **Revisiones de Código (*Code Review*):** Es un paso crítico para garantizar la calidad y compartir conocimiento.
* **Mensajes Claros:** Los mensajes de *commit* y los títulos de PRs deben ser explícitos.

---

## 6. Conclusiones y Buenas Prácticas

### Resumen de Flujos 🧭

| Flujo | Individual (Local) | Colaborativo (Remoto) |
| :--- | :--- | :--- |
| **Desarrollo** | `git add` $\rightarrow$ `git commit` | `git switch -c` $\rightarrow$ `git push` |
| **Integración** | `git merge` (entre ramas locales) | **Pull Request** $\rightarrow$ **Review** $\rightarrow$ **Merge** en GitHub |

### 🧼 Recomendaciones Finales

* **Historial Limpio:** Utiliza la opción **Squash and Merge** en GitHub para mantener la rama `main` legible.
* **Automatización:** Utiliza *hooks* o herramientas de Integración Continua (CI) para automatizar pruebas al subir código o abrir una PR.

### ❌ Errores Comunes que Deben Evitarse

* **Commit de Archivos Sensibles:** No incluyas claves API, contraseñas o datos personales. Usa `.gitignore`.
* **Commitear Directo a `main`:** Siempre trabaja en una rama de característica o corrección.
* **Olvidar Sincronizar:** Siempre haz `git pull` antes de empezar a trabajar o fusionar para evitar conflictos masivos.
