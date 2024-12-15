---
title: "Automated Redshift Fitter"
excerpt: "Here, I demonstrate the basic workflow of an automated redshift fitter that I have developed in Python.<br/><img src='/images/OII.png'>"
collection: portfolio
---

Manual redshift fitting takes a long time and is tedious. That's the main motivation for developing a program that can find redshifts from spectra.

The preliminaries are quite straightforward. You want the input spectrum (wavelength, flux, flux error) and the template spectrum (wavelength, flux, flux error).

For background subtraction, there are two choices. You can perform continuum subtraction, where you fit a curve to the continuum (masking major lines) and subtract that from the spectrum, so that we have the raw flux values for non-continuum flux. You can also perfom continuum normalization, where you fit a curve to the continuum (masking major lines) and divide the spectrum by the continuum, then subtract 1 so that all the values are around 0. Now you have relative flux values, or how many times the continuum flux you have at a particular wavelength. Generally, the second method returns better results, although if, due to flux calibration from PypeIt, the continuum crosses over 0 at a certain wavelength (for example, to the left of say, 5000 angstroms, the continuum is a small negative number, and to the right of 5000 angstroms, the continuum is a small positive number), then when you do continuum normalization, at the zero crossover point, you will be dividing by nearly 0, so your relative flux has crazy high numbers. If this happens, you may want to consider just fitting on the spectrum itself, since this usually only happens with very clean spectra.

To improve our spectra's quality, we can perform inverse-variance weighting. Basically, we weigh high-uncertainty results (noisy areas) very little compared to low-uncertainty results (real emission lines, for example). You can see the effect this has on the following example.

<iframe src='/images/weighting.html' frameborder='0' width='1300' height='500'></iframe>
