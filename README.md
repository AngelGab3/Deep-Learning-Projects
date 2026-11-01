# Deep Learning Projects

Colección de proyectos e implementaciones de **Aprendizaje Profundo** (*Deep Learning*), **Aprendizaje No Supervisado** (*Unsupervised Learning*) y **Preservación Topológica** (*Manifold Learning* / *Topological Mapping*), aplicados a problemas científicos de alta complejidad y astrofísica observacional.

Desarrollado y mantenido por **[Gabriel Velázquez](https://github.com/AngelGab3)**.

---

## 🌟 Proyectos Destacados

El repositorio reúne diversas arquitecturas, desde algoritmos clásicos de redes neuronales implementados desde cero hasta arquitecturas convolucionales acopladas a mapas auto-organizados (*Deep Embedded Self-Organizing Maps - DESOM*):

```
                               ┌────────────────────────────────────────────────────────┐
                               │                 Deep Learning Projects                 │
                               └───────────────────────────┬────────────────────────────┘
                                                           │
                    ┌──────────────────────────────────────┴──────────────────────────────────────┐
                    ▼                                                                             ▼
       ┌──────────────────────────┐                                                  ┌──────────────────────────┐
       │       MaNGA-DESOM        │                                                  │   Self-Organizing Maps   │
       ├──────────────────────────┤                                                  ├──────────────────────────┤
       │ • Autoencoders 1D & 2D   │                                                  │ • SOM desde cero (NumPy) │
       │ • Capas SOM entrenables  │                                                  │ • Mallas cuadradas y hex │
       │ • Espectroscopía MaNGA   │                                                  │ • Diagrama H-R estelar   │
       │ • Dashboard Interactivo  │                                                  │ • U-Matrix & Hit Maps    │
       └──────────────────────────┘                                                  └──────────────────────────┘
```

---

### 1. [MaNGA-DESOM](./MaNGA-DESOM/)
> **Deep Embedded Self-Organizing Maps aplicados a espectroscopía de campo integral (IFU) del sondeo SDSS-IV MaNGA.**

Replicación fiel y arquitectura de ingeniería optimizada para la clasificación no supervisada de la diversidad espectral de galaxias, basada en la metodología de *Teimoorinia et al. (The Astronomical Journal / [arXiv:2112.03425](https://arxiv.org/abs/2112.03425))*.

* **Arquitectura de Modelos:**
  * **DESOM-1:** Autoencoder Convolucional 1D + capa SOM (malla $15 \times 15$) para el aprendizaje y compresión latente de perfiles espectrales en el rango de longitud de onda `[3650, 8950] Å`.
  * **DESOM-2:** Autoencoder Convolucional 2D + capa SOM (malla $10 \times 10$) para agrupar las huellas dactilares espaciales (*galaxy fingerprints*) generadas por DESOM-1 y mapear la morfología global.
* **Componentes Clave de Ingeniería:**
  * **Pipeline Modular en 4 Etapas:** Descarga y Voronoi binning multinúcleo, consolidación de datos, entrenamiento DESOM-1 y entrenamiento DESOM-2 (`desom/cli/`).
  * **Procesamiento Paralelo CPU:** Distribución eficiente de apertura de cubos FITS LOGCUBE y binning con `ProcessPoolExecutor` y contexto `spawn`.
  * **Dashboard Web Astronómico:** Interfaz interactiva local en *Dark Mode* (`app.py`) con explorador espectral y proyección de huellas galácticas.
  * **Suite de Pruebas:** Pruebas automatizadas con `pytest` en `tests/test_pipeline.py`.
  * **Entorno Google Colab:** Notebook `Pipeline_Unificado.ipynb` optimizado para entrenamiento con GPUs en la nube o local.
* 📖 *Consulta la documentación completa en [MaNGA-DESOM/README.md](./MaNGA-DESOM/README.md).*

---

### 2. [Self-Organizing Maps (SOM)](./Self-Organizing-Maps/)
> **Implementación de mapas auto-organizados de Kohonen desde cero y reconstrucción del diagrama de Hertzsprung-Russell.**

Estudio teórico y práctico de la cuantización vectorial y proyección topológica de variedades no lineales sin depender de bibliotecas de alto nivel.

* **Implementación:**
  * Red neuronal SOM construida desde fundamentos matemáticos en Python puro y NumPy.
  * Soporte para topologías de vecindario en mallas tanto **cuadradas** como **hexagonales**.
  * Visualizaciones diagnósticas de interpretabilidad: **U-Matrix** (matriz de distancias unificadas), **planos de componentes**, mapa de densidad de impactos (*hit map*).
  * Métricas rigurosas de calidad topológica: Error de Cuantización ($QE$) y Error Topográfico ($TE$).
  * Clustering bi-etápico (SOM + K-Means) y optimización de hiperparámetros mediante *Grid Search*.
* **Aplicación Física:**
  * Mapeo no supervisado de 240 estrellas descritas por 4 variables astrofísicas (temperatura, luminosidad, radio y magnitud absoluta).
  * Reconstrucción autónoma de las ramas evolutivas del **diagrama de Hertzsprung-Russell (H-R)** demostrando la capacidad del algoritmo para redescubrir relaciones físicas conocidas sin etiquetas previas.
* 📖 *Consulta la documentación en [Self-Organizing-Maps/README.md](./Self-Organizing-Maps/README.md).*

---

### 3. Notebooks Experimentales y Prototipado
* **[`Test1_DESOM.ipynb`](./Test1_DESOM.ipynb):** Cuaderno interactivo desarrollado inicialmente en Google Colab (con aceleración por GPU T4) para la validación conceptual de la arquitectura DESOM y el análisis exploratorio de datos espectrales de MaNGA.

---

## 📂 Estructura del Repositorio

```text
Deep-Learning-Projects/
├── MaNGA-DESOM/                     # Pipeline completo DESOM para datos astrofísicos MaNGA
│   ├── desom/                       # Código fuente modular
│   │   ├── analysis/                # Métricas, huellas dactilares y evaluación
│   │   ├── cli/                     # Scripts ejecutables por línea de comandos (Etapas 1 a 4)
│   │   ├── data/                    # Descarga de catálogos, cubos FITS y procesamiento Voronoi
│   │   ├── models/                  # Capa SOM personalizada y Autoencoders 1D / 2D
│   │   ├── plots/                   # Generación de figuras científicas del paper
│   │   ├── training/                # Motores y esquemas de entrenamiento unificados
│   │   └── ui/                      # Servidor backend y frontend del dashboard web
│   ├── Paper Original/              # Código y referencias del paper base (arXiv:2112.03425)
│   ├── tests/                       # Pruebas unitarias automatizadas (pytest)
│   ├── app.py                       # Punto de entrada para el dashboard web interactivo
│   ├── Pipeline_Unificado.ipynb     # Notebook unificado para Google Colab
│   ├── requirements.txt             # Dependencias del proyecto MaNGA-DESOM
│   └── README.md                    # Documentación técnica detallada del subproyecto
│
├── Self-Organizing-Maps/            # Implementación desde cero de Kohonen SOM
│   ├── Self_Organizing_Maps.ipynb   # Notebook con teoría, implementación NumPy y aplicación H-R
│   └── README.md                    # Resumen y detalles de la implementación
│
├── Test1_DESOM.ipynb                # Validación experimental preliminar en Colab (GPU)
└── README.md                        # Documentación general del repositorio
```

---

## 🚀 Guía de Inicio Rápido (Quickstart)

### 1. Clonar el repositorio
```bash
git clone https://github.com/AngelGab3/Deep-Learning-Projects.git
cd Deep-Learning-Projects
```

### 2. Configurar el entorno virtual
Se recomienda utilizar un entorno virtual con Python 3.8 o superior:
```bash
python3 -m venv venv
source venv/bin/activate  # En macOS / Linux
# venv\Scripts\activate   # En Windows
```

### 3. Ejecutar los Proyectos

#### A. Explorar el proyecto MaNGA-DESOM
```bash
cd MaNGA-DESOM
pip install -r requirements.txt

# Iniciar el Dashboard Web:
python3 app.py --port 8050
# Acceder en el navegador a http://localhost:8050

# O ejecutar el pipeline completo por CLI:
python3 -m desom.cli.run_all --workers 4
```

#### B. Explorar los Mapas Auto-Organizados (SOM)
```bash
cd Self-Organizing-Maps
pip install numpy matplotlib scipy scikit-learn jupyter
jupyter notebook Self_Organizing_Maps.ipynb
```

---

## 🛠️ Tecnologías y Librerías

| Área | Tecnologías |
|---|---|
| **Lenguaje Principal** | Python 3.8+ |
| **Deep Learning & Modelado** | TensorFlow 2.x, Keras, NumPy, SciPy, Scikit-learn |
| **Astrofísica y Manejo de Datos** | Astropy, SDSS Marvin, FITS File Processing |
| **Visualización & Dashboard** | Matplotlib, Seaborn, Dashboard Web (Vanilla JS / HTML5 / CSS3) |
| **Calidad de Código y Testing** | PyTest, Flake8 |

---

## 📄 Referencias Científicas

* **Teimoorinia, H., Archinuk, F., Woo, J., et al. (2021):** *Mapping the Diversity of Galaxy Spectra using Deep Embedded Self-Organizing Maps*. [arXiv:2112.03425](https://arxiv.org/abs/2112.03425).
* **Kohonen, T. (1982):** *Self-organized formation of topologically correct feature maps*. Biological Cybernetics, 43(1), 59–69.

---

## 👤 Autor

**Gabriel Velázquez**
* GitHub: [@AngelGab3](https://github.com/AngelGab3)
