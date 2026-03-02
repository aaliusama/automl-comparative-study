# AutoML Comparative Study: Simulated Annealing vs FLAML vs TPOT

A comprehensive benchmarking study comparing three AutoML frameworks on real-world regression datasets using a fair, fixed time-budget approach.

**Tags**: #MachineLearning #AutoML #DataScience #Python #Benchmark #SimulatedAnnealing #XGBoost

## Project Overview

This project implements a custom **Simulated Annealing (SA)** based AutoML system and compares it against industry-standard AutoML frameworks **FLAML** (Fast AutoML) and **TPOT** (Genetic Programming). The comparison focuses on fair algorithm selection, hyperparameter optimization, and performance evaluation across diverse datasets.

### Key Features
- **Custom Simulated Annealing Implementation**: Temperature-based acceptance probability, reheat mechanism, and intelligent neighbor generation
- **Fair Algorithm Comparison**: All methods evaluated on identical algorithm families (Random Forest, Gradient Boosting, XGBoost, KNN, Ridge, ElasticNet)
- **Fixed Time Budget**: 60-minute time allocation per dataset ensures realistic ML pipeline scenarios
- **Comprehensive Analysis**: Feature importance, residual analysis, and performance metrics across methods
- **Production-Ready Code**: Clean, documented, and reproducible workflow

## Datasets

### Airbnb Dataset
- **Size**: 74,111 samples, 71 features (after preprocessing)
- **Target**: Price prediction (continuous)
- **Preprocessing**: Scaling, encoding, feature engineering, target transformation
- **SA Iterations**: 164 unique configurations tested in 60 minutes

### Insurance Dataset
- **Size**: 1,338 samples, 10 features (including interaction term)
- **Target**: Log-transformed insurance charges (continuous)
- **Preprocessing**: Standard scaling, categorical encoding, feature interaction
- **SA Iterations**: 10,150+ unique configurations tested in 60 minutes

## Methodology

### Search Space Configuration
Total configurations evaluated by SA: **46,830**
- Random Forest: 2,880 configurations
- Gradient Boosting: 5,400 configurations
- XGBoost: 38,400 configurations
- Ridge Regression: 56 configurations
- ElasticNet: 70 configurations
- KNN: 24 configurations

### Evaluation Protocol
- **Cross-Validation**: 5-fold for SA and FLAML, 3-fold for TPOT
- **Metrics**: RMSE, MAE, R² Score
- **Time Budget**: 3,600 seconds (60 minutes) per dataset per method
- **Train-Test Split**: 80-20 with stratification

### Algorithm Comparison

| Aspect | SA | FLAML | TPOT |
|--------|----|----|------|
| Algorithm Family | Tree-based, Linear | Tree-based, Linear | Tree-based, Linear |
| Hyperparameter Tuning | Simulated Annealing | Cost-Frugal Optimization | Evolutionary Algorithms |
| Time Budget Allocation | Adaptive with Reheat | Intelligent Resource Allocation | Fixed per Pipeline |
| Configuration Space | 46,830 | Flexible | 1,000+ pipelines |
| Strengths | Exploration, Large Spaces | Speed, Early Stopping | Pipeline Optimization |

## Results

### Airbnb Performance
- **FLAML**: Best overall (Lower RMSE, higher R²)
- **SA**: Strong second, comprehensive exploration
- **TPOT**: Competitive but resource-intensive

### Insurance Performance
- **FLAML**: Optimal configuration discovery
- **SA**: Robust performance on smaller datasets
- **TPOT**: Good generalization

## Files and Structure

```
.
├── AutoML_Project1.ipynb          # Main notebook with full implementation
├── AutoML_Presentation_v2.pptx    # 30-slide presentation with analysis
├── Airbnb_Data.csv                # Airbnb dataset
├── insurance_data.csv             # Insurance dataset
├── results/                       # Saved model results and configurations
│   ├── sa_results.pkl            # SA best models and configurations
│   ├── flaml_results.pkl         # FLAML best models
│   ├── tpot_results.pkl          # TPOT best models
│   ├── Airbnb_predictions.csv    # SA/RS predictions
│   └── Airbnb_flaml_predictions.csv # FLAML predictions
└── plots/                         # Generated visualizations
    ├── eda_airbnb.png            # Exploratory data analysis
    ├── feature_importance_sa.png  # Feature importance from best SA models
    ├── residual_airbnb.png        # Residual analysis (all three methods)
    └── [additional analysis plots]
```

## How to Run

### Requirements
```bash
pip install pandas numpy scikit-learn xgboost flaml tpot matplotlib jupyter
```

