# DeDe

We are the same as `cvxpy` except we require separate constraints input.

## Hardware requirements
- Linux OS
- a multi-core CPU instance

## Dependencies
- Python 3.8
- Run `pip install -r requirements.txt` to install `cvxpy` and `ray`

## Running DeDe
A toy example for resource allocation with DeDe is as follows.
```
import dede as dd
N, M = 100, 100

# Create allocation variables.
x = dd.Variable((N, M), nonneg=True)

# Create the constraints.
resource_constrs = [x[i,:].sum() == 1 for i in range(N)]
demand_constrs = [x[:,j].sum() == 1 for j in range(M)]

# Create an objective.
obj = dd.Minimize(x.sum())

# Construct the problem.
prob = dd.Problem(obj, resource_constrs, demand_constrs)

# Solve the problem with DeDe on a 64-core CPU.
print(prob.solve(num_cpus=64))

# Solve the problem with cvxpy
print(prob.solve(enable_dede=False))
```
