Perfecto. Te dejo **TODO completamente detallado**, **ordenado**, **listo para copiar y pegar**, y con **explicación clara de para qué sirve cada comando**.
La idea es que **no tengas que pensar qué hacer**, solo seguirlo como receta 👌

---

# 🐧 PRÁCTICA COMPLETA EN RED HAT LINUX

**Exploración del sistema de archivos + Diseño CMS + Simulación de planificación de disco**

---

# 🔵 PARTE 1 – EXPLORACIÓN DEL SISTEMA DE ARCHIVOS

## 📍 1. Abrir terminal

(No hay comando, solo abrir Terminal)

---

## 📍 2. Ver en qué directorio estás

```bash
pwd
```

📌 **Para qué sirve**
Muestra la ruta completa del directorio actual.

---

## 📍 3. Listar contenido del directorio actual

```bash
ls
```

📌 **Para qué sirve**
Muestra archivos y carpetas del directorio donde estás.

---

## 📍 4. Listar con detalle

```bash
ls -l
```

📌 **Para qué sirve**
Muestra permisos, dueño, tamaño y fecha de modificación.

---

## 📍 5. Ir al directorio raíz del sistema

```bash
cd /
pwd
```

📌 **Para qué sirve**
Te posiciona en el **nivel más alto del sistema de archivos**.

---

## 📍 6. Ver carpetas principales del sistema

```bash
ls
```

📌 **Para qué sirve**
Muestra las carpetas base del sistema Linux.

---

## 📍 7. Entrar a `/home` (usuarios)

```bash
cd /home
pwd
ls
```

📌 **Para qué sirve**
Aquí viven las carpetas de cada usuario del sistema.

---

## 📍 8. Volver a raíz

```bash
cd /
```

---

## 📍 9. Entrar a `/etc` (configuración)

```bash
cd /etc
pwd
ls
```

📌 **Para qué sirve**
Contiene **archivos de configuración** del sistema y servicios.

---

## 📍 10. Entrar a `/var` (datos variables)

```bash
cd /var
pwd
ls
```

📌 **Para qué sirve**
Guarda logs, colas, caché y datos que cambian con el tiempo.

---

## 📍 11. Instalar `tree` (si no está)

```bash
sudo dnf install tree -y
```

📌 **Para qué sirve**
Instala un comando que muestra carpetas en forma de árbol.

---

## 📍 12. Usar `tree` para visualizar estructura

```bash
tree /home
```

📌 **Para qué sirve**
Visualiza la jerarquía de directorios claramente.

---

## 📍 13. Directorios importantes (para el reporte)

| Directorio | Función                   |
| ---------- | ------------------------- |
| `/`        | Raíz del sistema          |
| `/home`    | Carpetas de usuarios      |
| `/etc`     | Configuración del sistema |
| `/var`     | Logs y datos variables    |
| `/bin`     | Comandos esenciales       |
| `/usr`     | Programas y librerías     |
| `/tmp`     | Archivos temporales       |

---

# 🟢 PARTE 2 – DISEÑO DEL SISTEMA DE ARCHIVOS (CMS)

## 📍 14. Crear estructura base del servidor web

```bash
sudo mkdir -p /var/www
```

📌 **Para qué sirve**
Crea la carpeta donde se alojarán los sitios web.

---

## 📍 15. Crear sitios web independientes

```bash
sudo mkdir -p /var/www/sitio1/{public_html,uploads,logs,config}
sudo mkdir -p /var/www/sitio2/{public_html,uploads,logs,config}
sudo mkdir -p /var/www/shared/backups
```

📌 **Para qué sirve**
Crea estructura separada para múltiples sitios web.

---

## 📍 16. Verificar estructura creada

```bash
tree /var/www
```

📌 **Para qué sirve**
Confirma que la estructura se creó correctamente.

---

## 📍 17. Configurar permisos de seguridad

### Public HTML (acceso web)

```bash
sudo chmod 755 /var/www/sitio1/public_html
sudo chmod 755 /var/www/sitio2/public_html
```

📌 **Para qué sirve**
Permite lectura pública de archivos web.

---

### Uploads (solo servidor y admin)

```bash
sudo chmod 750 /var/www/sitio1/uploads
sudo chmod 750 /var/www/sitio2/uploads
```

📌 **Para qué sirve**
Protege archivos subidos por usuarios.

---

### Configuración privada

```bash
sudo chmod 700 /var/www/sitio1/config
sudo chmod 700 /var/www/sitio2/config
```

📌 **Para qué sirve**
Evita acceso no autorizado a configuraciones sensibles.

---

### Logs

```bash
sudo chmod 750 /var/www/sitio1/logs
sudo chmod 750 /var/www/sitio2/logs
```

📌 **Para qué sirve**
Protege información de auditoría.

---

## 📍 18. Medidas de seguridad (para explicar)

✔ Separación de sitios
✔ Permisos restrictivos
✔ Backups centralizados
✔ Uso de usuarios por sitio
✔ SELinux activo
✔ HTTPS

---

# 🔴 PARTE 3 – SIMULACIÓN DE PLANIFICACIÓN DE DISCO

## 📍 19. Crear archivo Python

```bash
nano disk_scheduling.py
```

📌 **Para qué sirve**
Crea el archivo del programa de simulación.

---

## 📍 20. Pegar TODO el código

```python
def fcfs(requests, head):
    total = 0
    current = head
    for r in requests:
        total += abs(r - current)
        current = r
    return total


def sstf(requests, head):
    total = 0
    current = head
    pending = requests[:]

    while pending:
        closest = min(pending, key=lambda x: abs(x - current))
        total += abs(closest - current)
        current = closest
        pending.remove(closest)

    return total


def scan(requests, head, max_track=199):
    left = sorted([r for r in requests if r < head])
    right = sorted([r for r in requests if r >= head])

    total = 0
    current = head

    for r in right:
        total += abs(r - current)
        current = r

    total += abs(max_track - current)
    current = max_track

    for r in reversed(left):
        total += abs(r - current)
        current = r

    return total


requests = [95, 180, 34, 119, 11, 123, 62, 64]
head = 50

print("FCFS:", fcfs(requests, head))
print("SSTF:", sstf(requests, head))
print("SCAN:", scan(requests, head))
```

Guardar:

* `CTRL + O`
* `ENTER`
* `CTRL + X`

---

## 📍 21. Ejecutar el programa

```bash
python3 disk_scheduling.py
```

📌 **Para qué sirve**
Ejecuta la simulación de planificación de disco.

---

## 📍 22. Interpretación de resultados (para explicar)

| Algoritmo | Descripción                  |
| --------- | ---------------------------- |
| FCFS      | Atiende en orden de llegada  |
| SSTF      | Atiende la pista más cercana |
| SCAN      | Movimiento tipo elevador     |

---

## ✅ LISTO PARA ENTREGAR

Con esto tienes:
✔ Comandos ejecutados
✔ Evidencia práctica
✔ Diseño lógico
✔ Seguridad
✔ Código funcional
✔ Explicación completa

---

Si quieres, el **siguiente paso** puede ser:

* 📄 Reporte Word / PDF
* 🖊️ Diagrama del CMS
* ☕ Versión en Java
* 🎥 Guion para explicación en video

Dime qué sigue y lo armamos 🔥
