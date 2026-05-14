# BIA SSPD · Variables Tarifarias

Proceso automático para generar y validar los **20 archivos Excel por mercado** del Formato Variables Tarifarias SSPD (Superintendencia de Servicios Públicos Domiciliarios).

**Período actual:** Enero 2024 – Marzo 2026 · 27 meses · 15,120 celdas validadas

---

## ▶️ Abrir en Google Colab

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/allisoncubillos-bot/bia-sspd-variables-tarifarias/blob/main/BIA_SSPD_Proceso_Tarifario.ipynb)

El link siempre apunta a la última versión del notebook. Cada usuario autoriza su propia cuenta de Google Drive al ejecutarlo.

---

## ¿Qué hace?

| Fase | Descripción | Salida |
|------|-------------|--------|
| 1 | Llena el formato mensual (una hoja por mes, columnas por mercado) | `Formato Variables_202401-202603.xlsx` |
| 2 | Genera 20 archivos individuales por mercado (3 hojas por año) | 20 `.xlsx` en carpeta `Formato variables 202401-202603/` |
| 3 | Inserta los 3 valores DERIVEX CFG3 y limpia el relleno amarillo | Modifica los 20 archivos |
| 4 | Completa con `0` los meses sin operación DERIVEX | Modifica los 20 archivos |
| 5 | Valida cada celda contra la fuente `rates_period` | Reporte en consola |
| 6 | Genera reporte auditable con 200 spot-checks + sumas + canónicos | `REPORTE_VALIDACION.xlsx` |

---

## Estructura de carpetas requerida en Google Drive

```
Mi Drive/
└── INSPECCIÓN SSPD 2026/
    ├── RATES DEFINITIVO/
    │   ├── rates_period_1-2024.xlsx
    │   ├── ...
    │   └── rates_period_3-2026.xlsx     (27 archivos)
    │
    └── FORMATO VARIABLES/
        ├── FORMA MAPEO VARIABLES.xlsx
        ├── Formato Variables_202401-202603.xlsx
        ├── Formato Variables Tarifarias (202401-202603) - MERCADO.xlsx
        └── Formato variables 202401-202603/   (se crea automáticamente)
```

---

## Cómo se usa

1. Abrir el notebook con el link de Colab de arriba
2. Ejecutar la celda **Paso 0** (instala dependencias y autoriza Google Drive)
3. Revisar la celda **⚙️ Configuración** — editar solo si el nombre de la carpeta cambia
4. Ejecutar la celda **Verificar estructura** para confirmar que todos los archivos están en su lugar
5. Ejecutar las **fases 1 a 6 en orden**
6. Abrir `REPORTE_VALIDACION.xlsx` para auditar antes de entregar

Tiempo estimado de ejecución completa: **8–15 minutos**.

---

## Stack

- **Python 3** + `openpyxl 3.1.5`
- **Google Colab** como entorno de ejecución (sin instalación local)
- **Google Drive** como almacenamiento de entrada/salida
- **GitHub** para versionado y distribución del notebook

---

## Notas del período actual

- **Diciembre 2025 (CFG3 = 1.44):** el valor original llegó referenciado como "diciembre 2056"; se interpretó como diciembre 2025 (único mes con ese valor compatible con el rango del archivo). **Confirmar con el equipo regulatorio antes del próximo cierre.**
- **CASANARE:** queda con celdas vacías en febrero, marzo, abril, junio y julio de 2024 porque BIA no operó en ese mercado durante esos meses (los archivos `rates_period` correspondientes no contienen CASANARE). Es correcto, no es un error.
- **Acentos en mercados:** `NARIÑO` se normaliza automáticamente contra `NARINO` en la fuente. No hay que ajustar manualmente.
- **Resultado del último ciclo:** 0 discrepancias sobre 15,120 celdas validadas.

---

## Cómo actualizar para el próximo período

1. Subir los nuevos archivos `rates_period_M-AAAA.xlsx` a `RATES DEFINITIVO/`
2. Actualizar los valores `CFG3_ESPECIALES` en la celda **⚙️ Configuración** del notebook si los costos DERIVEX cambiaron
3. Ajustar la lista `MARKETS` si se incorpora o retira algún mercado
4. Ejecutar el notebook completo y revisar el reporte de validación

Para cambios al código, editar el notebook localmente y hacer `git push` — el link de Colab queda actualizado automáticamente para todo el equipo.

---

*Equipo BIA Energy · `team.energy@bia.app`*
