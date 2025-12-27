# Staged Sweeps Design

These are the sweeps for model training that I ran over the course of this contract. Each sweep contains a set of base parameters that were held constant, and a set of sweep parameters that were varied via a factorial sweep. These were defined in a spec file, which then generated a config file that defines a single experiment for each factor in the sweep. Each experiment was then run from model training, inference, and evaluation.
