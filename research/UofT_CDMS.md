---
layout: single
title: University of Toronto SuperCDMS (Summer 2021)
header:
    overlay_image: /assets/images/ridge.jpg
classes: wide
---

--------------------------------

# Specific Skills Used 

Programming (C, C++, python), High Performance Computing, Data Analysis, Software Testing

# Summary

In Summer 2021, I recieved an Engineering Science Research Opportunity (ESROP) grant to work on software testing for the Super Cryogenic Dark Matter Search (SuperCDMS) Collaboration at UofT under the Supervision of Professor Miriam Diamond. Throughout the summer, I attended conferences and seminars to gain understanding of the current state of experiments across different areas of High Energy Particle Physics. Once I understood the field better, I was able to properly understand the objectives of the experiment, and worked on various testing objectives, which culminated in work towards a continuous integration testing system for the Gitlab repository where the analysis packages were hosted.

# Background about SuperCDMS

SuperCDMS is a dark matter detection experiment that uses extremely low temperature (15mK) silicon and germanium crystals. When a dark matter particle hits the crystals it imparts a small amount of energy within the crystal which can then be measured. This allows for extremely small interactions to be measured by the thousands of sensors attached to each crystal.

There is additional background about the SuperCDMS experiment available from both [SNOLab](https://www.snolab.ca/experiment/supercdms/) and [SLAC](https://supercdms.slac.stanford.edu/).

# My Contribution

I worked with the [CDMSBats](https://www.slac.stanford.edu/exp/cdms/software/releasedocs/latest/cdmsbats/CDMSBatsDocumentation/Overview/) packages within the SuperCDMS collaboration. CDMSBats is a set of rawdata processing packages that are used in the early stages of analysis to generate useful experimental data. Raw pulses from the detector modules are filtered and analyzed by a number of different programs. I built the framework for Continuous Integration (CI) testing within the [GitLab CI/CD framework](https://docs.gitlab.com/topics/build_your_application/), and set it up within the CDMSBats pipeline as well as exploring a variety of data errors manually.