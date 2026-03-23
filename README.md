# La máquina estocástica

**Procesos aleatorios, redes neuronales y modelos generativos para físicos**

*J. A. Chala Casanova*

---

## Qué es este libro

Un texto para estudiantes de posgrado en física que quieren llegar a los modelos generativos modernos (difusión, flow matching) desde las herramientas que ya dominan: mecánica estadística, ecuaciones diferenciales estocásticas, teoría de la información.

La tesis central es que el aprendizaje automático moderno **es** física estadística en dimensión alta. La ecuación de Fokker-Planck que describe la distribución estacionaria del SGD es la misma que describe la distribución de neutrones en un sistema de fisión crítico. El score $\nabla\log p_t$ que guía la generación de imágenes es la misma cantidad que aparece en la condición de balance detallado. El puente de Schrödinger que unifica los modelos de difusión es el mismo problema variacional que Schrödinger formuló en 1931 pensando en partículas brownianas. No son analogías: son identidades matemáticas.

## Estructura

El libro tiene 12 capítulos en tres arcos, 5 apéndices y un sistema de secciones opcionales ("Estrellas Polares") que aplican cada capítulo a sistemas físicos concretos.

### Arco I — La red neuronal desde cero (Caps. 1–4)

| Cap. | Título | Contenido central |
|------|--------|-------------------|
| 1 | El problema de aproximación de funciones | Familias paramétricas, ecuaciones normales, RBFs como puente a redes neuronales, fenómeno de Runge |
| 2 | Sobreajuste, regularización y la descomposición espectral | Sesgo-varianza, Tikhonov, SVD como modos normales del ajuste, filtro de Wiener |
| 3 | Geometría del espacio de parámetros | Gradiente, hessiano, índice de Morse, convexidad, saddle points en alta dimensión (GOE) |
| 4 | Redes neuronales: el aproximador universal | MLP, activaciones (sigmoide = Fermi-Dirac, ReLU), teorema universal, profundidad vs. anchura |

Un ejemplo unificado del **oscilador armónico** recorre los cuatro capítulos como laboratorio práctico.

### Arco II — Ruido, incertidumbre y estructura (Caps. 5–9)

| Cap. | Título | Contenido central |
|------|--------|-------------------|
| 5 | SGD y la ecuación de Langevin | SGD como SDE de Langevin, Fokker-Planck del SGD, distribución de Gibbs, $T_{\text{eff}} = \eta c/2$ |
| 6 | Backpropagation como método adjunto | Principio de Pontryagin, adjunto continuo, gradient checkpointing |
| 7 | Probabilidad, inferencia y el fundamento estadístico | MLE, MAP, ELBO, VAE, truco de reparametrización, cotas VC |
| 8 | El MLP en la práctica | Ciclo de entrenamiento, dropout, normalización, double descent (Marchenko-Pastur) |
| 9 | Arquitecturas especializadas | CNNs (Lema de Schur), GNNs (Weisfeiler-Leman), transformers, equivarianza SO(3) (Clebsch-Gordan), Neural ODEs |

### Arco III — Hacia los modelos generativos (Caps. 10–12)

| Cap. | Título | Contenido central |
|------|--------|-------------------|
| 10 | Cálculo de Itô | Variación cuadrática, integral de Itô, fórmula de Itô, Feynman-Kac |
| 11 | De Fokker-Planck al score matching | FP por dualidad $L^2$, teorema de Anderson, DSM, puente de Schrödinger, transporte óptimo, flow matching |
| 12 | Modelos de difusión y flow matching | DDPM, score SDE, DDIM, rectified flow, OT flow matching, CFG, U-Net, DiT, latent diffusion |

### Apéndices

| Ap. | Contenido |
|-----|-----------|
| A | Probabilidad avanzada (filtración, esperanza condicional, martingalas) |
| B | Información y mecánica estadística (Shannon = Boltzmann, Gibbs, H-teorema, tabla de correspondencias ML–física) |
| C | Álgebra lineal (SVD, pseudoinversa, $L^2$ como Hilbert) |
| D | Algoritmos de implementación (Euler-Maruyama, Milstein, DSM loop, referencia NumPy/PyTorch/JAX) |
| E | Diccionario ML–física (glosario temático con análogos físicos) |

### Estrellas Polares

Secciones opcionales al final de cada capítulo que aplican los resultados a dos sistemas físicos: la cinética puntual estocástica del reactor de investigación IAN-R1 (Caps. 1–8) y la simulación de cascadas electromagnéticas en calorímetros de altas energías (Caps. 9–12). Pueden omitirse sin perder continuidad.

## Público objetivo

Estudiante de posgrado en física (o de último año de licenciatura con motivación suficiente) que ha tomado cursos de mecánica clásica, electromagnetismo, mecánica cuántica, mecánica estadística y métodos matemáticos. Se asume familiaridad con EDOs/EDPs, álgebra lineal y cálculo multivariable. Se asume que sabe programar pero nunca ha implementado una red neuronal. No se asume conocimiento de física nuclear ni de altas energías.

## Convenciones

