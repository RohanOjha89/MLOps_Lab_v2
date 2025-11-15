## Ray vs. Sequential Execution for ElasticNet Hyperparameter Tuning
This repository demonstrates the performance benefits of using Ray (a distributed computing framework) over traditional sequential execution for hyperparameter tuning in machine learning models. Specifically, we focus on tuning the ElasticNet regressor from scikit-learn using a grid search over alpha and l1_ratio parameters.
The lab highlights how Ray can parallelize computationally intensive tasks across a cluster, significantly reducing execution time.

### Overview
- Model: ElasticNet (from sklearn.linear_model)
- Task: Grid search for optimal hyperparameters using cross-validation.
- Hyperparameters:
        alpha_values: [0.0001, 0.001, 0.01, 0.1]
        l1_ratio_values: [0.1, 0.2, 0.3, 0.4, 0.5, 0.75, 0.9]

- Total Combinations: 4 × 7 = 28 hyperparameter pairs
- Dataset: California Housing

We compare:
- Sequential Execution: Single-threaded grid search.
- Ray Distributed: Parallelized using Ray's @ray.remote decorator for hyperparameter evaluations across a cluster.