# System Architecture

## Overview

Alpha Evolution Lab is designed as a modular system with clear separation between evolution logic, evaluation, and presentation. The architecture allows horizontal scalability and extensibility through plugins.

## Main Components

### 1. Frontend Layer (React/TypeScript)

**Responsibilities:**
- User interface for control and visualization
- State management of alphas and generations
- Communication with backend services
- Visualization of metrics and statistics

**Technologies:**
- React 19+ for UI
- TypeScript for type safety
- Vite for build tooling
- Recharts for data visualization

### 2. LLM Service Layer

**Responsibilities:**
- Abstraction of multiple LLM providers (Gemini, OpenAI)
- Automatic fallback management
- Construction of specialized prompts
- Parsing of LLM responses

**Mutation Strategies:**
- Standard: Generic mutation based on incremental improvements
- Adaptive Volatility: Adaptation according to volatility conditions
- Market Regime: Detection and adaptation to regime changes
- Volume Filter: Incorporation of volume filters

### 3. Evolution Engine

**Responsibilities:**
- Lifecycle management of populations
- Implementation of selection algorithms
- Coordination of mutations
- Convergence detection

**Selection Algorithm:**
- Elitism: Top N alphas are preserved
- Diversity: Inclusion of random alphas to avoid stagnation
- Stopping criteria: Convergence, overfitting, iteration limit

### 4. Backtesting Framework

**Responsibilities:**
- Safe execution of generated Python code
- Performance metrics calculation
- Code validation before execution
- Error and timeout handling

**Technologies:**
- Pyodide for Python execution in the browser
- Syntax validation before execution
- Sandboxing for security

### 5. Data Pipeline

**Responsibilities:**
- Loading of historical market data
- Preprocessing and normalization
- Train/validation/test split
- Cache management

**Data Sources:**
- Market APIs (EODHD, etc.)
- Local CSV files
- Standard OHLCV formats

### 6. Metrics Calculator

**Responsibilities:**
- Information Coefficient (IC) calculation
- Risk metrics (Sharpe, Sortino, Drawdown)
- Trading metrics (Win Rate, Profit Factor)
- Metrics validation (anomaly detection)

## Data Flows

### Initial Generation Flow

```
User Prompt → LLM Service → Parse Response → Alpha Objects → UI Display
```

### Evolution Flow

```
Current Population → Selection → LLM Mutation → New Alphas → Evaluation → Population Update
```

### Evaluation Flow

```
Alpha Code → Code Validation → Backtest Execution → Metrics Calculation → Score Assignment
```

## Design Patterns

### Strategy Pattern
- Multiple interchangeable mutation strategies
- Different selection algorithms

### Factory Pattern
- Creation of alphas from LLM responses
- Construction of evaluation models

### Observer Pattern
- Notifications of population changes
- Real-time UI updates

## Security Considerations

### Code Execution
- Sandboxing via Pyodide
- Syntax validation before execution
- Timeouts to prevent infinite loops
- Resource limits (memory, CPU)

### Sensitive Data
- API keys stored in environment variables
- No exposure of market data in logs
- User input sanitization

## Scalability

### Horizontal Scaling
- Stateless services allow multiple instances
- Queue system for asynchronous processing (future)

### Vertical Scaling
- Caching of evaluation results
- Optimization of LLM calls (batching)

## Extensibility

### New LLM Providers
- Common interface for LLM services
- Implementation of adapters for new providers

### New Metrics
- Plugin system for custom metrics
- Metrics logging in database (future)

### New Mutation Strategies
- Interface for custom strategies
- Configuration via JSON files

## Current Limitations

1. **Browser Execution**: Pyodide has performance limitations
2. **In-Memory Data**: No persistence of results between sessions
3. **Synchronous Processing**: Evaluations block the UI
4. **Single Market**: Limited support to one ticker at a time

## Future Improvements

1. **Dedicated Backend**: Migration to server for better performance
2. **Database**: Persistence of alphas and results
3. **Asynchronous Processing**: Queue system for evaluations
4. **Multi-Market**: Support for multiple instruments simultaneously