- Escalares: itálica ($x, t, \lambda$). Vectores: negrita minúscula ($\bm{x}, \bm{\theta}$). Matrices: negrita mayúscula ($\bm{W}, \bm{H}$).
- Notación $f(\bm{x};\bm{\theta})$: punto y coma separa entradas de parámetros.
- Cada sección indica su nivel de exigencia en dos ejes: dificultad matemática y dificultad física (★ a ★★★★★).
- Anglicismos técnicos conservados en inglés (*score matching*, *flow matching*, *dropout*, *batch normalization*).
- Sistema de coloreo semántico de ecuaciones (3 ejes: rol sintáctico, estatus epistémico, tipo matemático). Desactivable con `\eqcolorsfalse`.

## Compilación

Requiere una instalación completa de TeX Live o MiKTeX.

```bash
# Con latexmk (recomendado)
latexmk -pdf main.tex

# Manual
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

## Estructura del proyecto

```
.
├── main.tex                     # Documento raíz
├── metadata.tex                 # Título, autor, metadatos PDF
├── references.bib               # Bibliografía centralizada
├── config/
│   ├── packages.tex             # Carga de paquetes (~30)
│   ├── geometry.tex             # Layout de página, headers/footers
│   ├── hyperref.tex             # Configuración de hipervínculos
│   ├── macros.tex               # Macros de matemáticas/física
│   ├── tcolorbox-config.tex     # Estilo base de cajas
│   ├── titles-config.tex        # Formato de capítulos/secciones
│   ├── listings-catppuccin.tex  # Listings de código (10 lenguajes)
│   ├── algorithms.tex           # Estilo de Algorithm2e
│   ├── tables-config.tex        # Tablas con overflow y colores
│   ├── equation-styles.tex      # Coloreo semántico de ecuaciones
│   ├── pgfplots-config.tex      # Estilos de gráficas
│   └── captions-config.tex      # Formato de captions
├── environments/
│   ├── generator.tex            # Fábrica de entornos
│   ├── instances.tex            # Entornos concretos
│   └── specials.tex             # Ejercicios, dificultad, notas bib
├── themes/
│   ├── catppuccin-palette.tex   # Tema principal (Latte/Frappé/Macchiato/Mocha)
│   ├── catppuccin-latte.tex     # Configuración alternativa
│   └── custom-theme.tex         # Fallback sin Catppuccin
├── frontmatter/
│   ├── titlepage.tex            # Página de título
│   ├── preliminary.tex          # Dedicatoria, epígrafe
│   └── preface.tex              # Prefacio
├── chapters/
│   ├── chapter1.tex             # Cap. 1: Aproximación de funciones
│   ├── chapter2.tex             # Cap. 2: Sobreajuste y regularización
│   ├── ...
│   └── chapter12.tex            # Cap. 12: Modelos de difusión
├── backmatter/
│   ├── appendixA.tex            # Probabilidad avanzada
│   ├── ...
│   └── appendixE.tex            # Diccionario ML–física
├── figs/                        # Figuras
└── code/                        # Código auxiliar
```

## Entornos disponibles

| Entorno | Color | Contador | Uso |
|---------|-------|:--------:|-----|
| `definicion` | Azul | ✓ | Definiciones formales |
| `teorema` | Malva | ✓ | Teoremas con demostración |
| `proposicion` | Verde | ✓ | Proposiciones y lemas |
| `ejemplo` | Durazno | ✓ | Ejemplos desarrollados |
| `observacion` | Gris | — | Comentarios y observaciones |
| `fisicaconexion` | Zafiro | — | Conexiones con la física |
| `estrella` | Amarillo | ✓ | Secciones de Estrella Polar |
| `ejerciciocomp` | Rosa | ✓ | Ejercicios computacionales |
| `ejercicio` | — | ✓ | Ejercicios teóricos (sin caja) |
| `notasbib` | Gris claro | — | Notas bibliográficas |

## Temas visuales

Basado en la paleta [Catppuccin](https://catppuccin.com). Para cambiar de sabor:

```latex
% En themes/catppuccin-palette.tex
\usepackage[Latte,styleAll]{catppuccinpalette}    % claro (por defecto)
%\usepackage[Mocha,styleAll]{catppuccinpalette}   % oscuro
```

Para sabores oscuros (Frappé, Macchiato, Mocha), descomentar `\darkthemetrue`.

## Estado del proyecto

| Componente | Estado |
|------------|--------|
| Caps. 1–4 (Arco I) | v3 — reescritura completa con narrativa reforzada, ejemplo del oscilador, RBFs |
| Caps. 5–9 (Arco II) | v2 — estable |
| Caps. 10–12 (Arco III) | v2 — estable |
| Apéndices A–E | v2 — estable |
| Prefacio | v2 — estable |
| Plantilla LaTeX | Estable |
| Bibliografía | Actualizada (Caps. 1–4 v3) |

## Licencia

Plantilla LaTeX bajo licencia [MIT](LICENSE). Contenido del libro © J. A. Chala Casanova. Paleta Catppuccin © contribuidores de Catppuccin.

## Autor

**J. A. Chala Casanova** — [GitHub](https://github.com/Zessinthel) · [GitLab](https://gitlab.com/Zessinthel)
