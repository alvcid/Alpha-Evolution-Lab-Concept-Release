# Ejemplos de Prompts Efectivos

Esta guía proporciona ejemplos de prompts efectivos para generar alphas con Alpha Evolution Lab.

## Principios de Prompts Efectivos

### ✅ Características de un Buen Prompt

1. **Específico**: Define claramente el objetivo y tipo de señal
2. **Con Restricciones**: Incluye límites de complejidad y líneas de código
3. **Con Contexto**: Menciona condiciones de mercado o características deseadas
4. **Realista**: Expectativas alineadas con métricas típicas de la industria

### ❌ Errores Comunes

1. **Demasiado Vago**: "Haz un alpha bueno"
2. **Sin Restricciones**: Permite código excesivamente complejo
3. **Expectativas Irreales**: "IC de 0.10 o más"
4. **Sin Contexto**: No menciona condiciones de mercado

## Ejemplos por Categoría

### 1. Reversión de Precio

#### Ejemplo 1: Reversión Simple
```
Genera un alpha que identifique oportunidades de reversión después de 
movimientos extremos de precio. Usa RSI o momentum para detectar condiciones 
sobrecompradas/sobrevendidas. El código debe ser simple, máximo 15 líneas.
```

#### Ejemplo 2: Reversión con Volumen
```
Crea un alpha de reversión que combine:
- Movimientos extremos de precio (últimos 2% de rango)
- Confirmación de volumen anormal (volumen > 1.5x promedio)
- Filtro de tendencia (solo reversión contra tendencia)

Máximo 20 líneas de código Python.
```

### 2. Momentum y Tendencia

#### Ejemplo 3: Seguimiento de Tendencia
```
Genera un alpha que identifique tendencias alcistas usando:
- Media móvil cruzada (corto plazo > largo plazo)
- Momentum positivo (retorno > 0 en ventana de 5 días)
- Filtro de volatilidad (evitar señales en alta volatilidad)

Código máximo 25 líneas.
```

#### Ejemplo 4: Momentum con Confirmación
```
Crea un alpha de momentum que requiera:
- Precio por encima de media móvil de 20 días
- Aceleración de momentum (cambio en tasa de cambio)
- Volumen creciente como confirmación

Máximo 20 líneas.
```

### 3. Volumen y Liquidez

#### Ejemplo 5: Anomalías de Volumen
```
Genera un alpha que detecte oportunidades basadas en:
- Volumen anormalmente alto (> 2x promedio de 20 días)
- Movimiento de precio acompañante
- Contexto de rango vs tendencia

Código simple, máximo 18 líneas.
```

### 4. Volatilidad

#### Ejemplo 6: Estrategia de Volatilidad
```
Crea un alpha que se adapte a diferentes regímenes de volatilidad:
- Alta volatilidad: reducir exposición
- Baja volatilidad: aumentar exposición
- Usar Bollinger Bands o ATR para medir volatilidad

Máximo 22 líneas de código.
```

### 5. Multi-Factor

#### Ejemplo 7: Combinación de Factores
```
Genera un alpha que combine múltiples señales:
- Factor 1: Momentum (retorno 5 días)
- Factor 2: Volumen (ratio volumen actual/promedio)
- Factor 3: Volatilidad (ATR normalizado)

Señal final = promedio ponderado de los 3 factores.
Máximo 25 líneas.
```

## Prompts para Evolución

### Mejora Incremental
```
Mejora el siguiente alpha para mayor robustez:
[alpha code aquí]

Enfócate en:
- Manejo de casos extremos
- Filtros adicionales para reducir falsos positivos
- Mantener la lógica central intacta

Genera 5 variantes mejoradas.
```

### Adaptación a Condiciones
```
Adapta este alpha para diferentes condiciones de mercado:
[alpha code aquí]

Considera:
- Ajuste dinámico de umbrales según volatilidad
- Filtros de régimen de mercado
- Reducción de exposición en condiciones extremas

Genera 5 variantes adaptativas.
```

### Simplificación
```
Simplifica este alpha manteniendo el rendimiento:
[alpha code aquí]

Objetivos:
- Reducir complejidad del código
- Eliminar componentes redundantes
- Mantener o mejorar el IC

Genera 5 variantes simplificadas.
```

## Prompts Avanzados

### Estrategia Específica de Mercado
```
Genera un alpha para mercados laterales (ranging markets):
- Detectar cuando el precio está en rango
- Identificar niveles de soporte/resistencia
- Señal de compra cerca de soporte, venta cerca de resistencia

Máximo 20 líneas, incluye lógica de detección de rango.
```

### Estrategia de Eventos
```
Crea un alpha que responda a eventos de mercado:
- Detectar gaps de precio significativos
- Evaluar probabilidad de cierre del gap
- Generar señal basada en dirección esperada del cierre

Máximo 22 líneas.
```

## Mejores Prácticas

### Estructura Recomendada

1. **Objetivo Claro**: Primera línea define qué busca el alpha
2. **Componentes**: Lista los indicadores o factores a usar
3. **Restricciones**: Límites de complejidad y líneas de código
4. **Contexto Opcional**: Condiciones de mercado específicas

### Ejemplo de Estructura Ideal

```
[OBJETIVO] Genera un alpha que [descripción del objetivo]

[COMPONENTES] Usa los siguientes elementos:
- Indicador 1: [descripción]
- Indicador 2: [descripción]
- Filtro: [descripción]

[RESTRICCIONES] 
- Máximo X líneas de código
- Código simple y legible
- Incluye comentarios explicativos

[CONTEXTO OPCIONAL] Considera [condiciones específicas]
```

## Errores a Evitar

### ❌ Prompt Malo
```
Haz un alpha que gane dinero. Que sea bueno.
```

**Problemas:**
- Demasiado vago
- Sin restricciones
- Expectativa irreal

### ✅ Prompt Mejorado
```
Genera un alpha de reversión que identifique oportunidades después de 
movimientos extremos usando RSI. El código debe ser simple (máximo 15 líneas) 
y enfocarse en condiciones sobrecompradas/sobrevendidas.
```

**Mejoras:**
- Específico (reversión, RSI)
- Con restricciones (15 líneas)
- Realista (no promete ganancias garantizadas)

## Consejos Adicionales

1. **Iteración**: Empieza simple y evoluciona
2. **Especificidad**: Más específico = mejores resultados
3. **Validación**: Siempre valida resultados manualmente
4. **Documentación**: Pide al LLM que incluya comentarios
5. **Diversidad**: Varía tipos de estrategias en la población inicial

---

**Nota**: Estos ejemplos son guías. Los prompts efectivos dependen del contexto específico y objetivos del usuario.

