---
layout: single
title: Undergraduate Thesis (2023-2024)
header:
    overlay_image: /assets/images/ridge.jpg
classes: wide
---

--------------------------------

# Links

<a href="/fusion/undergrad_thesis_document.pdf" target="_blank">View Undergraduate Thesis Document</a>

[DSMC Literature Review](/fusion/dsmc_lit_review)

[PIC Literature Review](/fusion/pic_lit_review)

# Specific Skills Used

Physics Simulation, Computational Fluid Dynamics, Individual Particle Simulation, High Performance Computing, and Scientific Communication

# Table of Contents
- [Abstract](#abstract)
- [Introduction](#introduction)
- [Theory](#theory)
    - [DSMC Theory](#dsmc-theory)
    - [PIC Theory](#pic-theory)
- 



# Abstract

This undergraduate thesis investigates the neutral gas distribution over time during the vacuum filling process in General Fusion’s PI-3 plasma injector. Previously, General Fusion had not simulated the dynamics of the PI-3 filling process, so there is an opportunity to further understand the gas distribution at the time of ionization, potentially increasing the total amount of plasma produced by modifying the filling process. This research models the gas distribution within an approximated PI-3 geometry over time using Direct Simulation Monte Carlo methods, and includes a detailed exploration of collisional Particle in Cell codes that could be used to extend this work into a full ionization model. The final simulations of the PI-3 plasma injector showed promising particle density in the Penning trap with some accumulation at the tip of the ionization chamber as well. It also showed that the peak number density was reached after over 300μs despite General Fusion only running their gas puff for 240μs. This should be further explored in the ionization model and other experiments to further optimize plasma formation in the PI-3 plasma injector.


# Introduction

## Project Description and Background

This thesis project involves the use of Direct Simulation Monte Carlo (DSMC) methods to predict non-equilibrium gas filling in a small chamber, and then researching how this simulation could be extended to include ionization as well (see Chapter 2 for more information about General Fusion and their approach to fusion energy Generation). The project and problem definition were provided by General Fusion [1], but will be primarily supervised by Prof. Clinton Groth [2] from the University of Toronto Institute of Aerospace Studies (UTAIS) with assistance from Abetheran Antony who works in Applied Physics at General Fusion. General Fusion’s approach to fusion energy is a hybrid of Inertial and Magnetic Confinement where the plasma is formed in their Fusion Plasma Injector [3] (a form of Plasma Railgun similar to the one proposed by John Marshall [4]) and then fired into a central chamber to undergo fusion. This plasma injection process starts with gas flowing into an evacuated chamber from a number of different valves; then before equilibrium is reached, that gas is ionized with extremely high voltage and compressed using the Fusion Plasma Injector. The beginning stages of this process are what General Fusion is interested in learning more about through the work conducted in this thesis. Currently General Fusion assumes a distribution for the diffusion of gas in the chamber, and then models the ionization and plasma injection from that point, but this can be made more accurate with DSMC simulation of the initial gas diffusion.

## Gap in Existing Research

The proposed research gap is to properly understand the density distribution of neutral gas in the PI-3 Ionization chamber. Up to this point, the assumed distribution of the gases in the chamber was a Gaussian about each valve. General Fusion doesn’t have any existing simulations that they have used to determine the process of filling in the PI-3 ionization chamber, so any insight that can be gained from the DSMC simulations in this thesis will fill that gap in knowledge.

## Central Research Objective

The objective of this thesis work is to provide a more accurate description of the initial gas distribution at the time of ionization, as well as the distribution of ionized gas before compression.
Since it is based on DSMC, this description will incorporate all the relevant particle interactions so
that General Fusion can learn more about where the gas is when ionization occurs in their plasma
injector [5] and where most of the ions are distributed within the chamber before compression.
DSMC should be a great tool for tackling this problem provided the Knudsen Number (see Section
3.1.1) and flow regime (see section 3.1.2) make it computationally viable. This is because DSMC
simulates the fundamental physical interactions and is great for problems like this without known
solutions.

## 


# Theory

As the theory and background are a summarization of existing work, they will live on their own separate pages seperate from this main thesis page. Their links can be found below.

### DSMC Theory

A brief overview of the theoretical background of DSMC and an outline of some available OpenSource DSMC codes is available on the [DSMC Literature Review](/fusion/dsmc_lit_review) page.


### PIC Theory

A brief overview of the theoretical background of PIC and an outline of some available OpenSource PIC codes is available on the [PIC Literature Review](/fusion/pic_lit_review) page.



# Neutral Gas Experimental Approach

## Problem Definition


## Preliminary Calculations and Verification

### Flow Regime for Valve Exit and Unfilled Chamber

### Flow Regime for Chamber after Filling

### Table of Knudsen Numbers


## Approaches

### List of Potential Approaches

### Moment Closure

### Fokker-Planck Solver

### Fokker-Planck and DSMC Hybrid Solver

### Direct Simulation Monte Carlo

### Direct Simulation Monte Carlo Navier Stokes Hybrid Solver


## Test Cases

### Defining Specific Test Cases

### Verification Framework of DSMC Assumptions


## Final Simulation


# Neutral Gas Simulations


# References

