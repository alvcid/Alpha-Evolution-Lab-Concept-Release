# Usage Examples

## Example 1: Initial Population Generation

### User Prompt

```
Generate 5 alphas that identify reversal opportunities after extreme price movements,
using momentum and volume indicators. Each alpha should be simple, with less than 20 lines of code.
```

### Process

1. User enters the prompt in the interface
2. System sends the prompt to the LLM with additional context
3. LLM generates Python code for each alpha
4. Each alpha is parsed and an Alpha object is created with:
   - Signal code
   - Explanatory reasoning
   - Initial status: 'pending'

### Expected Result

```
Alpha 1: Reversal by extreme RSI
- IC In-Sample: 0.023
- IC Out-of-Sample: 0.019
- Status: DECENT

Alpha 2: Reversal by abnormal volume
- IC In-Sample: 0.015
- IC Out-of-Sample: 0.012
- Status: DECENT

...
```

## Example 2: Alpha Evolution

### Context

You have an alpha with IC of 0.025 that you want to improve.

### Mutation Process

1. **Selection**: The alpha is selected as elite
2. **Mutation**: Sent to LLM with improvement prompt:
   ```
   Improve this alpha to be more robust in different market conditions.
   Keep the core logic but add validation filters.
   ```
3. **Generation**: LLM produces 5 variants
4. **Evaluation**: Each variant is backtested
5. **Selection**: Best variants are kept

### Expected Result

```
Original Alpha: IC = 0.025
Mutated Alpha 1: IC = 0.028 (improvement)
Mutated Alpha 2: IC = 0.022 (regression)
Mutated Alpha 3: IC = 0.031 (significant improvement) ← Selected
```

## Example 3: Overfitting Detection

### Scenario

An alpha shows:
- IC In-Sample: 0.045
- IC Out-of-Sample: 0.012
- IC Decay: 73%

### Detection Process

```
if (ic_decay > 0.5):
    status = "SUSPICIOUS"
    alert_user("Possible overfitting detected")
    recommend_review()
```

### Recommended Action

1. Review alpha code for look-ahead bias
2. Simplify the logic
3. Increase validation size
4. Discard if cannot be corrected

## Example 4: Auto-Evolution

### Configuration

- Iterations: 25
- Initial population: 10 alphas
- Save criterion: IC >= 0.01 and OOS > IS

### Automated Process

```
for iteration in range(25):
    1. Select top 3 + 1 random
    2. Generate mutations (5 per parent = 20 new)
    3. Backtest all new alphas
    4. Save alphas that meet criteria
    5. Update population (top 10)
    6. Check convergence
```

### Expected Result

```
Iteration 1: 2 alphas saved
Iteration 5: 1 alpha saved
Iteration 12: 3 alphas saved
...
Iteration 25: Total 8 alphas saved
```

## Example 5: Adaptive Mutation Strategy

### Market Context

- High volatility detected
- Selected strategy: ADAPTIVE_VOLATILITY

### Generated Prompt

```
The following alpha works well in normal conditions. Adapt its logic to be more robust
during periods of high volatility. Consider:
- Dynamic threshold adjustments
- Volatility filters
- Exposure reduction in extreme conditions
```

### Generated Code (Pseudocode)

```
def adaptive_alpha(data):
    base_signal = original_alpha_logic(data)
    volatility = calculate_volatility(data, window=20)
    
    if volatility > threshold_high:
        # Reduce exposure in high volatility
        signal = base_signal * 0.5
    elif volatility < threshold_low:
        # Increase exposure in low volatility
        signal = base_signal * 1.2
    else:
        signal = base_signal
    
    return signal
```

## Example 6: Correlation Analysis

### Objective

Identify redundant alphas in the population.

### Process

```
1. Calculate correlation between signals of all alphas
2. Identify pairs with correlation > 0.8
3. Compare performance metrics
4. Keep the best of each correlated pair
```

### Result

```
Alpha A and Alpha B: Correlation = 0.85
- Alpha A: IC = 0.028
- Alpha B: IC = 0.025
→ Keep Alpha A, discard Alpha B
```

## Example 7: Code Validation

### Generated Code (with error)

```python
def alpha_signal(data):
    # Error: use of undefined variable
    signal = price_change / volume
    return signal
```

### Validation Process

```
1. Parse code (syntax check)
2. Detect undefined variables
3. Reject alpha with error
4. Notify user
5. Option for manual correction
```

### Result

```
Status: ERROR
Error: NameError - 'price_change' is not defined
Action: Alpha rejected, requires correction
```

## Best Practices

### Effective Prompts

✅ **Good:**
- Specific about the objective
- Includes constraints (lines of code, complexity)
- Mentions desired metrics

❌ **Bad:**
- Too vague ("make a good alpha")
- Without constraints
- Unrealistic expectations

### Alpha Selection

✅ **Good:**
- Prioritize stability over maximum IC
- Verify that OOS > IS
- Manually review code for alphas with IC > 0.06

❌ **Bad:**
- Select only by in-sample IC
- Ignore overfitting signals
- Blindly trust metrics

### Population Management

✅ **Good:**
- Maintain diversity (different types of signals)
- Clean redundant alphas
- Document reasoning for each alpha

❌ **Bad:**
- Homogeneous population (all similar)
- Don't review correlations
- No documentation

