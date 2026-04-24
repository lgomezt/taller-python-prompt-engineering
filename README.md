# Taller de Python — Clase 11: Prompt Engineering para Data Science

Repositorio de la Clase 11 del **Taller de Python para Economistas · Data Science con GenAI** (Maestría, Universidad de los Andes).

En esta sesión introducimos **Git y GitHub** como herramientas de trabajo, y después usamos **prompt engineering** con asistentes de IA (Cursor, Claude Code, Antigravity) para limpiar y analizar datos reales.

---

## Contenido del repositorio

```
taller-python-prompt-engineering/
├── README.md                              <- este archivo
├── AGENTS_TEMPLATE.md                     <- template del contexto para el agente
├── .gitignore
├── notebooks/
│   ├── 01_Intro_Git_GitHub.ipynb          <- Parte 1: Git/GitHub + tutorial practico
│   ├── 02_Tutorial_Cursor.ipynb           <- Parte 2: tutorial narrativo (el que lees)
│   ├── 03_EDA.ipynb                       <- Seccion 1: exploracion
│   ├── 04_Limpieza.ipynb                  <- Seccion 2: limpieza + merge
│   ├── 05_Modelado.ipynb                  <- Seccion 3: modelado con Plan Mode
│   └── 06_Reporte.ipynb                   <- Seccion 4: reporte final
├── data/                                  <- INMUTABLE
│   ├── admissions.csv                     <- base de admisiones (con Student_ID, aun sucia)
│   └── bmi.csv                            <- datos antropometricos (con Student_ID)
└── outputs/                               <- artefactos que vas a generar con Cursor
    └── figures/                           <- graficas del EDA y del modelo
```

## Flujo de la sesión

1. **Parte 1 — Git y GitHub** (`notebooks/01_Intro_Git_GitHub.ipynb`):
   - Qué es Git vs GitHub.
   - Instalar Git en Mac/Windows.
   - Clonar este repo.

2. **Parte 2 — Prompt engineering con Cursor** (`notebooks/02_Tutorial_Cursor.ipynb` + los notebooks `03_EDA` → `06_Reporte`):
   - Instalar Cursor.
   - El prompt ingenuo vs el prompt bueno.
   - `AGENTS_TEMPLATE.md` y el harness (+ cómo activar `AGENTS.md`).
   - Las tres recetas-prompt:
     - **exploración** en `03_EDA.ipynb`
     - **limpieza + merge** en `04_Limpieza.ipynb`
     - **modelado con Plan Mode** en `05_Modelado.ipynb`
   - Reporte ejecutivo en `06_Reporte.ipynb`.

> **Nota pedagógica**: dividimos el análisis en 4 notebooks a propósito. Un archivo = un *concern* es buena práctica de ciencia de datos: cada notebook lee los outputs intermedios del anterior y escribe los suyos en `outputs/`. Esto hace más manejable el análisis, fácil de debugear y fácil de iterar por secciones.

## Datasets — resumen rápido

| Archivo | Filas | Columnas | Descripción |
|---|---|---|---|
| `data/admissions.csv` | 157 | 8 | Registros de admisión con `Student_ID` añadido. Incluye datos "sucios" a propósito: valores faltantes, edades negativas, porcentajes fuera de rango. |
| `data/bmi.csv` | 34,605 | 6 | Medidas antropométricas (altura, peso, edad, género) con `Student_ID`. Solo ~111 IDs coinciden con admisiones; el resto tienen prefijo `EXT_` (cohorte externa). |

Llave de join: `Student_ID`. Ver `AGENTS_TEMPLATE.md` para detalles.

## ⚠️ Nota importante sobre los datos

**GitHub NO es un repositorio para compartir datos.** En esta clase los incluimos por simplicidad (son pequeños y públicos), pero:

- En proyectos reales los datos viven en S3, Google Cloud Storage, bases de datos o servidores internos.
- Datos personales/sensibles en un repo pueden violar leyes (Habeas Data, GDPR, HIPAA).
- Git está diseñado para texto (código), no para archivos binarios grandes.

Ver la sección 6 del notebook `notebooks/01_Intro_Git_GitHub.ipynb` para la discusión completa.

## Cómo empezar

1. Clonar el repositorio:
   ```bash
   git clone https://github.com/TU_USUARIO/taller-python-prompt-engineering.git
   cd taller-python-prompt-engineering
   ```

2. Instalar dependencias:
   ```bash
   pip install jupyterlab pandas numpy matplotlib seaborn scikit-learn statsmodels pyarrow
   ```

3. Abrir los notebooks y Cursor:
   ```bash
   jupyter lab notebooks/
   ```
   Y en paralelo abrir la misma carpeta en **Cursor** para la Parte 2.

## Licencia y uso

Material educativo — Universidad de los Andes, Maestría en Economía.
