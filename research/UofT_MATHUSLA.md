---
layout: single
title: University of Toronto MATHUSLA (Summer 2022)
header:
    overlay_image: /assets/images/ridge.jpg
classes: wide
---

--------------------------------

# Specific Skills Used 

Programming (C++, python), Circuit Design, Microcontroller Programming, CAD, 3-D Printing 

# Summary

In Summer 2022, I continued to work under the supervision of Miriam Diamond (as I had done during the previous summer working for the [**SuperCDMS Collaboration**](https://humerbenjamin.github.io/projects/UofT_CDMS)). The MATHUSLA Lab at UofT was working on materials testing, specifically testing properties of different types of Wavelength Shifting Fibers (WSFs), Plastic Scintillators, and Silicon Photo Multipliers (SiPMs). These are all essential components of the planned MATHUSLA detector, so assessing and eventually selecting the right materials is key for detector performance.

# MATHUSLA Background Information

MATHUSLA is a proposed detector at CERN which 

There is additional background about the MATHUSLA experiment available from [CERN](https://mathusla-experiment.web.cern.ch/).


# My Contribution

At the beginning of the summer, I built a comprehensive testing setup for all of these different components, and then after construction of the setup was finished, I gathered an initial round of test data, and analyzed it to determine general trends as to which materials would be preferred. At the end of the summer, a cosmic ray measurement setup was constructed which validated that the materials configuration would be able to detect cosmic rays on top of acting as a dark matter detector.

### Testing Setup

The setup that I built was primarily for testing WSFs. The important properties that needed to be measured were attenuation and the delay in propogation between the two sides of the fiber to determine the propogation time (since wavelength conversion will make the packet of light arrive in a broader interval than if it were just a beam running through a fiber optic cable).

These measurements utilized a laser shining on a WSF and two SIPMs on either end of the fiber to capture the signal from the light. For attenuation and delay to be accurately measured, the precise location of the light along the fiber needed to be measured, which was what the setup was built for. The setup is shown in the image below.


<div style="text-align: center;">
    <img src="/assets/images/fibre_spool.PNG" style="width: 55%;" alt="mathusla_cosmic">
</div>


The main components of the setup are the large semi-circular spool, and the motor and electronics housing. The motor and electronics housing are on the right, and control the precise location of the fiber down to the nearest $10^{-4}m$ by turning two motors that go in the small cutout on the right of the electronics housing module. There is another similar semi-circular setup on the far side of the dark box that the testing setup was contained within, and the fiber spools between these two semi-circles while the end is slowly fed through the slot on the right of the image by the motors. Connected on the two posts you can see in the image was a housing for the fiber optic cable that aligned it with the WSL.

<div style="text-align: center;">
    <img src="/assets/images/mathusla_setup_picture.jpg" style="width: 70%;" alt="mathusla_cosmic">
</div>

### Cosmic Ray Detector

<div style="text-align: center;">
    <img src="/assets/images/mathusla_cosimic_ray.png" style="width: 80%;" alt="mathusla_cosmic">
</div>