# ThermoRoute Q
### Quantum-Assisted Thermal-Aware Scheduling for AI Data Centers

ThermoRoute Q is a software-based simulation project that explores how classical scheduling algorithms and a QAOA-based optimization approach can assign AI workloads to virtual servers while considering estimated thermal conditions, workload distribution, and energy consumption.

**Important:** This project uses simulated server data and a local quantum-circuit simulator. It does not control physical data-center hardware and does not claim quantum advantage.

## Features

- Simulates eight virtual servers with different initial temperatures and processing capacities.
- Generates reproducible workloads using a random seed.
- Compares three classical scheduling strategies:
  - Round Robin
  - Performance-first
  - Thermal-aware
- Implements a QAOA-based job-to-server assignment optimizer using Qiskit and Qiskit Aer.
- Reports estimated peak temperature, energy consumption, makespan, and measured algorithm runtime.
- Displays workload information, scheduling results, and comparison charts in a Streamlit dashboard.
- Includes unit tests for simulation, schedulers, metrics, and the quantum optimizer.

## Technology Stack

- **Language:** Python
- **Dashboard:** Streamlit
- **Charts:** Plotly
- **Quantum circuit and simulation:** Qiskit and Qiskit Aer
- **Numerical computation:** NumPy and SciPy
- **Testing:** Python `unittest`

## Project Structure

```text
ThermoRouteQ/
├── app.py
├── simulation.py
├── schedulers.py
├── quantum_optimizer.py
├── metrics.py
├── test_simulation.py
├── test_schedulers.py
├── test_quantum_optimizer.py
├── test_metrics.py
├── requirements.txt
└── README.md
```

## Setup

Python and a working terminal are required.

Activate the project's existing virtual environment in PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Install dependencies if needed:

```powershell
python -m pip install -r requirements.txt
```

## Run the Dashboard

From the project directory, run:

```powershell
streamlit run app.py
```

Streamlit will provide a local address, usually `http://localhost:8501`, which you can open in a browser.

## Run the Tests

Run the full test suite:

```powershell
python -m unittest -q
```

To compile-check the QAOA optimizer:

```powershell
python -m py_compile quantum_optimizer.py
```

## Scheduling and QAOA

The classical algorithms provide comparison baselines for distributing jobs among virtual servers.

The QAOA optimizer formulates job-to-server assignment as a binary optimization problem and uses Qiskit Aer to simulate a quantum circuit. The current implementation supports at most 16 assignment variables. With eight servers, this permits at most two jobs for QAOA. Classical schedulers can handle larger workloads.

QAOA is a heuristic and may not outperform the classical algorithms. Its local simulator runtime includes the overhead of circuit simulation and optimization.

## Metrics and Limitations

The project reports:

- **Peak simulated temperature:** Highest estimated server temperature.
- **Estimated energy:** Energy calculated by the simulation model.
- **Estimated makespan:** Estimated completion interval based on server workload and processing capacity.
- **Measured runtime:** Wall-clock runtime measured on the computer running the algorithms.

Temperatures, energy, and completion intervals are model estimates, not measurements from real data-center equipment. Results depend on the generated workload, model assumptions, and algorithm settings.

The project is an experimental comparison and does not establish real-world thermal-management performance or quantum advantage.

## Future Improvements

- Evaluate scheduling strategies over multiple random seeds and workload sizes.
- Improve the scalability of the QAOA formulation.
- Add clearer comparisons of thermal, energy, and performance trade-offs.
- Calibrate the simulation model using appropriate real-world data.
