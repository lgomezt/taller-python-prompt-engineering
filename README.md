# Taller de Python — Clase 11: Prompt Engineering para Data Science

Repositorio de la Clase 11 del **Taller de Python para Economistas · Data Science con GenAI** (Maestría, Universidad de los Andes).

En esta sesión introducimos **Git y GitHub** como herramientas de trabajo, y después usamos **prompt engineering** con asistentes de IA (Cursor, Claude Code, Antigravity) para limpiar y analizar datos reales.

---

## Contenido del repositorio

```
taller-python-prompt-engineering/
├── README.md                              <- este archivo
├── AGENTS.md                              <- contexto para el agente IA (Cursor, etc.)
├── .gitignore
├── notebooks/
│   ├── 01_Intro_Git_GitHub.ipynb          <- Parte 1: Git/GitHub + tutorial practico
│   ├── 02_Tutorial_Cursor.ipynb           <- Parte 2: tutorial narrativo (el que lees)
│   └── 03_Analisis_Admisiones.ipynb       <- Parte 2: notebook de trabajo (donde Cursor escribe)
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

2. **Parte 2 — Prompt engineering con Cursor** (`notebooks/02_Tutorial_Cursor.ipynb`):
   - Instalar Cursor.
   - El prompt ingenuo vs el prompt bueno.
   - AGENTS.md y el harness.
   - Las tres recetas-prompt: **exploración**, **limpieza**, **modelado con Plan Mode**.
   - Se trabaja sobre `notebooks/03_Analisis_Admisiones.ipynb`.

## Datasets — resumen rápido

| Archivo | Filas | Columnas | Descripción |
|---|---|---|---|
| `data/admissions.csv` | 157 | 8 | Registros de admisión con `Student_ID` añadido. Incluye datos "sucios" a propósito: valores faltantes, edades negativas, porcentajes fuera de rango. |
| `data/bmi.csv` | 34,605 | 6 | Medidas antropométricas (altura, peso, edad, género) con `Student_ID`. Solo ~111 IDs coinciden con admisiones; el resto tienen prefijo `EXT_` (cohorte externa). |

Llave de join: `Student_ID`. Ver `AGENTS.md` para detalles.

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

3. Abrir los notebooks:
   ```bash
   jupyter lab notebooks/
   ```

4. Abrir el mismo folder en **Cursor** para la Parte 2.

## Licencia y uso

Material educativo — Universidad de los Andes, Maestría en Economía.
