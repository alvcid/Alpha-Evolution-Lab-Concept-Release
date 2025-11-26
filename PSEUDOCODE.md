# Pseudocódigo del Sistema

Este documento contiene pseudocódigo explicativo del sistema. **NO contiene código real del proyecto**, solo representaciones conceptuales para fines de documentación.

## Proceso Principal de Evolución

```
FUNCTION main_evolution_loop(initial_prompt, max_generations, population_size):
    // Inicialización
    population = []
    generation = 0
    
    // Generar población inicial
    population = generate_initial_population(initial_prompt, population_size)
    
    // Bucle de evolución
    WHILE generation < max_generations:
        // Evaluar todos los alphas en la población actual
        FOR EACH alpha IN population:
            IF alpha.status == 'pending':
                result = evaluate_alpha(alpha.code, training_data, validation_data)
                alpha.score = result.in_sample_ic
                alpha.validation_score = result.out_of_sample_ic
                alpha.status = 'scored'
        
        // Detectar problemas
        IF detect_overfitting(population):
            LOG_WARNING("Overfitting detected, stopping evolution")
            BREAK
        
        IF detect_convergence(population):
            LOG_INFO("Convergence reached")
            BREAK
        
        // Selección de padres
        candidates = filter_valid_alphas(population)
        elite_alphas = select_top_n(candidates, n=3)
        random_alpha = select_random(candidates, exclude=elite_alphas)
        parents = [elite_alphas, random_alpha]
        
        // Generar nueva generación mediante mutación
        new_alphas = []
        FOR EACH parent IN parents:
            mutations = mutate_alpha(parent, mutation_strategy)
            new_alphas.extend(mutations)
        
        // Actualizar población
        population = merge_populations(population, new_alphas)
        population = keep_top_k(population, k=population_size)
        
        generation = generation + 1
        LOG_PROGRESS(generation, population)
    
    // Retornar mejores alphas
    best_alphas = select_top_n(population, n=10)
    RETURN best_alphas
END FUNCTION
```

## Generación de Población Inicial

```
FUNCTION generate_initial_population(prompt, size):
    // Construir prompt completo con contexto
    full_prompt = build_generation_prompt(prompt, size)
    
    // Solicitar generación al LLM
    llm_response = call_llm_service(full_prompt)
    
    // Parsear respuesta
    alpha_codes = parse_llm_response(llm_response)
    
    // Crear objetos Alpha
    population = []
    FOR EACH code IN alpha_codes:
        alpha = create_alpha_object(
            code: code,
            generation: 0,
            status: 'pending',
            score: null
        )
        population.append(alpha)
    
    RETURN population
END FUNCTION
```

## Evaluación de Alpha

```
FUNCTION evaluate_alpha(alpha_code, training_data, validation_data):
    // Validar código
    IF NOT validate_code_syntax(alpha_code):
        RETURN error_result("Invalid syntax")
    
    // Ejecutar alpha en datos de entrenamiento
    training_signals = execute_alpha_safely(alpha_code, training_data)
    training_returns = calculate_forward_returns(training_data)
    
    // Calcular IC in-sample
    in_sample_ic = calculate_ic(training_signals, training_returns)
    
    // Ejecutar alpha en datos de validación
    validation_signals = execute_alpha_safely(alpha_code, validation_data)
    validation_returns = calculate_forward_returns(validation_data)
    
    // Calcular IC out-of-sample
    out_of_sample_ic = calculate_ic(validation_signals, validation_returns)
    
    // Calcular métricas adicionales
    metrics = calculate_additional_metrics(
        signals: validation_signals,
        returns: validation_returns
    )
    
    // Detectar anomalías
    IF in_sample_ic > SUSPICIOUS_THRESHOLD:
        LOG_WARNING("Suspiciously high IC, possible data leakage")
    
    IF out_of_sample_ic < in_sample_ic * 0.5:
        LOG_WARNING("High IC decay, possible overfitting")
    
    RETURN {
        in_sample_ic: in_sample_ic,
        out_of_sample_ic: out_of_sample_ic,
        metrics: metrics,
        status: determine_status(in_sample_ic, out_of_sample_ic)
    }
END FUNCTION
```

## Cálculo de Information Coefficient

```
FUNCTION calculate_ic(signals, forward_returns):
    // Validar inputs
    IF length(signals) != length(forward_returns):
        RETURN error("Mismatched lengths")
    
    // Calcular correlación de Spearman (robusta a outliers)
    ic = spearman_correlation(signals, forward_returns)
    
    // Validar resultado
    IF abs(ic) > 0.1:
        LOG_WARNING("Unusually high IC, verify for data leakage")
    
    RETURN ic
END FUNCTION
```

## Mutación de Alpha

```
FUNCTION mutate_alpha(parent_alpha, strategy):
    // Construir prompt de mutación según estrategia
    mutation_prompt = build_mutation_prompt(parent_alpha, strategy)
    
    // Solicitar mutaciones al LLM
    llm_response = call_llm_service(mutation_prompt)
    
    // Parsear múltiples variantes
    mutated_codes = parse_llm_response(llm_response, expected_count=5)
    
    // Crear objetos Alpha mutados
    mutations = []
    FOR EACH code IN mutated_codes:
        mutation = create_alpha_object(
            code: code,
            generation: parent_alpha.generation + 1,
            parent_id: parent_alpha.id,
            status: 'pending'
        )
        mutations.append(mutation)
    
    RETURN mutations
END FUNCTION
```

## Construcción de Prompts

