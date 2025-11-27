# Feature List

## Main Features

### 1. Automatic Alpha Generation
- **Description**: Uses language models (LLMs) to generate financial signal code from high-level descriptions
- **Benefit**: Reduces development time from weeks to hours
- **Technology**: Integration with Gemini and OpenAI with automatic fallback

### 2. AI-Guided Evolution
- **Description**: Mutation and selection system that iteratively refines the most promising strategies
- **Benefit**: Continuous improvement of alphas without manual intervention
- **Strategies**: Standard, Adaptive Volatility, Market Regime, Volume Filter

### 3. Rigorous Evaluation
- **Description**: Complete backtesting with industry-standard metrics
- **Metrics**: IC, Sharpe, Sortino, Maximum Drawdown, Win Rate, Profit Factor
- **Validation**: Strict in-sample / out-of-sample separation

### 4. Intuitive Visual Interface
- **Description**: Web dashboard to monitor the evolution process in real-time
- **Components**: 
  - Alpha visualization by generation
  - Performance graphs
  - Aggregated statistics
  - Evolution controls

### 5. Out-of-Sample Validation
- **Description**: Strict separation between training and validation data
- **Benefit**: Prevents overfitting and detects generalization problems
- **Metrics**: IC Decay, Stability Score

### 6. Multiple Mutation Strategies
- **Standard**: Generic incremental improvement
- **Adaptive Volatility**: Adaptation to volatility conditions
- **Market Regime**: Detection and adaptation to regime changes
- **Volume Filter**: Incorporation of volume filters

### 7. Safe Code Execution
- **Description**: Sandboxing via Pyodide to execute generated Python code
- **Security**: Syntax validation, timeouts, resource limits
- **Isolation**: Prevention of file system and network access

### 8. Auto-Evolution
- **Description**: Automated process of multiple evolution iterations
- **Configuration**: Number of iterations, save criteria
- **Result**: Promising alphas automatically saved

### 9. Anomaly Detection
- **Description**: Automatic identification of suspicious or erroneous alphas
- **Detections**: 
  - Look-ahead bias
  - Overfitting (high IC decay)
  - Syntax errors
  - Unrealistic metrics

### 10. Population Management
- **Description**: System to maintain diversity and quality in the alpha population
- **Features**:
  - Elitism (preserve best)
  - Diversity (avoid stagnation)
  - Cleaning of redundant ones

## Technical Features

### Modular Architecture
- Clear separation of responsibilities
- Easy extension and maintenance
- Reusable components

### Multi-Provider LLM
- Support for multiple providers
- Automatic fallback
- Unified abstraction

### Type Safety
- TypeScript in frontend
- Type hints in Python
- Runtime type validation

### Performance
- Result caching
- Optimized processing
- Lazy loading of components

## Security Features

### Sandboxing
- Isolated execution of generated code
- Prevention of system resource access
- Time and memory limits

### Code Validation
- Syntax verification
- Dangerous pattern detection
- Automatic rejection of invalid code

### Error Handling
- Graceful recovery
- Detailed logging
- User notifications

## Future Features (Roadmap)

### Phase 2
- Multiple timeframes
- More data sources
- Alpha combination (ensemble)

### Phase 3
- Hyperparameter optimization
- Advanced regime analysis
- Walk-forward analysis

### Phase 4
- Dedicated backend
- Data persistence
- Real-time monitoring
- REST API

### Phase 5
- Integrated Machine Learning
- Sentiment analysis
- Automated trading
- Alpha marketplace

## Comparison with Alternatives

### Advantages
- ✅ Complete process automation
- ✅ Integration with state-of-the-art LLMs
- ✅ Built-in rigorous validation
- ✅ Intuitive visual interface
- ✅ Extensible and modular

### Current Limitations
- ⚠️ Browser execution (performance limitations)
- ⚠️ No persistence between sessions
- ⚠️ Synchronous processing
- ⚠️ One market at a time

---

**Note**: This list reflects the current state of the project. For planned features, see ROADMAP.md.

