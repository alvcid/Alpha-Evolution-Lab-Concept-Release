# System Pseudocode

This document contains explanatory pseudocode of the system. **It does NOT contain real project code**, only conceptual representations for documentation purposes.

## Main Evolution Process

```
FUNCTION main_evolution_loop(initial_prompt, max_generations, population_size):
    // Initialization
    population = []
    generation = 0
    
    // Generate initial population
    population = generate_initial_population(initial_prompt, population_size)
    
    // Evolution loop
    WHILE generation < max_generations:
        // Evaluate all alphas in current population
        FOR EACH alpha IN population:
            IF alpha.status == 'pending':
                result = evaluate_alpha(alpha.code, training_data, validation_data)
                alpha.score = result.in_sample_ic
                alpha.validation_score = result.out_of_sample_ic
                alpha.status = 'scored'
        
        // Detect problems
        IF detect_overfitting(population):
            LOG_WARNING("Overfitting detected, stopping evolution")
            BREAK
        
        IF detect_convergence(population):
            LOG_INFO("Convergence reached")
            BREAK
        
        // Parent selection
        candidates = filter_valid_alphas(population)
        elite_alphas = select_top_n(candidates, n=3)
        random_alpha = select_random(candidates, exclude=elite_alphas)
        parents = [elite_alphas, random_alpha]
        
        // Generate new generation through mutation
        new_alphas = []
        FOR EACH parent IN parents:
            mutations = mutate_alpha(parent, mutation_strategy)
            new_alphas.extend(mutations)
        
        // Update population
        population = merge_populations(population, new_alphas)
        population = keep_top_k(population, k=population_size)
        
        generation = generation + 1
        LOG_PROGRESS(generation, population)
    
    // Return best alphas
    best_alphas = select_top_n(population, n=10)
    RETURN best_alphas
END FUNCTION
```

## Initial Population Generation

```
FUNCTION generate_initial_population(prompt, size):
    // Build complete prompt with context
    full_prompt = build_generation_prompt(prompt, size)
    
    // Request generation from LLM
    llm_response = call_llm_service(full_prompt)
    
    // Parse response
    alpha_codes = parse_llm_response(llm_response)
    
    // Create Alpha objects
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

## Alpha Evaluation

```
FUNCTION evaluate_alpha(alpha_code, training_data, validation_data):
    // Validate code
    IF NOT validate_code_syntax(alpha_code):
        RETURN error_result("Invalid syntax")
    
    // Execute alpha on training data
    training_signals = execute_alpha_safely(alpha_code, training_data)
    training_returns = calculate_forward_returns(training_data)
    
    // Calculate in-sample IC
    in_sample_ic = calculate_ic(training_signals, training_returns)
    
    // Execute alpha on validation data
    validation_signals = execute_alpha_safely(alpha_code, validation_data)
    validation_returns = calculate_forward_returns(validation_data)
    
    // Calculate out-of-sample IC
    out_of_sample_ic = calculate_ic(validation_signals, validation_returns)
    
    // Calculate additional metrics
    metrics = calculate_additional_metrics(
        signals: validation_signals,
        returns: validation_returns
    )
    
    // Detect anomalies
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

## Information Coefficient Calculation

```
FUNCTION calculate_ic(signals, forward_returns):
    // Validate inputs
    IF length(signals) != length(forward_returns):
        RETURN error("Mismatched lengths")
    
    // Calculate Spearman correlation (robust to outliers)
    ic = spearman_correlation(signals, forward_returns)
    
    // Validate result
    IF abs(ic) > 0.1:
        LOG_WARNING("Unusually high IC, verify for data leakage")
    
    RETURN ic
END FUNCTION
```

## Alpha Mutation

```
FUNCTION mutate_alpha(parent_alpha, strategy):
    // Build mutation prompt according to strategy
    mutation_prompt = build_mutation_prompt(parent_alpha, strategy)
    
    // Request mutations from LLM
    llm_response = call_llm_service(mutation_prompt)
    
    // Parse multiple variants
    mutated_codes = parse_llm_response(llm_response, expected_count=5)
    
    // Create mutated Alpha objects
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

## Prompt Construction

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

## Overfitting Detection

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

## Elitist Selection

```
FUNCTION select_top_n(population, n):
    // Filter valid alphas
    valid_alphas = FILTER population WHERE status == 'scored' AND score IS NOT NULL
    
    // Sort by descending score
    sorted_alphas = SORT valid_alphas BY score DESC
    
    // Return top N
    RETURN sorted_alphas[0:n]
END FUNCTION
```

## Safe Code Execution

```
FUNCTION execute_alpha_safely(alpha_code, market_data):
    // Validate syntax
    IF NOT validate_python_syntax(alpha_code):
        THROW SyntaxError
    
    // Prepare sandbox environment
    sandbox = create_sandbox_environment()
    sandbox.set_timeout(MAX_EXECUTION_TIME)
    sandbox.set_memory_limit(MAX_MEMORY)
    
    // Inject market data
    sandbox.set_variable('data', market_data)
    
    // Execute code
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

## Additional Metrics Calculation

```
FUNCTION calculate_additional_metrics(signals, returns):
    // Calculate strategy returns
    strategy_returns = signals * returns
    
    // Sharpe Ratio
    sharpe = mean(strategy_returns) / std(strategy_returns) * sqrt(252)
    
    // Sortino Ratio (only negative deviation)
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

## Population Management

```
FUNCTION merge_populations(old_population, new_alphas):
    // Combine populations
    combined = old_population + new_alphas
    
    // Remove duplicates (by code hash)
    unique_alphas = remove_duplicates(combined, key='code_hash')
    
    RETURN unique_alphas
END FUNCTION

FUNCTION keep_top_k(population, k):
    // Sort by score
    sorted_pop = SORT population BY score DESC
    
    // Keep top K
    top_k = sorted_pop[0:k]
    
    // Optional: keep some random ones for diversity
    remaining = sorted_pop[k:]
    IF LENGTH(remaining) > 0:
        random_sample = SAMPLE(remaining, size=min(2, LENGTH(remaining)))
        top_k.extend(random_sample)
    
    RETURN top_k
END FUNCTION
```

## Constants and Thresholds

```
CONSTANTS:
    SUSPICIOUS_THRESHOLD = 0.06  // Suspiciously high IC
    OVERFITTING_THRESHOLD = 0.5  // 50% decay indicates overfitting
    DECENT_IC_THRESHOLD = 0.01   // Minimum IC to consider "decent"
    EXCELLENT_IC_THRESHOLD = 0.03 // IC to consider "excellent"
    MAX_EXECUTION_TIME = 30      // seconds
    MAX_MEMORY = 512             // MB
    DEFAULT_POPULATION_SIZE = 10
    DEFAULT_MUTATIONS_PER_PARENT = 5
```

---

**Note**: This pseudocode is a conceptual representation. The actual implementation may differ in specific details and optimizations.

