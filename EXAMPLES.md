# Ejemplos de Uso

## Ejemplo 1: Generación Inicial de Población

### Prompt de Usuario

```
Genera 5 alphas que identifiquen oportunidades de reversión después de 
movimientos extremos de precio, usando indicadores de momentum y volumen.
Cada alpha debe ser simple, con menos de 20 líneas de código.
```

### Proceso

1. El usuario ingresa el prompt en la interfaz
2. El sistema envía el prompt al LLM con contexto adicional
3. El LLM genera código Python para cada alpha
4. Cada alpha se parsea y se crea un objeto Alpha con:
   - Código de la señal
   - Razonamiento explicativo
   - Estado inicial: 'pending'

### Resultado Esperado

```
Alpha 1: Reversión por RSI extremo
- IC In-Sample: 0.023
- IC Out-of-Sample: 0.019
- Status: DECENT

Alpha 2: Reversión por volumen anormal
- IC In-Sample: 0.015
- IC Out-of-Sample: 0.012
- Status: DECENT

...
```

## Ejemplo 2: Evolución de Alpha

### Contexto

Tienes un alpha con IC de 0.025 que quieres mejorar.

### Proceso de Mutación

1. **Selección**: El alpha es seleccionado como elite
2. **Mutación**: Se envía al LLM con prompt de mejora:
   ```
   Mejora este alpha para que sea más robusto en diferentes 
   condiciones de mercado. Mantén la lógica central pero añade 
   filtros de validación.
   ```
3. **Generación**: El LLM produce 5 variantes
4. **Evaluación**: Cada variante se backtestea
5. **Selección**: Se mantienen las mejores variantes

### Resultado Esperado

```
Alpha Original: IC = 0.025
Alpha Mutado 1: IC = 0.028 (mejora)
Alpha Mutado 2: IC = 0.022 (regresión)
Alpha Mutado 3: IC = 0.031 (mejora significativa) ← Seleccionado
```

## Ejemplo 3: Detección de Overfitting

### Escenario

Un alpha muestra:
- IC In-Sample: 0.045
- IC Out-of-Sample: 0.012
- IC Decay: 73%

### Proceso de Detección

```
if (ic_decay > 0.5):
    status = "SUSPICIOUS"
    alert_user("Possible overfitting detected")
    recommend_review()
```

### Acción Recomendada

1. Revisar código del alpha para look-ahead bias
2. Simplificar la lógica
3. Aumentar tamaño de validación
4. Descartar si no se puede corregir

## Ejemplo 4: Auto-Evolución

### Configuración

- Iteraciones: 25
- Población inicial: 10 alphas
- Criterio de guardado: IC >= 0.01 y OOS > IS

### Proceso Automatizado

```
for iteration in range(25):
    1. Seleccionar top 3 + 1 aleatorio
    2. Generar mutaciones (5 por padre = 20 nuevos)
    3. Backtestear todos los nuevos alphas
    4. Guardar alphas que cumplan criterios
    5. Actualizar población (top 10)
    6. Verificar convergencia
```

### Resultado Esperado

```
Iteración 1: 2 alphas guardados
Iteración 5: 1 alpha guardado
Iteración 12: 3 alphas guardados
...
Iteración 25: Total 8 alphas guardados
```

## Ejemplo 5: Estrategia de Mutación Adaptativa

### Contexto de Mercado

- Volatilidad alta detectada
- Estrategia seleccionada: ADAPTIVE_VOLATILITY

### Prompt Generado

```
El siguiente alpha funciona bien en condiciones normales. 
Adapta su lógica para que sea más robusto durante períodos 
de alta volatilidad. Considera:
- Ajuste de umbrales dinámicos
- Filtros de volatilidad
- Reducción de exposición en condiciones extremas
```

### Código Generado (Pseudocódigo)

```
def adaptive_alpha(data):
    base_signal = original_alpha_logic(data)
    volatility = calculate_volatility(data, window=20)
    
    if volatility > threshold_high:
        # Reducir exposición en alta volatilidad
        signal = base_signal * 0.5
    elif volatility < threshold_low:
        # Aumentar exposición en baja volatilidad
        signal = base_signal * 1.2
    else:
        signal = base_signal
    
    return signal
```

## Ejemplo 6: Análisis de Correlación

### Objetivo

Identificar alphas redundantes en la población.

### Proceso

```
1. Calcular correlación entre señales de todos los alphas
2. Identificar pares con correlación > 0.8
3. Comparar métricas de rendimiento
4. Mantener el mejor de cada par correlado
```

### Resultado

```
Alpha A y Alpha B: Correlación = 0.85
- Alpha A: IC = 0.028
- Alpha B: IC = 0.025
→ Mantener Alpha A, descartar Alpha B
```

## Ejemplo 7: Validación de Código

### Código Generado (con error)

```python
def alpha_signal(data):
    # Error: uso de variable no definida
    signal = price_change / volume
    return signal
```

### Proceso de Validación

```
1. Parsear código (syntax check)
2. Detectar variables no definidas
3. Rechazar alpha con error
4. Notificar al usuario
5. Opción de corrección manual
```

### Resultado

```
Status: ERROR
Error: NameError - 'price_change' is not defined
Action: Alpha rechazado, requiere corrección
```

## Mejores Prácticas

### Prompts Efectivos

✅ **Bueno:**
- Específico sobre el objetivo
- Incluye restricciones (líneas de código, complejidad)
- Menciona métricas deseadas

❌ **Malo:**
- Demasiado vago ("haz un alpha bueno")
- Sin restricciones
- Expectativas irreales

### Selección de Alphas

✅ **Bueno:**
- Priorizar estabilidad sobre IC máximo
- Verificar que OOS > IS
- Revisar código manualmente para alphas con IC > 0.06

❌ **Malo:**
- Seleccionar solo por IC in-sample
- Ignorar señales de overfitting
- Confiar ciegamente en métricas

### Gestión de Población

✅ **Bueno:**
- Mantener diversidad (diferentes tipos de señales)
- Limpiar alphas redundantes
- Documentar razonamiento de cada alpha

❌ **Malo:**
- Población homogénea (todos similares)
- No revisar correlaciones
- Sin documentación

