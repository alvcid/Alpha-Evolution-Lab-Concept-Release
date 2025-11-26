# Lista de Características

## Características Principales

### 1. Generación Automática de Alphas
- **Descripción**: Utiliza modelos de lenguaje (LLMs) para generar código de señales financieras a partir de descripciones de alto nivel
- **Beneficio**: Reduce el tiempo de desarrollo de semanas a horas
- **Tecnología**: Integración con Gemini y OpenAI con fallback automático

### 2. Evolución Guiada por IA
- **Descripción**: Sistema de mutación y selección que refina iterativamente las estrategias más prometedoras
- **Beneficio**: Mejora continua de alphas sin intervención manual
- **Estrategias**: Standard, Adaptive Volatility, Market Regime, Volume Filter

### 3. Evaluación Rigurosa
- **Descripción**: Backtesting completo con métricas estándar de la industria
- **Métricas**: IC, Sharpe, Sortino, Maximum Drawdown, Win Rate, Profit Factor
- **Validación**: Separación estricta in-sample / out-of-sample

### 4. Interfaz Visual Intuitiva
- **Descripción**: Dashboard web para monitorear el proceso de evolución en tiempo real
- **Componentes**: 
  - Visualización de alphas por generación
  - Gráficos de performance
  - Estadísticas agregadas
  - Controles de evolución

### 5. Validación Out-of-Sample
- **Descripción**: Separación estricta entre datos de entrenamiento y validación
- **Beneficio**: Previene overfitting y detecta problemas de generalización
- **Métricas**: IC Decay, Stability Score

### 6. Múltiples Estrategias de Mutación
- **Standard**: Mejora genérica incremental
- **Adaptive Volatility**: Adaptación a condiciones de volatilidad
- **Market Regime**: Detección y adaptación a cambios de régimen
- **Volume Filter**: Incorporación de filtros de volumen

### 7. Ejecución Segura de Código
- **Descripción**: Sandboxing mediante Pyodide para ejecutar código Python generado
- **Seguridad**: Validación de sintaxis, timeouts, límites de recursos
- **Aislamiento**: Prevención de acceso a sistema de archivos y red

### 8. Auto-Evolución
- **Descripción**: Proceso automatizado de múltiples iteraciones de evolución
- **Configuración**: Número de iteraciones, criterios de guardado
- **Resultado**: Alphas prometedores guardados automáticamente

### 9. Detección de Anomalías
- **Descripción**: Identificación automática de alphas sospechosos o con errores
- **Detecciones**: 
  - Look-ahead bias
  - Overfitting (IC decay alto)
  - Errores de sintaxis
  - Métricas irreales

### 10. Gestión de Población
- **Descripción**: Sistema para mantener diversidad y calidad en la población de alphas
- **Características**:
  - Elitismo (preservar mejores)
  - Diversidad (evitar estancamiento)
  - Limpieza de redundantes

## Características Técnicas

### Arquitectura Modular
- Separación clara de responsabilidades
- Fácil extensión y mantenimiento
- Componentes reutilizables

### Multi-Provider LLM
- Soporte para múltiples proveedores
- Fallback automático
- Abstracción unificada

### Type Safety
- TypeScript en frontend
- Type hints en Python
- Validación de tipos en runtime

### Performance
- Caching de resultados
- Procesamiento optimizado
- Lazy loading de componentes

## Características de Seguridad

### Sandboxing
- Ejecución aislada de código generado
- Prevención de acceso a recursos del sistema
- Límites de tiempo y memoria

### Validación de Código
- Verificación de sintaxis
- Detección de patrones peligrosos
- Rechazo automático de código inválido

### Manejo de Errores
- Recuperación graceful
- Logging detallado
- Notificaciones al usuario

## Características Futuras (Roadmap)

### Fase 2
- Múltiples timeframes
- Más fuentes de datos
- Combinación de alphas (ensemble)

### Fase 3
- Optimización de hiperparámetros
- Análisis avanzado de régimen
- Walk-forward analysis

### Fase 4
- Backend dedicado
- Persistencia de datos
- Monitoreo en tiempo real
- API REST

### Fase 5
- Machine Learning integrado
- Análisis de sentimiento
- Trading automatizado
- Marketplace de alphas

## Comparación con Alternativas

### Ventajas
- ✅ Automatización completa del proceso
- ✅ Integración con LLMs de última generación
- ✅ Validación rigurosa incorporada
- ✅ Interfaz visual intuitiva
- ✅ Extensible y modular

### Limitaciones Actuales
- ⚠️ Ejecución en navegador (limitaciones de rendimiento)
- ⚠️ Sin persistencia entre sesiones
- ⚠️ Procesamiento síncrono
- ⚠️ Un mercado a la vez

---

**Nota**: Esta lista refleja el estado actual del proyecto. Para características planificadas, ver ROADMAP.md.