```
FUNCTION build_mutation_prompt(alpha, strategy):
    base_prompt = "Improve the following alpha signal:"
    base_prompt += "\n\n" + alpha.code
    base_prompt += "\n\nCurrent performance: IC = " + alpha.score
    
    IF strategy == ADAPTIVE_VOLATILITY:
        base_prompt += "\n\nAdapt the alpha to be more robust across different volatility regimes."
        base_prompt += "Consider dynamic threshold adjustments and volatility filters."
    
    ELSE IF strategy == MARKET_REGIME:
        base_prompt += "\n\nModify the alpha to detect and adapt to market regime changes."
        base_prompt += "Add regime detection logic."
    
    ELSE IF strategy == VOLUME_FILTER:
        base_prompt += "\n\nAdd volume-based filters to improve signal quality."
        base_prompt += "Consider abnormal volume detection and volume confirmation."
    
    ELSE: // STANDARD
        base_prompt += "\n\nMake incremental improvements while maintaining the core logic."
        base_prompt += "Focus on robustness and edge case handling."
    
    base_prompt += "\n\nReturn 5 improved variants as Python code."
    
    RETURN base_prompt
END FUNCTION
```

## Detección de Overfitting

```
FUNCTION detect_overfitting(population):
    FOR EACH alpha IN population:
        IF alpha.score IS NOT NULL AND alpha.validation_score IS NOT NULL:
            ic_decay = (alpha.score - alpha.validation_score) / alpha.score
            
            IF ic_decay > OVERFITTING_THRESHOLD:
                RETURN true
    
    RETURN false
END FUNCTION
```

## Selección Elitista

```
FUNCTION select_top_n(population, n):
    // Filtrar alphas válidos
    valid_alphas = FILTER population WHERE status == 'scored' AND score IS NOT NULL
    
    // Ordenar por score descendente
    sorted_alphas = SORT valid_alphas BY score DESC
    
    // Retornar top N
    RETURN sorted_alphas[0:n]
END FUNCTION
```

## Ejecución Segura de Código

```
FUNCTION execute_alpha_safely(alpha_code, market_data):
    // Validar sintaxis
    IF NOT validate_python_syntax(alpha_code):
        THROW SyntaxError
    
    // Preparar entorno sandbox
    sandbox = create_sandbox_environment()
    sandbox.set_timeout(MAX_EXECUTION_TIME)
    sandbox.set_memory_limit(MAX_MEMORY)
    
    // Inyectar datos de mercado
    sandbox.set_variable('data', market_data)
    
    // Ejecutar código
    TRY:
        signals = sandbox.execute(alpha_code)
        RETURN signals
    CATCH TimeoutError:
        LOG_ERROR("Execution timeout")
        THROW TimeoutError
    CATCH MemoryError:
        LOG_ERROR("Memory limit exceeded")
        THROW MemoryError
    CATCH Exception AS e:
        LOG_ERROR("Execution error: " + e.message)
        THROW e
    FINALLY:
        sandbox.cleanup()
END FUNCTION
```

## Cálculo de Métricas Adicionales

```
FUNCTION calculate_additional_metrics(signals, returns):
    // Calcular retornos de la estrategia
    strategy_returns = signals * returns
    
    // Sharpe Ratio
    sharpe = mean(strategy_returns) / std(strategy_returns) * sqrt(252)
    
    // Sortino Ratio (solo desviación negativa)
    negative_returns = FILTER strategy_returns WHERE value < 0
    sortino = mean(strategy_returns) / std(negative_returns) * sqrt(252)
    
    // Maximum Drawdown
    cumulative = cumprod(1 + strategy_returns)
    running_max = cummax(cumulative)
    drawdown = (cumulative - running_max) / running_max
    max_drawdown = min(drawdown)
    
    // Win Rate
    win_rate = COUNT(strategy_returns > 0) / LENGTH(strategy_returns)
    
    // Profit Factor
    total_gains = SUM(FILTER strategy_returns WHERE value > 0)
    total_losses = ABS(SUM(FILTER strategy_returns WHERE value < 0))
    profit_factor = total_gains / total_losses IF total_losses > 0 ELSE infinity
    
    RETURN {
        sharpe: sharpe,
        sortino: sortino,
        max_drawdown: max_drawdown,
        win_rate: win_rate,
        profit_factor: profit_factor
    }
END FUNCTION
```

## Gestión de Población

```
FUNCTION merge_populations(old_population, new_alphas):
    // Combinar poblaciones
    combined = old_population + new_alphas
    
    // Eliminar duplicados (por código hash)
    unique_alphas = remove_duplicates(combined, key='code_hash')
    
    RETURN unique_alphas
END FUNCTION

FUNCTION keep_top_k(population, k):
    // Ordenar por score
    sorted_pop = SORT population BY score DESC
    
    // Mantener top K
    top_k = sorted_pop[0:k]
    
    // Opcional: mantener algunos aleatorios para diversidad
    remaining = sorted_pop[k:]
    IF LENGTH(remaining) > 0:
        random_sample = SAMPLE(remaining, size=min(2, LENGTH(remaining)))
        top_k.extend(random_sample)
    
    RETURN top_k
END FUNCTION
```

## Constantes y Umbrales

```
CONSTANTS:
    SUSPICIOUS_THRESHOLD = 0.06  // IC sospechosamente alto
    OVERFITTING_THRESHOLD = 0.5  // 50% de decay indica overfitting
    DECENT_IC_THRESHOLD = 0.01   // IC mínimo para considerar "decente"
    EXCELLENT_IC_THRESHOLD = 0.03 // IC para considerar "excelente"
    MAX_EXECUTION_TIME = 30      // segundos
    MAX_MEMORY = 512             // MB
    DEFAULT_POPULATION_SIZE = 10
    DEFAULT_MUTATIONS_PER_PARENT = 5
```

---

**Nota**: Este pseudocódigo es una representación conceptual. La implementación real puede diferir en detalles específicos y optimizaciones.

