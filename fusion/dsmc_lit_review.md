---
layout: single
title: DSMC Literature Review
header:
    overlay_image: /assets/images/ridge.jpg
classes: wide
---

# Table of Contents

- [Fluid Mechanics Background for Neutral Gases](#fluid-mechanics-background-for-neutral-gases)
    - [Knudsen Numer](#knudsen-number)
    - [Classification of Flow Regimes](#classification-of-flow-regimes)
- [Direct Simulation Monte Carlo (DSMC)](#direct-simulation-monte-carlo-dsmc)
    - [Key Assumptions of DSMC](#key-assumptions-of-dsmc)
    - [How DSMC Differs from Other Molecular Dynamics Simulations](#how-dsmc-differs-from-other-molecular-dynamics-simulations)
    - [Why Do Molecules Need to Stay in Their Cells for Multiple Time Steps](#why-do-molecules-need-to-stay-in-their-cells-for-multiple-time-steps)
    - [The DSMC Algorithm](#the-dsmc-algorithm)
- [Existing Open Source DSMC Packages](#existing-open-source-dsmc-packages)
    - [Graeme Bird](#graeme-bird)
    - [OpenFOAM](#openfoam)
    - [hyStrath](#hystrath)
    - [SPARTA](#sparta)
    - [Starfish](#starfish)
- [Comparison of Existing Open Source DSMC Codes](#comparison-of-existing-open-source-dsmc-codes)


# Fluid Mechanics Background for Neutral Gases

Theory and background information is presented for technical readers who are not specialists in fluid mechanics or gas dynamics. Specialists in fluid mechanics or gas dynamics may not need to read this section of this page. It will be referenced in further sections of the page so readers can return to this technical content if required. Those familiar with the intricacies of DSMC may also not need to read the section outlining [DSMC](#direct-simulation-monte-carlo-dsmc).

## Knudsen Number

Many key question associated with this thesis revolve around why DSMC is well suited for
tackling this specific type of gas dynamics problem, and the foundation of this discussion depends on an understanding of flow regimes. The flow regimes covered by present theory are often classified by their Knudsen Number. The Knudsen Number is a dimensionless number defined as the ratio of the molecular mean free path to the representative physical length scale 

$$
Kn=\lambda/L \; . \quad (1)
$$

Where $λ$ is the molecular mean free path (see [10] for a basic definition) in the medium of interest, and $L$ is some representative physical length scale such as the gap length that a gas could travel through before collision with a solid surface. This can intuitively be understood as a metric for how collisional the medium will be by thinking about the edge cases of the values the Knudsen Number can take on, so from Equation (1) we take the following 2 cases.

1. $Kn → ∞$: then the mean free path is infinitely larger than the length scale, and molecular collisions have very little impact on the evolution of the system.

2. $Kn → 0$: then the length scale is infinitely larger than the mean free path, statistical fluctuations disappear since the molecules of the fluid are effectively constantly colliding, and are effectively homogeneous at a small enough length scale.

In case 1, statistical fluctuations will be dominant for a fine resolution hexahedral grid (where $V \approx L^3$ for the grid). This is because within each cell, there will be no collisions, resulting in free diffusion based on the statistical profile of the gas in each cell.

In case 2, the cancellation of statistical fluctuations leads to the functions describing the gas at different points in space being continuous. Consider an example function such as T(⃗r, t) representing the temperature of a fluid at various points in space ⃗r at times t. For an infinitely collisional gas, properties of the gas in two infinitesimally nearby locations are going to be the same, since they will exchange energy and momentum through their frequent collisions. This leads to the equality 

$$
T(\vec{r},t) = \lim_{d\vec{x} \to 0} T(\vec{r} \pm d\vec{x},t) \; . \quad(2)
$$

The difference in modeling these 2 extreme cases comes from these continuous functions seen in case 2. In case 2, the model can be abstracted to these continuous properties and the effects they have on each other; while in case 1 the dynamics of individual molecules or groups of molecules must be modeled for the full physical picture to be understood. These regimes and the different models that apply to them are further discussed in the section about [Flow Regimes](#flow-regimes).

## Classification of Flow Regimes

With the knowledge of Knudsen Number presented in the section about the [Knudsen Numer](#knudsen-number), gas dynamics processes can be classified based on their Knudsen Number. These classifications are separated into four basic categories presented in Figure 1, where the molecular regime, and continuum regime are recognizable from the [Knudsen Numer](#knudsen-number) section where they were labeled cases 1 and 2 respectively.

<div style="text-align: center;">
    <img src="/assets/images/undergraduate_thesis/flow_regimes.png" style="width:80%;" alt="flow_regimes">
    <figcaption>Figure 1: Flow regimes covered by present theory classified based on Knudsen Number [11].</figcaption>
</div>

With an understanding of the 2 extreme cases presented in the section about the [Knudsen Number](#knudsen-number), understanding can be extended into the slip flow and transition regimes shown in Figure 1. In the molecular regime, the intuition formed in case 1 fully applies, and in the continuum regime, the intuition formed in case 2 fully applies. The continuum regime will not be discussed further, but more information is available in the following set of notes [12]. In the slip flow regime, the internal flow can be thought of as the same as in continuum flow, but on the edges there may be different phenomena based on the imposition of boundary conditions on the flow (see Section 4 of [13] for more details about flow boundary layers). In the transition regime, there is a mix of both free path DSMC particles as well as sufficient collisional frequency to preserve continuum like trends in the data, but depending on the Knudsen Number, these statistical fluctuations keep continuum models from being accurate. The different fluid flow models in terms of their flow regimes are described in Figure 2.

<div style="text-align: center;">
    <img src="/assets/images/undergraduate_thesis/comp_methods_regimes.png" style="width:80%;" alt="flow_regimes">
    <figcaption>Figure 2: Continuum mechanics simulation types classified based on the Knudsen Number regimes over which they provide accurate numerical results [14].</figcaption>
</div>

From Figure 2 (see [14] for further detail), we can see that the continuum models for a fluid
flow are valid until the beginning of the transitional flow regime, but after that the end of the Burnett Hydrodynamics Equations, there is no closed set of equations that can describe the flow of a fluid. When considering molecular models however, there is no Knudsen Number range in which they do not provide accurate solutions. This is because they are simulating the fundamental physical interactions that govern macroscopic properties of interest in continuum simulations (see case 2 in the [Knudsen Numer](#knudsen-number) section for an example). This means that for a simulation that begins with part of the domain having a Knudsen Number of $Kn < 0.001$, and another part of the domain having a Knudsen Number of $Kn → ∞$, and a final Knudsen number of $Kn > 0.1$, then modelling the entire domain using a molecular model that accounts for collisions (such as a Boltzmann or DSMC model) is perfectly valid. The flow regimes for the specific gas filling process that General Fusion is interested in are analyzed on the main page relating to this [Undergradaute Thesis](/fusion/undergrad_thesis/#preliminary-calculations-and-verification).



# Direct Simulation Monte Carlo (DSMC)

## Key Assumptions of DSMC

## How DSMC Differs From Other Molecular Dynamics Simulations

## Why Do Molecules Need to Stay in Their Cells for Multiple Time Steps

## The DSMC Algorithm


# Existing Open Source DSMC Packages

## Graeme Bird

## OpenFOAM

## hyStrath

## SPARTA

## Starfish


# Comparison of Existing Open Source DSMC Codes