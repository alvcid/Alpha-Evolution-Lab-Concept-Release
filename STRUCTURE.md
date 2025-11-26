# Estructura de Carpetas Recomendada

Esta es la estructura de carpetas recomendada para el repositorio de GitHub.

```
alpha-evolution-lab/
│
├── README.md                    # Documentación principal
├── LICENSE                      # Licencia MIT con aviso de componentes propietarios
├── .gitignore                   # Archivos a ignorar en Git
│
├── docs/                        # Documentación adicional
│   ├── ARCHITECTURE.md          # Arquitectura del sistema
│   ├── EXAMPLES.md              # Ejemplos de uso
│   ├── FEATURES.md              # Lista de características
│   ├── PSEUDOCODE.md            # Pseudocódigo explicativo
│   ├── ROADMAP.md               # Roadmap de desarrollo
│   └── STRUCTURE.md              # Este archivo
│
├── src/                         # Código fuente (conceptual)
│   ├── core/                    # Motor de evolución
│   │   ├── __init__.py
│   │   ├── evolution_engine.py # Lógica principal de evolución
│   │   ├── population_manager.py # Gestión de poblaciones
│   │   └── selection_strategies.py # Estrategias de selección
│   │
│   ├── llm/                     # Integración con LLMs
│   │   ├── __init__.py
│   │   ├── llm_service.py       # Abstracción de servicios LLM
│   │   ├── prompt_templates.py  # Plantillas de prompts
│   │   └── mutation_strategies.py # Estrategias de mutación
│   │
│   ├── evaluation/              # Sistema de evaluación
│   │   ├── __init__.py
│   │   ├── backtest_engine.py   # Motor de backtesting
│   │   ├── metrics_calculator.py # Cálculo de métricas
│   │   └── validation.py        # Validación de código y datos
│   │
│   ├── data/                    # Pipeline de datos
│   │   ├── __init__.py
│   │   ├── data_loader.py       # Carga de datos
│   │   ├── preprocessor.py      # Preprocesamiento
│   │   └── market_data_api.py   # Integración con APIs
│   │
│   └── utils/                   # Utilidades
│       ├── __init__.py
│       ├── code_validator.py    # Validación de código Python
│       └── logger.py            # Sistema de logging
│
├── frontend/                    # Frontend React/TypeScript (conceptual)
│   ├── src/
│   │   ├── components/          # Componentes React
│   │   │   ├── AlphaCard.tsx
│   │   │   ├── StatsGraph.tsx
│   │   │   └── CodeViewer.tsx
│   │   │
│   │   ├── services/            # Servicios frontend
│   │   │   ├── llmService.ts
│   │   │   ├── dataService.ts
│   │   │   └── backtestService.ts
│   │   │
│   │   ├── types.ts             # Definiciones de tipos
│   │   └── App.tsx              # Componente principal
│   │
│   ├── package.json             # Dependencias npm
│   ├── tsconfig.json            # Configuración TypeScript
│   └── vite.config.ts           # Configuración Vite
│
├── notebooks/                   # Jupyter notebooks de ejemplo
│   ├── examples/
│   │   ├── basic_evolution.ipynb      # Ejemplo básico
│   │   └── custom_mutation.ipynb      # Mutación personalizada
│   │
│   └── analysis/
│       └── alpha_analysis.ipynb       # Análisis de alphas
│
├── examples/                    # Ejemplos y plantillas
│   ├── sample_prompts.md        # Ejemplos de prompts efectivos
│   └── example_outputs.json     # Ejemplos de salidas (sin datos reales)
│
├── tests/                       # Tests (conceptual)
│   ├── unit/                    # Tests unitarios
│   │   ├── test_evolution_engine.py
│   │   ├── test_metrics_calculator.py
│   │   └── test_code_validator.py
│   │
│   ├── integration/             # Tests de integración
│   │   └── test_full_evolution_cycle.py
│   │
│   └── fixtures/                # Datos de prueba
│       └── sample_market_data.csv
│
└── .github/                     # Configuración de GitHub
    ├── workflows/               # GitHub Actions (opcional)
    │   └── ci.yml
    │
    └── ISSUE_TEMPLATE/          # Plantillas de issues
        └── feature_request.md
```



