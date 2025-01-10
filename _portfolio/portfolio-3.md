---
title: "DY Pegasi Analysis"
excerpt: " senior project where I concatenated a light curve for DY Pegasi and found its period and othe properties. <br/><img src='/images/curves.png'>"
collection: portfolio
---

I used the university telescope to observe 3 periods of DY Pegasi, a member of the SX Phoenicis variable star category. This category is a middle-ground between long-period and short-period variables, with periods of around a few hours, and amplitudes of around 0.5 magnitudes.

The first goal was to determine the period of DY Pegasi. Having additional observations of the period increased the accuracy of the result. A variation of the Lomb-Scargle Periodogram was used to find the period, which is implemented in the PIPS package (see write up) in a so-called "Fourier likelihood periodogram". I found the period to be 0.072918 ± 0.000024 days, or 1 hour 45 minutes 0 seconds ± 2 seconds. This is well in agreement with the literature value of 0.07292621 ± 0.00000005 days, or 1 hour 45 minutes 0.825 seconds ± 0.005 seconds.

<img src="/images/DYPegasi.png" alt="CCD photograph, 1 of 600+.">

Another aspect of the project was to ascertain key properties of DY Pegasi by taking observations in both the B and V bands. In the interest of time, in order to accomplish this in one night, I alternated filters every 10 minutes for the full 6 hour observation duration. Then, the 3 periods of DY Pegasi were phase folded on top of each other, and a light curve was fitted using a 5-term Fourier solution.

<img src="/images/curves.png" alt="Phase Folded Light Curves">

From the period, I could use a PL relation to find its intrinsic luminosity. I compare the intrinsic luminosity to the apparent luminosity to find its distance from Earth. A bolometric correction is applied.

Separately, we find the B-V color index curve (taken by simply subtracting the V light curve from the B light curve) to see how its color changes over the course of the period. A temperature curve can be estimated using Ballesteros’s Formula (depends on B-V) to see how its temperature varies with the period.

Finally, with the temperature curve and luminosity curves, we can plot its variation on an HR diagram and plot some isocrones to estimate its mass. Assuming low metallicity of Z=0.002 and rotational velocity of 23.6 km/s (from literature), the HR plot and isochrones indicate it's probably around 1.3-1.4 solar masses, which is close to the literature. I don't provide an uncertainty for this (and neither does the literature).

<img src="/images/iso.png" alt="HR Diagram of DY Pegasi">

<a href="https://astroburke.github.io/files/DY_Pegasi_Writing_Sample.pdf">Click here to see the full write up.</a>