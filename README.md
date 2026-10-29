# Workload-Aware Cloud Storage Tiering

**Optimizing cloud storage costs and access latency through workload-aware tiering, adaptive policies, and simulation-driven evaluation.**

## Problem

Cloud storage must balance storage cost with data retrieval speed. Keeping every object in a high-performance tier can increase storage expenses, while moving data into cheaper tiers can introduce retrieval charges, migration overhead, and higher access latency. A policy that works under stable access patterns may behave differently when workloads shift.

## What this project does

This project evaluates storage-tiering strategies using a reproducible simulation with synthetic access workloads. It compares four policies—Static-hot, Threshold, Workload-aware, and SLA-aware cost—under stable and shifting workload scenarios. The experiment matrix contains two scenarios, five random seeds, and four policies (40 policy-run combinations).

The evaluation focuses on estimated cost, access latency, migration activity, sensitivity to configuration, and ablation of policy components. The notebook and exported CSV/JSON files are provided so the experiment can be inspected and rerun.

## Repository contents

- `Cloud_Storage_Tiering_Complete_Colab_Project_final_executed.ipynb`: executed Colab notebook containing workload generation, policy implementations, simulation, evaluation, and export steps.
- `results/README_RESULTS.txt`: generated summary notes.
- `results/experiment_config.json`: experiment configuration and assumptions.
- `results/aggregate_summary.csv`: aggregated results.
- `results/baseline_comparison.csv`: baseline comparisons.
- `results/per_run_results.csv`: per-run measurements.
- `results/ablation_results.csv` and `results/ablation_summary.csv`: ablation outputs.
- `results/sensitivity_analysis.csv`: sensitivity-analysis outputs.
- `results/interval_migration_records.csv`: migration records.
- `results/sample_stable_trace.csv` and `results/sample_shift_trace.csv`: representative workload traces.

## How to reproduce

1. Open the notebook in Google Colab.
2. Read the configuration and assumptions before changing parameters.
3. Run the cells in order in a fresh runtime.
4. Inspect the exported files and compare new results with the committed outputs.

Package versions, seeds, and configuration may affect exact reproduction; refer to the notebook's setup and configuration cells.

## What the results mean

The results are evidence about the behavior of the implemented policies under the configured simulation, not proof that any one strategy is universally best. The recorded experiments show trade-offs between the Static-hot baseline and dynamic policies, including retrieval and migration overhead. The ablation results indicate that hysteresis affects migration activity, while the supplied recency ablation does not change the recorded outcomes.

## Limitations and research integrity

- Workloads are synthetic, not production access traces.
- Cost and latency values are illustrative assumptions, not live measurements from AWS, Azure, Google Cloud, or another provider.
- The supplied configuration indicates that the latency constraint is **not enforced as a hard constraint**. Recorded feasibility flags must not be presented as evidence of real-world SLA compliance.
- Results depend on the workload generator, tier assumptions, parameters, and policy implementations.
- Production recommendations require validation using representative traces, provider-specific pricing, measured latency, and explicit enforcement of service-level constraints.

## Future work

Evaluate real or public traces, use verified provider pricing, enforce latency constraints directly in decision-making, quantify uncertainty across broader workloads, and compare against additional cloud-native lifecycle policies.

## License

No license is currently specified. Add an appropriate license before inviting reuse or redistribution.