### Execute the Analysis
1. **Open the notebook**:
   ```bash
   jupyter notebook AutoML_Project1.ipynb
   ```

2. **Run all cells** in sequence to:
   - Load and preprocess datasets
   - Execute Simulated Annealing search (60 min per dataset)
   - Run FLAML AutoML (60 min per dataset)
   - Execute TPOT pipeline optimization (60 min per dataset)
   - Generate feature importance and residual analysis plots
   - Produce final comparison results

3. **Execution Time**: ~4-5 hours total (60 min × 3 methods × 2 datasets)

### Key Output Files
- Results saved in `results/` folder (pickle format for reproducibility)
- Visualizations generated in `plots/` folder
- Predictions exported as CSV for detailed analysis

## Key Insights

### Why FLAML Outperformed SA and TPOT

1. **Cost-Frugal Optimization**: FLAML uses a greedy approach to evaluate promising configurations first, maximizing performance discovery within the time budget
2. **Early Stopping**: FLAML's multi-fidelity optimization evaluates configurations at different data sizes, efficiently eliminating poor performers
3. **Algorithm Selection**: Smart resource allocation focuses computational budget on high-potential algorithm families
4. **Stability**: Consistent top-10% performance across all experimental runs

### SA Advantages
- Systematic exploration of high-dimensional search spaces
- Reheat mechanism prevents premature convergence
- Good for larger feature spaces (Airbnb: 71 features)
- Reproducible and interpretable process

### TPOT Considerations
- Excels at pipeline composition and feature engineering
- Slower due to genetic algorithm overhead
- Better suited for complex feature relationships
- Resource-intensive on large datasets

## Performance Metrics Summary

### Airbnb Dataset (RMSE Lower is Better)
- FLAML: Best performance
- SA: 2-5% higher RMSE than FLAML
- TPOT: 5-8% higher RMSE than FLAML

### Insurance Dataset (RMSE Lower is Better)
- FLAML: Optimal configuration discovery
- SA: Competitive on smaller feature space
- TPOT: Strong generalization capability

## Technical Implementation Details

### Simulated Annealing Approach
- **Temperature Schedule**: Exponential cooling with reheat triggers
- **Neighborhood Generation**: Random hyperparameter perturbation
- **Acceptance Probability**: Metropolis criterion with temperature scaling
- **Reheat Mechanism**: Prevents local optima stagnation, enables full 60-minute budget usage

### Data Preprocessing Pipeline
- **Missing Value Handling**: Median imputation for numerical features
- **Feature Scaling**: StandardScaler for all numerical features
- **Categorical Encoding**: One-hot encoding for categorical variables
- **Feature Engineering**: Target transformation (log1p for right-skewed targets), interaction terms
- **Train-Test Split**: 80-20 with fixed random state for reproducibility

## Reproducibility

All results are fully reproducible due to:
- Fixed random seeds (random_state=42)
- Saved model configurations in pickle format
- Detailed preprocessing documentation
- Cross-validation fold specifications
- Time budget tracking in results files

## Visualization Highlights

The `plots/` folder contains:
- **EDA Plots**: Data distributions, correlations, outlier analysis
- **Convergence Plots**: SA temperature schedule and solution quality over time
- **Model Comparisons**: Predicted vs. actual values for all three methods
- **Feature Importance**: Top contributing features from best SA models
- **Residual Analysis**: Distribution and patterns of prediction errors

## Future Work

Potential extensions and improvements:
- Ensemble methods combining SA, FLAML, and TPOT predictions
- Bayesian optimization with Gaussian Processes
- Neural Architecture Search integration
- Distributed computing for parallel configuration evaluation
- Transfer learning from similar datasets

## Getting Started

### Quick Start
```bash
# Clone the repository
git clone <repository-url>
cd automl-comparative-study

# Install dependencies
pip install -r requirements.txt

# Run the analysis
jupyter notebook AutoML_Project1.ipynb
```

### System Requirements
- Python 3.8+
- 4GB RAM minimum (8GB recommended)
- ~4-5 hours for full benchmark execution

## References

- Bergstra, J., & Bengio, Y. (2012). Random Search for Hyper-Parameter Optimization
- Wang, Z., et al. (2021). FLAML: A Fast and Lightweight AutoML Library
- Le, T. T., et al. (2020). A Fast, Scalable and Accurate Genetic Programming based Automated Machine Learning Approach (TPOT)
- Kirkpatrick, S., et al. (1983). Optimization by Simulated Annealing

---

**Project Status**: ✓ Complete | Production-Ready | Fully Reproducible
