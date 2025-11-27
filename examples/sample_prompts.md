# Examples of Effective Prompts

This guide provides examples of effective prompts for generating alphas with Alpha Evolution Lab.

## Principles of Effective Prompts

### ✅ Characteristics of a Good Prompt

1. **Specific**: Clearly defines the objective and signal type
2. **With Constraints**: Includes complexity and code line limits
3. **With Context**: Mentions market conditions or desired characteristics
4. **Realistic**: Expectations aligned with typical industry metrics

### ❌ Common Errors

1. **Too Vague**: "Make a good alpha"
2. **Without Constraints**: Allows excessively complex code
3. **Unrealistic Expectations**: "IC of 0.10 or more"
4. **Without Context**: Does not mention market conditions

## Examples by Category

### 1. Price Reversal

#### Example 1: Simple Reversal
```
Generate an alpha that identifies reversal opportunities after extreme price movements.
Use RSI or momentum to detect overbought/oversold conditions. The code should be simple,
maximum 15 lines.
```

#### Example 2: Reversal with Volume
```
Create a reversal alpha that combines:
- Extreme price movements (last 2% of range)
- Abnormal volume confirmation (volume > 1.5x average)
- Trend filter (only reversal against trend)

Maximum 20 lines of Python code.
```

### 2. Momentum and Trend

#### Example 3: Trend Following
```
Generate an alpha that identifies bullish trends using:
- Moving average crossover (short term > long term)
- Positive momentum (return > 0 in 5-day window)
- Volatility filter (avoid signals in high volatility)

Maximum 25 lines of code.
```

#### Example 4: Momentum with Confirmation
```
Create a momentum alpha that requires:
- Price above 20-day moving average
- Momentum acceleration (change in rate of change)
- Increasing volume as confirmation

Maximum 20 lines.
```

### 3. Volume and Liquidity

#### Example 5: Volume Anomalies
```
Generate an alpha that detects opportunities based on:
- Abnormally high volume (> 2x 20-day average)
- Accompanying price movement
- Range vs trend context

Simple code, maximum 18 lines.
```

### 4. Volatility

#### Example 6: Volatility Strategy
```
Create an alpha that adapts to different volatility regimes:
- High volatility: reduce exposure
- Low volatility: increase exposure
- Use Bollinger Bands or ATR to measure volatility

Maximum 22 lines of code.
```

### 5. Multi-Factor

#### Example 7: Factor Combination
```
Generate an alpha that combines multiple signals:
- Factor 1: Momentum (5-day return)
- Factor 2: Volume (current/average volume ratio)
- Factor 3: Volatility (normalized ATR)

Final signal = weighted average of the 3 factors.
Maximum 25 lines.
```

## Prompts for Evolution

### Incremental Improvement
```
Improve the following alpha for greater robustness:
[alpha code here]

Focus on:
- Edge case handling
- Additional filters to reduce false positives
- Keep the core logic intact

Generate 5 improved variants.
```

### Adaptation to Conditions
```
Adapt this alpha for different market conditions:
[alpha code here]

Consider:
- Dynamic threshold adjustment according to volatility
- Market regime filters
- Exposure reduction in extreme conditions

Generate 5 adaptive variants.
```

### Simplification
```
Simplify this alpha while maintaining performance:
[alpha code here]

Objectives:
- Reduce code complexity
- Eliminate redundant components
- Maintain or improve IC

Generate 5 simplified variants.
```

## Advanced Prompts

### Market-Specific Strategy
```
Generate an alpha for ranging markets:
- Detect when price is in range
- Identify support/resistance levels
- Buy signal near support, sell signal near resistance

Maximum 20 lines, include range detection logic.
```

### Event Strategy
```
Create an alpha that responds to market events:
- Detect significant price gaps
- Evaluate gap closure probability
- Generate signal based on expected closure direction

Maximum 22 lines.
```

## Best Practices

### Recommended Structure

1. **Clear Objective**: First line defines what the alpha seeks
2. **Components**: Lists indicators or factors to use
3. **Constraints**: Complexity and code line limits
4. **Optional Context**: Specific market conditions

### Example of Ideal Structure

```
[OBJECTIVE] Generate an alpha that [objective description]

[COMPONENTS] Use the following elements:
- Indicator 1: [description]
- Indicator 2: [description]
- Filter: [description]

[CONSTRAINTS] 
- Maximum X lines of code
- Simple and readable code
- Include explanatory comments

[OPTIONAL CONTEXT] Consider [specific conditions]
```

## Errors to Avoid

### ❌ Bad Prompt
```
Make an alpha that makes money. Make it good.
```

**Problems:**
- Too vague
- Without constraints
- Unrealistic expectation

### ✅ Improved Prompt
```
Generate a reversal alpha that identifies opportunities after extreme movements using RSI.
The code should be simple (maximum 15 lines) and focus on overbought/oversold conditions.
```

**Improvements:**
- Specific (reversal, RSI)
- With constraints (15 lines)
- Realistic (does not promise guaranteed profits)

## Additional Tips

1. **Iteration**: Start simple and evolve
2. **Specificity**: More specific = better results
3. **Validation**: Always manually validate results
4. **Documentation**: Ask the LLM to include comments
5. **Diversity**: Vary strategy types in initial population

---

**Note**: These examples are guides. Effective prompts depend on the specific context and user objectives.

