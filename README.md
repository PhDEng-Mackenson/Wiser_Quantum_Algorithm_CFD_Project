# Project 3: Quantum Algorithm as a PDE Solver for Computational Fluid Dynamics (CFD).

**Team Information:**  
• **Team Member 1:**  
Full Name: Mackenson Polché  
Wiser Program Enrollment ID: gst-RsShCt7jVtKW0Du  
• **Team Member 2:**  
Full Name: Priyanshi Singh  
Wiser Program Enrollment ID: gst-WfQBewrHA2GLsp2  
• **Team Member 3:**  
Full Name: Sudikin Pramanik  
Wiser Program Enrollment ID: gst-rYawgBfBcuTJ2qD  

**Exploration of the Project Solution.**  
This repository contains two principal folders, **VQE_Approach** and **MPO**, which implement two different methodologies for solving the one-dimensional viscous Burgers' equation. The **MPO** folder presents a tensor-network, split-operator solution supported by a classical finite-difference baseline and a set of visualizations. The **VQE_Approach** folder presents a quantum-variational strategy in which a parametrized circuit is optimized to reproduce the Burgers' dynamics and is then compared against the classical reference.  

### **1) VQE_Approach folder — Variational Quantum Method**  
This folder contains all materials associated with the quantum Variational Quantum Eigensolver (VQE) strategy for solving the one-dimensional viscous Burgers' equation. The approach formulates a variational objective consistent with the discretized PDE, chooses a parametrized circuit (ansatz), and uses a classical optimizer to update the circuit parameters over successive time steps. The contents of the folder document the theoretical setup, provide a classical reference for benchmarking, and present visualizations of the VQE solution and its agreement with the baseline. 

**Mathematical_Approach_of_Burger_s_Equation**  
This document presents a resume of our solution, the theoretical framework used in the VQE method. It outlines the governing equation, the initial and boundary conditions, and the mapping from the PDE to a variational cost functional. It also explains the assumptions made for the ansatz and the role of viscosity in the dynamics that the variational model must capture.  

**Notebook-1_CFD.ipynb**  
This notebook implements the quantum variational approach to solve the Burgers' equation. Running this notebook produces the baseline solution and optional diagnostic plots. The baseline is used to validate the VQE results and to quantify accuracy through direct comparisons across the entire time evolution.  

**burgers_evolution.gif**  
This animation depicts the temporal evolution of the velocity field u(x,t) produced by the VQE approach. It shows the steepening of the initial profile, the formation and motion of the shock, and the smoothing effect of viscosity over time. The animation offers an intuitive view of whether the variational model reproduces the expected physical behavior.  

**burgers_2d.png**  
This figure provides a two-dimensional heatmap of u(x,t) with space on one axis and time on the other. It is useful for tracing the shock trajectory and for examining global coherence of the VQE solution over the full simulation window.  

**burgers_3d.png**  
This figure shows a three-dimensional surface of u(x,t), highlighting steep gradients during shock formation. It complements the heatmap by making localized features and amplitude variations easier to inspect.  

**burgers_comparison.png**  
This figure summarizes the agreement between the VQE solution and the classical CFD baseline. It typically overlays profiles at the same time instants or presents an error curve, allowing you to evaluate fidelity, stability, and any systematic discrepancies attributable to the variational ansatz or optimization settings.  

---

### **2) MPO folder — Matrix Product Operator (MPO) approach**  
This folder contains the full implementation and supporting artifacts for solving the one-dimensional viscous Burgers' equation using a Matrix Product Operator (MPO) time-splitting scheme. The method separates the advective and diffusive parts of the PDE, maps the corresponding updates to operator forms, and advances the state in time on a discretized spatial grid. To ensure trustworthy evaluation, the folder also includes a classical finite-difference (CFD) reference and a set of visualizations that document initial/final states, parameter sensitivity, and agreement between methods.  

**mpo.ipynb**  
This notebook is the main entry point for the MPO solution. It sets up the spatial grid and time integrator, constructs the split-operator updates, and implements the MPO evolution. When executed, it produces a numerical solution u(x,t) over the simulation window, saves results to disk, and generates the figures used for comparison. The notebook is designed to be reproducible and parameterized, allowing you to adjust viscosity, time step, and grid resolution.  

**fd_solution.npy**  
This NumPy file stores the CFD baseline solution u(x,t) computed on the same grid as the MPO run. It serves as a reference trajectory for quantitative and visual comparisons. Loading this array avoids re-running the classical solver when only comparisons or plots are needed.  

**mpo_split_solution.npy**  
This NumPy file contains the MPO split-step solution u(x,t) produced by the notebook. Because it shares the grid and time points with the CFD baseline, it can be compared directly to fd_solution.npy to assess accuracy across the entire evolution.  

**burgers_initial_final_split.png**  
This figure presents the initial profile u(x,0) together with the final profile u(x,T) obtained from the MPO evolution. It confirms the expected dynamics of Burgers' flow: steepening of the initial condition, shock formation and motion, and viscous smoothing of the shock front.  

**burgers_time_splitting_comparison.png**  
This figure evaluates the sensitivity of the solution to time-splitting choices (for example, different time steps or Trotter orders). It is intended to guide the selection of stable and accurate integration parameters and to document how numerical error behaves under typical settings.  

**classical_vs_mpo_comparison.png**  
This figure directly compares the CFD reference with the MPO solution—typically by overlaying profiles at selected times and/or by plotting an error curve. It provides a concise visual assessment of fidelity and helps diagnose any systematic discrepancies attributable to discretization, truncation, or splitting choices.  

---

**Additional Files:**  
**Presentation_Deck.pdf**  
This presentation deck outlines the methodology and comparative results from applying our VQE and MPO-based solutions to the Burgers equation.  

**README.md**  
This file provides concise instructions for working with the VQE and MPO materials in this folder. It describes how to set up the environment, how to run the relevant notebooks ,and how to interpret the saved figures when assessing the VQE solution.  

---

Due to limited access to quantum hardware resources, we were unable to run our algorithm experimentally to demonstrate its resilience to noise. We hope to continue this work in the future and aim to perform this crucial validation step using actual quantum hardware.  

We appreciate you taking the time to explore this project. Building and validating both the MPO and VQE solutions for Burgers' equation has been a careful, iterative effort, and we hope the notebooks, saved results, and figures make our approach clear and reproducible.  

To the Review Committee of the WISER Quantum Program 2025: thank you for your time and thoughtful assessment of our work. We hope this project contributes a clear, reproducible benchmark for hybrid quantum–classical methods on nonlinear PDEs and sparks discussion about practical paths from theory to implementation. We welcome any comments on our modeling choices, ansatz design, error analysis, and opportunities for scale-up (e.g., higher-dimensional cases, improved cost functionals, or hardware-aware circuits). Your feedback will directly guide our next step. We are grateful for your consideration and for the opportunity to share this work with the WISER community.
