---
title: "Automated Redshift Fitter"
excerpt: "Here, I demonstrate the basic workflow of an automated redshift fitter that I have developed in Python.<br/><img src='/images/OII.png'>"
collection: portfolio
---

Manual redshift fitting takes a long time and is tedious. That's the main motivation for developing a program that can find redshifts from spectra.

The preliminaries are quite straightforward. You want the input spectrum (wavelength, flux, flux error) and the template spectrum (wavelength, flux, flux error).

For background subtraction, there are two choices. You can perform continuum subtraction, where you fit a curve to the continuum (masking major lines) and subtract that from the spectrum, so that we have the raw flux values for non-continuum flux. You can also perfom continuum normalization, where you fit a curve to the continuum (masking major lines) and divide the spectrum by the continuum, then subtract 1 so that all the values are around 0. Now you have relative flux values, or how many times the continuum flux you have at a particular wavelength. Generally, the second method returns better results, although if, due to flux calibration from PypeIt, the continuum crosses over 0 at a certain wavelength (for example, to the left of say, 5000 angstroms, the continuum is a small negative number, and to the right of 5000 angstroms, the continuum is a small positive number), then when you do continuum normalization, at the zero crossover point, you will be dividing by nearly 0, so your relative flux has crazy high numbers. If this happens, you may want to consider just fitting on the spectrum itself, since this usually only happens with very clean spectra.

To improve our spectra's quality, we can perform inverse-variance weighting. Basically, we weigh high-uncertainty results (noisy areas) very little compared to low-uncertainty results (real emission lines, for example). You can see the effect this has on the following example.

**HOW TO USE THE BOKEH GRAPH WIDGET:** Click and drag to move around. Use your mouse scroll wheel to zoom in and out. **Use the scroll wheel on an axis to zoom in and out only in that direction.** If you get lost, click the "reset" button on the right sidebar of the widget. To hide a plotted line, click that line's entry in the legend.

In this example you can see the effect inverse-variance weighting has on the "fake" peaks and the "real" emission lines. Can you find the \[OII\] Doublet?

<iframe src='/images/weighting.html' frameborder='0' width='1100' height='500'></iframe>

**If the plot is too squashed, use scroll wheel on the axis to zoom out only along that axis!**

Next, it is important to use a [flux conserving algorithm](https://ui.adsabs.harvard.edu/abs/2017arXiv170505165C) to properly interpolate. Why do we need to interpolate? Because the wavelength values of the template are not exactly the same as the wavelength values of the spectrum. Naively, we could use linear interpolation, but that actually doesn't conserve the flux of our spectrum. Such interpolation has very small effects our spectrum, as shown here.

<iframe src='/images/interp.html' frameborder='0' width='1100' height='500'></iframe>

**If the plot is too squashed, use scroll wheel on the axis to zoom out only along that axis!**

Zoom in really deep to see the tiny differences between the weighted spectrum and the two interpolated ones. One would not think it would have such a huge impact, but see below.

<iframe src='/images/correlation.html' frameborder='0' width='1100' height='500'></iframe>

Wow! Especially at high redshifts, using a bad interpolation like linear interpolation has a very detrimental effect. Once we properly interpolate, we can use a cross correlation function, which is relatively straightforward and has been implemented in SciPy. Let's see our fit!

<iframe src='/images/resolved.html' frameborder='0' width='1100' height='500'></iframe>

It's good at finding the \[OII\] doublet, even when it's the only feature in the whole spectrum. Keck DEIMOS was designed to be able to resolve the \[OII\] doublet since it is the last emission line before the redshift desert begins, and there's no easily identifiable emission lines for a large wavelength range. 

How well does this perform for blended lines? Pretty well! Check this out:

<iframe src='/images/blended.html' frameborder='0' width='1100' height='500'></iframe>

Even when the line is "wide", but not clearly distinguishable as a double peak, cross-correlation can figure it out from the width of the peak, any other peaks (if they exist), and the continuum's subtle shape. The last point is quite difficult for a human to do, requiring one to bin and convince themselves they're seeing a pattern. Cross-correlation's power lies in being able to discern these subtle patterns from the noise.

