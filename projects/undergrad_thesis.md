---
layout: single
title: Undergraduate Thesis (2023-2024)
header:
    overlay_image: /assets/images/ridge.jpg
classes: wide
---

--------------------------------

# Specific Skills Used

Physics Simulation, Computational Fluid Dynamics, Individual Particle Simulation, High Performance Computing, and Scientific Communication

# Summary

** Thesis abstract goes here **

# Thesis Topic Information

## Project Description and Background

This thesis project involves the use of Direct Simulation Monte Carlo (DSMC) methods to predict nonequilibrium gas filling and ionization in a small chamber. The project and problem definition were provided by General Fusion [1], but will be primarily supervised by Prof. Clinton Groth [2] from the University of Toronto Institute of Aerospace Studies (UTAIS) with assistance from Abetheran Antony who works in Applied Physics at General Fusion. General Fusion’s approach to fusion energy is a hybrid of Inertial and Magnetic Confinement where the plasma is formed in their Fusion Plasma Injector [3] (a form of Plasma Railgun similar to the one proposed by John Marshall [4]) and then fired into a central chamber to undergo fusion. This plasma injection process starts with gas flowing into an evacuated chamber from a number of different valves; then before equilibrium is reached, that gas is ionized with extremely high voltage and compressed using the Fusion Plasma Injector. The beginning stages of this process are what General Fusion is interested in learning more about through the work conducted in this thesis. Currently General Fusion assumes a distribution for the diffusion of gas in the chamber, and then models the ionization and plasma injection from that point, but this can be made more accurate with DSMC simulation of the initial gas diffusion.

## Objectives and Hypothesis

Up to this point, the assumed distribution of the gases in the chamber was a 2-Dimensional Gaussian about each valve with an arbitrary width and height that the engineers thought made sense for the geometry of the chamber and the timescale of filling. The objective of this thesis work is to provide a more accurate description of this initial state at the time of ionization. Since it is based on DSMC, this description will incorporate all the relevant particle interactions so that General Fusion can learn more about where the gas is when ionization occurs in their plasma injector [5].

## Approach to be Taken

The approach that will be taken to modeling the neutral gas distribution will be DSMC simulation. DSMC simulation is a very accurate and comprehensive modelling tool for neutral gases in non-equilibrium systems (which is what will initially be simulated) [6]. There is currently a literature review underway which explores the different open source DSMC packages which are currently available in order to decide which will make the best tool for our simulations. Then once the neutral gas distribution is simulated, the ionization process will be modelled with an adapted DSMC package, or a hybrid PIC-DSMC simulation package (which will be decided with another literature review later in the thesis process).

## Signifigance of Proposed Research

General Fusion is looking to develop technology that can produce large amounts of carbon free energy with minimal radiative byproducts. More information about the way gas is distributed in the chamber at the time of ionization would allow for more control of the plasma in the injector itself. This should lead to a higher number of fusion events occurring in the plasma, moving General Fusion one step closer to net energy production.

# Thesis Components

## Literature Review

## Software Overview

## Method

## Results

# References

[1] Bringing Fusion Energy To Market. Sept. 2023. url: https://generalfusion.com/.  
[2] Clinton Groth. url: https://arrow.utias.utoronto.ca/~groth/.  
[3] Kelly Epp et al. “Confinement Physics on Plasma Injector 3”. In: APS Division of Plasma Physics Meeting Abstracts. Vol. 2020. APS Meeting Abstracts. Jan. 2020, ZP07.011, ZP07.011.  
[4] John Marshall. “Performance of a Hydromagnetic Plasma Gun”. In: Physics of Fluids 3.1 (Jan. 1960), pp. 134–135. doi: 10.1063/1.1705989.  
[5] G A Bird. “Monte Carlo simulation of gas flows”. In: Annual Review of Fluid Mechanics 10.1 (1978), pp. 11–31. doi: 10.1146/annurev.fl.10.010178.000303.  
[6] I. D. Boyd, D. R. Beattie, and M. A. Cappelli. “Numerical and experimental investigations of lowdensity supersonic jets of hydrogen”. In: Journal of Fluid Mechanics 280 (1994), pp. 41–67. doi: 10.1017/s0022112094002843.  