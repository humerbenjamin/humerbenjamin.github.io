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
- [References](#references)


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

Direct Simulation Monte Carlo (DSMC) is a method for simulating molecular dynamics in fluids
of all Knudsen Number regimes, but is largely used for highly rarefied flows [15].

## Key Assumptions of DSMC

The following four assumptions about the physical characteristics of the system are utilized in
DSMC [15].

1. Molecules move without interaction in free flight for the length of the chosen time step [15].
2. Impact parameters and initial orientations of colliding particles are random [15].
3. In every cubic mean free path there are many molecules, but only a small fraction need to be simulated for the molecular description of the flow to be accurate [15].
4. The only molecules that any molecule could collide with are the molecules within a molecule’s finishing cell.

For dilute gases, all four assumptions can be made so they are very accurate with the right parameters. This makes it so the DSMC method produces accurate simulations of macroscopic non- equilibrium flow fields. For dilute gases, there is always a time step which allows assumption 1 to be true regardless of Knudsen Number; Assumption 2 is true provided there is sufficient molecular spacing; assumption 3 is the true foundation of DSMC when compared to Collisional Boltzmann, and can be achieved using a number of different computational methods described later on in this section; and assumption 4 can always be made true with a sufficiently small time step just like assumption 1.

From the four above assumptions, we can understand the basics of a DSMC program (there is a section describing [The DSMC ALgorithm](#the-dsmc-algorithm) in more detail). Just like in other molecular dynamics simulations, the state of the system is determined by a list of properties associated with each individual particle. In DSMC, these properties must include at least the position and velocity ($\vec{x}(t)$ and $\vec{v}(t)$)of each particle at any time step $t$ of the simulation, but additional quantities such as internal rotational energy of the particle ($E_{rot}(t)$) are also quite common to more accurately handle energy and momentum transfer in complex collisions.

## How DSMC Differs From Other Molecular Dynamics Simulations

The way DSMC differs from other molecular dynamics simulations is by not simulating all the particles in a given domain, just a representative sample of the particles, which was alluded to in assumption 3 (from the section on the [Key Assumptions of DSMC](#key-assumptions-of-dsmc)). In any given time step ∆t where $∆t = tf −ti$, the particle moves from its specified position ($\vec{x}(t_i)$) to a final position by following its previous velocity trajectory ($\vec{x}(t_f)=\vec{x}(t_i) + \vec{v} (t_i) · ∆t$). Then based on the path length travelled over the time step ($d =\vec{v}(t_i)· ∆t$), a probability of collision is assigned to each particle, and collisions with other particles within their cells are simulated probabilistically regardless of whether their paths actually crossed. This is because if each cell has a representative set of particles, then a collision with any particle from the representative set at any random angle is the best approximation for modelling all the collisions with the highest degree of computational efficiency.

## Why Do Molecules Need to Stay in Their Cells for Multiple Time Steps

The fourth assumption (from the section on the [Key Assumptions of DSMC](#key-assumptions-of-dsmc)) does not appear in [15], but it is important for the specific case of a transient gas filling simulation, which is the core problem of this thesis. In a gas filling process from an inlet, as gas fills the chamber there will be a bias to the faster end of the velocity distribution (shown in Figure 3).

<div style="text-align: center;">
    <img src="/assets/images/undergraduate_thesis/mb_speed_parametrized.png" style="width:70%;" alt="mb_speed_parametrized">
    <figcaption>Figure 3: Plot of a Maxwell Boltzmann Distribution at $T = 300K$, parameterized on molecular velocity with the high energy section of the distribution highlighted.</figcaption>
</div>

This is d ue to the initial condition of the density, which is a step function where there is a high density area of gas that fills into a near vacuum (a snapshot of the density in a square chamber partway through the filling process is shown in Figure 4). The total flux through the inflow surface is described by 

$$
\Gamma=\frac{1}{4}nc_{gas} \; . \quad (3)
$$

In Equation (3), $n$ is the number density of the gas in $[molecules/m3]$, and $c_{gas}$ is the average velocity of the gas inflow in $[m/s]$. The equation for cgas can be derived from the Boltzmann Distribution, and it is

$$
c_{gas}=\left( \frac{8kT}{m\pi}\right)^\frac{1}{2} \;. \quad (4)
$$

<div style="text-align: center;">
    <img src="/assets/images/undergraduate_thesis/plot6_low-p-slit.png" style="width:70%;" alt="low_p_slit">
    <figcaption>Figure 4: Cube with inflow patch in a slit on the center of the $z = 0$ plane partway through a filling simulation.</figcaption>
</div>

This is important for filling, because the particles at the high velocity end of the Maxwell Boltzmann Distribution naturally form the leading edge of the gas (the leading edge of the gas is very visible in Figure 4 as the lightest part of the flow expanding outwards) from a density step function initial condition, so the gas is not thermalized; and as a result the distribution of energies in each cell will be different. This means the particles must not cross through multiple cells in one time step, otherwise the energy transfer between particles will not be representative of true physical phenomena. If particles pass through multiple cells over the course of one time step, then they do not properly represent the collisional probabilities in the cells they pass through along their path, just the cell they end up in at the end (see Figure 5).

<div style="text-align: center;">
    <img src="/assets/images/undergraduate_thesis/particle_moving_cells.png" style="width:70%;" alt="particle_moving_cells">
    <figcaption>Figure 5: Diagram showing a particle moving from cell A to cell C of a grid in one time step, skipping over cell B.</figcaption>
</div>

In Figure 5, a particle moves along the entirety of $\vec{d}$ in one time step. This is not a problem if properties of cells A, B, and C (such as energy distribution of particles, vector velocities of particles, and the macroscopic number density) are the same, but for a transient problem, adjacent cells will have different properties across the simulation domain. This means if a particle doesn’t spend multiple time steps in each cell, it is not properly accounting for the different collision probabilities and energy transfer parameters from the different cells, leading to incorrect simulation of the underlying physics.


## The DSMC Algorithm

In a DSMC program, the program runs in a loop from initial time ti to final time tf in N time steps of length $∆t$ specified by the equation

$$
\Delta t = \frac{t_f-t_i}{N} \;. \quad (5)
$$

At each time step, the following list of steps occur in the specified order.

1. Generate particles at inflow boundaries (or through imposition of initial conditions at $t = 0$) [15].
2. Move all particles in straight lines along their molecular velocity vectors for a time step less than the local mean collision time [15].
3. Apply Boundary Conditions to particles where it is appropriate (wall collisions and particle deletions) [15].
4. Perform stochastic collisions within each cell, assuming parameters for each collision pair to be random [15].
5. Sample particle properties in each cell [15].

#### Particle Generation

At the beginning of each time step, particles are generated at any inflow patches. They are
randomly assigned parameters, usually based on a modified Maxwell Boltzmann Distribution pa-
rameterized based on Temperature, and often include the ability to manually bias the mean velocity by some $\vec{v}_{bias}$. The Maxwell Boltzmann distribution for 3-dimensional velocity is defined as

$$
f(\vec{v}) \equiv \left[ \frac{2\pi k T}{m} \right]^{-\frac{3}{2}} exp \left( -\frac{1}{2}\frac{m\vec{v}^2}{kT} \right) \; . \quad (6)
$$

The modified distribution mentioned in the previous paragraph takes the velocity $\vec{v}$ from Equation (6) and then adds it to $\vec{v}_{bias}$ to define a particle velocity

$$
\vec{v}_{particle} = \vec{v}+\vec{v}_{bias} \; . \quad (7)
$$

#### Particle Movement

Particles created at the inflow patch were randomly assigned a position⃗x (ti) somewhere on the
face of the inflow patch in the previous step; and particles that were already part of the simulation for the previous time step have positions $\vec{x}(ti)$ which were saved to represent the system state after the previous time step.

At every time step, all particles (both created at the inflow patch and existing in the domain)
are moved by a distance $d$ along $\vec{v}(t_i)$

$$
\vec{d}=\vec{v}(t_i)\cdot \Delta t \;. \quad (8)
$$

This moves each particle to a position $\vec{x}(t_f)$ which is defined by

$$
\vec{x}(t_f)=\vec{x}(t_i)+\vec{v}(t_i)\cdot \Delta t = \vec{x}(t_i) + \vec{d} \; . \quad (9)
$$

After this movement of particles, the set of positions $\vec{x}(tf)$ of the particles forms the positions $\vec{x}(ti)$ of the next time step. This means the position state of the system has been fully specified at this point.

#### Boundary Conditions

Now that particles have been moved to their final positions, boundary conditions need to be
imposed on the particles that have left the domain. The main two boundary conditions that will be used throughout this thesis are wall boundary conditions and deletion boundary conditions. Particles that have left the domain and would have collided with the wall are brought back to the point of contact, and then collide with the wall in whichever way is specified by the boundary (see [16] for some examples). If a particle that has left the domain would have collided with a deletion patch, then the particle is removed from the state of the simulation so it is not a part of the simulation at the beginning of the next time step. Now only the particles that are actually entering the next time step of the simulation remain as a part of the saved state.

#### Stochastic Collisions







# Existing Open Source DSMC Packages

## Graeme Bird

## OpenFOAM

## hyStrath

## SPARTA

## Starfish


# Comparison of Existing Open Source DSMC Codes


# References