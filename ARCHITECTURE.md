# Arquitectura del Sistema

## Visión General

Alpha Evolution Lab está diseñado como un sistema modular con separación clara entre la lógica de evolución, evaluación y presentación. La arquitectura permite escalabilidad horizontal y extensibilidad mediante plugins.

## Componentes Principales

### 1. Frontend Layer (React/TypeScript)

**Responsabilidades:**
- Interfaz de usuario para control y visualización
- Gestión de estado de alphas y generaciones
- Comunicación con servicios backend
- Visualización de métricas y estadísticas

**Tecnologías:**
- React 19+ para UI
- TypeScript para type safety
- Vite para build tooling
- Recharts para visualización de datos

### 2. LLM Service Layer

**Responsabilidades:**
- Abstracción de múltiples proveedores de LLM (Gemini, OpenAI)
- Gestión de fallback automático
- Construcción de prompts especializados
- Parsing de respuestas del LLM

**Estrategias de Mutación:**
- Standard: Mutación genérica basada en mejoras incrementales
- Adaptive Volatility: Adaptación según condiciones de volatilidad
- Market Regime: Detección y adaptación a cambios de régimen
- Volume Filter: Incorporación de filtros de volumen

### 3. Evolution Engine

**Responsabilidades:**
- Gestión del ciclo de vida de poblaciones
- Implementación de algoritmos de selección
- Coordinación de mutaciones
- Detección de convergencia

**Algoritmo de Selección:**
- Elitismo: Top N alphas se preservan
- Diversidad: Inclusión de alphas aleatorios para evitar estancamiento
- Criterios de parada: Convergencia, overfitting, límite de iteraciones

### 4. Backtesting Framework

**Responsabilidades:**
- Ejecución segura de código Python generado
- Cálculo de métricas de rendimiento
- Validación de código antes de ejecución
- Manejo de errores y timeouts

**Tecnologías:**
- Pyodide para ejecución de Python en el navegador
- Validación de sintaxis antes de ejecución
- Sandboxing para seguridad

### 5. Data Pipeline

**Responsabilidades:**
- Carga de datos históricos de mercado
- Preprocesamiento y normalización
- División train/validation/test
- Gestión de cache

**Fuentes de Datos:**
- APIs de mercado (EODHD, etc.)
- Archivos CSV locales
- Formatos estándar OHLCV

### 6. Metrics Calculator

**Responsabilidades:**
- Cálculo de Information Coefficient (IC)
- Métricas de riesgo (Sharpe, Sortino, Drawdown)
- Métricas de trading (Win Rate, Profit Factor)
- Validación de métricas (detección de anomalías)

## Flujos de Datos

### Flujo de Generación Inicial

```
User Prompt → LLM Service → Parse Response → Alpha Objects → UI Display
```

### Flujo de Evolución

```
Current Population → Selection → LLM Mutation → New Alphas → Evaluation → Population Update
```

### Flujo de Evaluación

```
Alpha Code → Code Validation → Backtest Execution → Metrics Calculation → Score Assignment
```

## Patrones de Diseño

### Strategy Pattern
- Múltiples estrategias de mutación intercambiables
- Diferentes algoritmos de selección

### Factory Pattern
- Creación de alphas desde respuestas de LLM
- Construcción de modelos de evaluación

### Observer Pattern
- Notificaciones de cambios en población
- Actualización de UI en tiempo real

## Consideraciones de Seguridad

### Ejecución de Código
- Sandboxing mediante Pyodide
- Validación de sintaxis antes de ejecución
- Timeouts para prevenir bucles infinitos
- Límites de recursos (memoria, CPU)

### Datos Sensibles
- API keys almacenadas en variables de entorno
- No exposición de datos de mercado en logs
- Sanitización de inputs de usuario

## Escalabilidad

### Horizontal Scaling
- Servicios stateless permiten múltiples instancias
- Queue system para procesamiento asíncrono (futuro)

### Vertical Scaling
- Caching de resultados de evaluación
- Optimización de llamadas a LLM (batching)

## Extensibilidad

### Nuevos Proveedores de LLM
- Interfaz común para servicios LLM
- Implementación de adapters para nuevos proveedores

### Nuevas Métricas
- Sistema de plugins para métricas personalizadas
- Registro de métricas en base de datos (futuro)

### Nuevas Estrategias de Mutación
- Interfaz para estrategias personalizadas
- Configuración mediante archivos JSON

## Limitaciones Actuales

1. **Ejecución en Navegador**: Pyodide tiene limitaciones de rendimiento
2. **Datos en Memoria**: No hay persistencia de resultados entre sesiones
3. **Procesamiento Síncrono**: Las evaluaciones bloquean la UI
4. **Un solo Mercado**: Soporte limitado a un ticker a la vez

## Mejoras Futuras

1. **Backend Dedicado**: Migración a servidor para mejor rendimiento
2. **Base de Datos**: Persistencia de alphas y resultados
3. **Procesamiento Asíncrono**: Queue system para evaluaciones
4. **Multi-Mercado**: Soporte para múltiples instrumentos simultáneos

