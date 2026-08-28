# Guía: Cómo Exportar Jupyter Notebooks en VS Code

Bienvenido a esta breve guía. Aquí aprenderás cómo exportar tus archivos de Jupyter Notebook (`.ipynb`) a diferentes formatos (como HTML, PDF o scripts de Python) directamente desde Visual Studio Code, y cómo solucionar los problemas de dependencias más comunes.

---

## 1. Pasos para exportar tu archivo

1. Abre tu archivo `.ipynb` dentro de Visual Studio Code.
2. En la barra de herramientas superior del notebook (donde están los botones de ejecutar celdas), busca el botón que dice **"Export"** (Exportar). Si no lo ves, haz clic en los tres puntos **"..."** para desplegar más acciones.

> [!TIP]
> **Atajo rápido:** También puedes usar la Paleta de Comandos (`Ctrl + Shift + P` en Windows/Linux o `Cmd + Shift + P` en Mac) y escribir `Jupyter: Export to...`.

3. Selecciona el formato deseado en el menú desplegable (por ejemplo, HTML o PDF).

---

## 2. Instalación de complementos faltantes

Si es la primera vez que exportas un archivo o ejecutas código en ese entorno, es muy probable que VS Code detecte que te faltan algunas herramientas (como el motor de exportación `nbconvert` o el propio Kernel de Python).

> [!IMPORTANT]
> **Si VS Code te muestra una ventana emergente en la esquina inferior derecha pidiendo instalar el kernel, el paquete de exportación o cualquier complemento faltante, simplemente dale clic al botón "Install" (Instalar).**

El editor intentará descargar y configurar todo automáticamente.

---

## 3. Solución de errores comunes (Troubleshooting)

### Error de compilación con `pyzmq`

**Mensaje de error típico:**
```text
Export failed ERROR: Failed to build 'pyzmq' when getting requirements to build wheel
```

> [!NOTE]
> **¿Por qué sucede?**
> Este error ocurre porque el proceso automático de VS Code intenta forzar la instalación de una versión antigua de las librerías (`"jupyter-client<8" "pyzmq<25"`). Al no ser compatibles con versiones recientes de Python, el sistema intenta compilar el código fuente desde cero y falla si no encuentra las herramientas de C++ instaladas en tu computadora.

### La Solución Definitiva

Para arreglar esto y saltarte la restricción del editor, debes instalar las versiones más actualizadas manualmente. 

1. Abre la terminal integrada de VS Code (puedes usar el atajo `Ctrl + ñ` o ir al menú superior `Terminal > New Terminal`).
2. Copia y pega exactamente el siguiente comando y presiona Enter:

```bash
python.exe -m pip install -U notebook jupyter-client pyzmq
```

Este comando fuerza la actualización (`-U`) de los paquetes clave utilizando sus versiones más recientes precompiladas. Una vez que termine de instalarse, intenta exportar tu documento nuevamente y funcionará a la perfección.
