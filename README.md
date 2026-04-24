# Taller de Python — Clase 11: Prompt Engineering para Data Science

Repositorio de la Clase 11 del **Taller de Python para Economistas · Data Science con GenAI** (Maestría, Universidad de los Andes).

En esta sesión introducimos **Git y GitHub** como herramientas de trabajo, y después usamos **prompt engineering** con asistentes de IA (Claude Code, Cursor, Antigravity) para limpiar y analizar datos reales.

---

## Contenido del repositorio

```
taller-python-prompt-engineering/
├── README.md                           <- este archivo
├── .gitignore
├── notebooks/
│   └── 01_Intro_Git_GitHub.ipynb       <- notebook explicativo + tutorial
└── data/
    ├── admissions.csv                  <- base de admisiones (con Student_ID, aun sucia)
    └── bmi.csv                         <- datos antropometricos (con Student_ID)
```

## Datasets — resumen rápido

| Archivo | Filas | Columnas | Descripción |
|---|---|---|---|
| `data/admissions.csv` | 157 | 8 | Registros de admisión con `Student_ID` añadido. |
| `data/bmi.csv` | 34,605 | 6 | Medidas antropométricas (altura, peso, edad, género) con `Student_ID` |


## ⚠️ Nota importante sobre los datos

**GitHub NO es un repositorio para compartir datos.** En esta clase los incluimos por simplicidad (son pequeños y públicos), pero:

- En proyectos reales los datos viven en S3, Google Cloud Storage, bases de datos o servidores internos.
- Datos personales/sensibles en un repo pueden violar leyes (Habeas Data, GDPR, HIPAA).
- Git está diseñado para texto (código), no para archivos binarios grandes.

Ver la sección 6 del notebook `notebooks/01_Intro_Git_GitHub.ipynb` para la discusión completa.

## Cómo empezar

1. Clonar el repositorio:
   ```bash
   git clone https://github.com/lgomezt/taller-python-prompt-engineering
   cd taller-python-prompt-engineering
   ```
   
2. Abrir el notebook:
   ```bash
   jupyter lab notebooks/01_Intro_Git_GitHub.ipynb
   ```
