<!--
==============================================================
ESTE ARCHIVO ES UN TEMPLATE. NO esta activo para el agente.
Cursor / Claude Code / Antigravity reconocen unicamente
archivos llamados exactamente `AGENTS.md` (o `CLAUDE.md` para
Claude Code).

Para activarlo: segui el Paso 6 del tutorial
notebooks/02_Tutorial_Cursor.ipynb, donde te vamos a pedir
que hagas:

    cp AGENTS_TEMPLATE.md AGENTS.md

Y a partir de ese momento el agente lee el contexto automatico.
==============================================================
-->

# AGENTS.md — Taller de Prompt Engineering para Data Science

Este archivo le da contexto persistente al agente (Cursor, Claude Code, Antigravity, Codex, etc.) cada vez que arranca una sesión en este repo.

## Proyecto

Taller educativo de **Data Science con GenAI** para estudiantes de maestría en economía (Universidad de los Andes).

Objetivo del análisis: **predecir si un estudiante es admitido (`Admission Status`)** combinando su registro de admisión con datos antropométricos (BMI).

## Datasets

Los datos viven en `./data/` y son **inmutables** — nunca los sobrescribas.

| Archivo | Separador | Filas | Columnas clave | Nota |
|---|---|---|---|---|
| `data/admissions.csv` | `,` | 157 | `Student_ID` (llave primaria), `Name`, `Age`, `Gender`, `Admission Test Score`, `High School Percentage`, `City`, `Admission Status` | Datos sucios a propósito: NAs, edades negativas, porcentajes fuera de rango. |
| `data/bmi.csv` | `;` | 34,605 | `Student_ID` (FK), `gender`, `measurement_code`, `height_m`, `weight_kg`, `age` | ~111 `Student_ID` matchean con admissions. El resto son `EXT_*` (no sirven para este análisis). |

La llave de join es `Student_ID`. `admissions` es la base — usamos LEFT JOIN desde admissions ← bmi.

## Convenciones

- Python 3.11+, pandas, numpy, statsmodels, scikit-learn, matplotlib.
- **NO uses librerías exóticas** (XGBoost, LightGBM, PyTorch, etc.). La audiencia son economistas, no ML engineers.
- Para modelos con coeficientes interpretables usa **statsmodels**, no sklearn.
- Para métricas de clasificación sí puedes usar sklearn.metrics.
- Estilo: funciones cortas, docstrings de 1 línea, comentarios en español explicando el **por qué**, no el qué.
- Naming: `snake_case` en variables y funciones. Los datasets vienen con nombres `Title Case` — normalízalos al cargar.

## Estructura del repo

```
./
├── AGENTS.md                           ← este archivo
├── README.md                           ← descripción del repo
├── data/                               ← INMUTABLE
│   ├── admissions.csv
│   └── bmi.csv
├── notebooks/
│   ├── 01_Intro_Git_GitHub.ipynb       ← tutorial de git
│   ├── 02_Tutorial_Cursor.ipynb        ← tutorial narrativo (el que lee el estudiante)
│   └── 03_Analisis_Admisiones.ipynb    ← notebook de trabajo (donde Cursor escribe código)
└── outputs/                            ← artefactos generados por el agente
    ├── figures/                        ← .png
    ├── eda_summary.md                  ← resumen de exploración
    ├── analysis_clean.parquet          ← dataset limpio final
    ├── analysis_clean.csv              ← versión CSV para inspección humana
    └── model_report.md                 ← resultados del modelado
```

## Reglas operativas para el agente

1. **Nunca modifiques `data/`**. Todo artefacto derivado va a `outputs/`.
2. **Un archivo, una responsabilidad**. Si un análisis produce más de 3 outputs diferentes, sepáralos en archivos distintos. No devuelvas un monolito.
3. **Documenta decisiones**. Cuando tomes una decisión ambigua (imputar vs eliminar, OLS vs logit, etc.), deja un comentario `# DECISIÓN: ...` en el código y expande en el markdown.
4. **Progressive disclosure**. No cargues el contenido completo de archivos grandes al contexto; usa `.head()`, `.info()`, `.describe()` y deja que el usuario pida más si necesita.
5. **Cuando uses Plan Mode**, genera un plan con máximo 10 pasos y archivos target específicos. No inventes abstracciones.
6. **Si no sabes algo del dataset**, léelo primero (1-2 filas) en lugar de asumir.

## Flujo esperado

El estudiante irá leyendo `notebooks/02_Tutorial_Cursor.ipynb` y pegándote prompts-receta. Tú respondes escribiendo/ejecutando código en `notebooks/03_Analisis_Admisiones.ipynb`, que ya tiene la estructura por secciones.

Las secciones del notebook 03 están alineadas con el tutorial:
- § 1 Exploración (EDA individual por dataset)
- § 2 Limpieza + merge
- § 3 Modelado (LPM + logit)
- § 4 Presentación de resultados

No saltes secciones sin confirmar con el usuario.

## Comandos útiles

```bash
# Correr un notebook sin abrirlo (útil para validar que el código no rompa)
jupyter nbconvert --to notebook --execute notebooks/03_Analisis_Admisiones.ipynb --inplace

# Ver el último estado del dataset limpio
python -c "import pandas as pd; print(pd.read_parquet('outputs/analysis_clean.parquet').info())"
```

## Lo que NO sabes sin leer el código

- La columna `measurement_code` de bmi.csv **no tiene uso definido** — es probablemente ruido. Sugiere descartarla, no inventes interpretación.
- Los `Student_ID` con prefijo `EXT_*` **no pertenecen a admissions**. Son registros sobrantes de una cohorte externa.
- El profesor generó los datos con un script (`scripts/prepare_datasets.py`) que está gitignored — no lo busques, no lo necesitas.
