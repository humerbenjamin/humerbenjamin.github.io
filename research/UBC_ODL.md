---
layout: single
title: University of British Columbia Ocean Dynamics Lab (Summer 2023)
header:
    overlay_image: /assets/images/ridge.jpg
classes: wide
---

--------------------------------

# Summary

# Specific Skills Used

Programming (python, matlab, ), Data Analysis, Hardware Testing, Oceanography

# Summary

In summer 2023 I recieved an NSERC USRA grant to work in the University of British Columbia (UBC) Ocean Dynamics Lab (ODL) on the [ODL Drifters Project](https://drifters.eoas.ubc.ca/). This project looks to map the outflow of the Fraser river to determine how long it takes to pass victoria in the Juan de Fuca Strait. This is important because the fresher water from the fraser carries all the dissolved substances such as agricultural nutrients, sewage, and sediment out into the ocean. It is important to know how long this contaminants remain in the Salish Sea before they make it out to the open Pacific Ocean.

# My Contribution

With my limited oceanography experience, my personal contribution over the summer was primarily based in software and general problem solving skills. I worked on integrating a new higher frequency tracker into the backend of the website, so they could be deployed during our hovercraft expeditions with the coast guard. I also extensively tested the hardware of the new higher frequency GPS units to confirm they were consistent enough to be useful for data collection.

### Oceanography

The work done in the ODL revolves around going out onto the ocean to measure water properties and deploy drifters. The deployment of drifters was my primary role throughout the summer, so that was the focus of my personal on water time as well. A line of floating drifters is shown below.

<div style="text-align: center;">
    <img src="/assets/images/drifters_floating.png" style="width: 60%;" alt="drifters_software">
</div>

Along with being responsible for the deployment and retrieval of drifters on these trips, I also helped with taking other oceanographic measurements while we were out on the water. The image below shows me on the front of the hovercraft communicating with the winch operator as we lower a probe down to take temperature, salinity, and debris measurements as a function of depth.

<div style="text-align: center;">
    <img src="/assets/images/hovercraft_me.png" style="width: 60%;" alt="hovercraft_data">
</div>


### Drifter's Website Backend

Since a new tracker from a new service was being integrated, it was no longer compatible with the old backend of the [drifter's website map](https://drifters.eoas.ubc.ca/sites/default/files/maps/SUMMARY/mapSALISH.html). I built a parallel process in the backend that took the new data from the [TRACKI](https://tracki.com/?ref=jccwommy&gad_source=1&gclid=CjwKCAjwzMi_BhACEiwAX4YZULb2_n0TUZEKCh784JDrqIemDywiQGmK3wG9k1UIhvy_2SQoyu8trRoCJ7wQAvD_BwE) drifters and reformatted it so it matched the output of the old [SPOT](https://www.findmespot.com/en-us) drifters. A block diagram of the software I wrote is shown below.

<div style="text-align: center;">
    <img src="/assets/images/drifters_software.png" style="width: 70%;" alt="drifters_software">
</div>


### Tracki Hardware Testing

The reason why the [TRACKI](https://tracki.com/?ref=jccwommy&gad_source=1&gclid=CjwKCAjwzMi_BhACEiwAX4YZULb2_n0TUZEKCh784JDrqIemDywiQGmK3wG9k1UIhvy_2SQoyu8trRoCJ7wQAvD_BwE) GPS units were integrated into the drifters system was to investigate the plume front where the Fraser River mixes with the Salish Sea. This is possible since the drifters with TRACKI units on them provide higher frequency updates about their GPS position which allows us to better resolve the dynamics on the plume front. An image of the hovercraft on the plume front where drifters were deployed is shown below.

<div style="text-align: center;">
    <img src="/assets/images/hovercraft_on_tidal_edge.png" style="width: 70%;" alt="plume_front_hovercraft">
</div>

This new GPS system required extensive testing to validate its effectiveness, and the flaws in the hardware ended up requiring that the data be extensively filtered to remove unwanted data points. This process took up about half of my time throughout the summer; but once the system was working properly, we were able to observe that there were convergence events on the plume front which was a novel observation for this river sea boundary.