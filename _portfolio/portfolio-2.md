---
title: "Gaia DR3 Visualizations"
excerpt: "Here, I show off some beautiful renders of the Gaia catalog.<br/><img src='/images/GaiaRenders/Export/densitymap.png'>"
collection: portfolio
---

**If you just want to see pictures, scroll down!**

For brevity, I'll only be covering the main points.

The Gaia DR3 source catalog is huge, 700 GB compressed (around 3 TB uncompressed csv files), with 1.8 billion sources. This clearly won't open in most consumer programs (e.g. excel). You can't open this with most programming libraries because the dataset is larger than RAM. In simple terms, your computer has RAM (memory) that is used to store for quick access (e.g. intermediate results of a calculation, keeping a program in RAM so it opens quickly), somewhere from 8 GB to 64 GB probably (unless you're here on a computing cluster). You can't fit the whole 3 TB into that RAM.

I use a programming library called dask that can split up the dataset into small chunks, and only keep the main results. It's designed for data science on huge datasets such as this.

I also use a plotting package called datashader, which natively supports dask and makes it easy to render visualizations of huge datasets. You can't use something like matplotlib because it will probably just crash with 1 billion points. If you try to use alpha values to make the points transparent, you actually run into other issues, which datashader calls over and underplotting. The simple solution for this is to *shade* your data according to the attribute you want.

I am skipping a lot of steps involving how to programatically decompress files, the importance of partitioning your files, the structure of the catalog, etc. You can see these in my jupyter notebook.

**The main takeaway** is that, as long as you have the catalog saved somewhere, and you have a computer or laptop from the last 15 years, that you can make beautiful renders of huge datasets without compromises, in a relatively short amount of time. The Gaia DPAC used some cloud computing and a much larger amount of RAM to render these. For me, it took 2 days to download the dataset (download speeds throttled by Gaia Archive service, nothing you can do), 8 hours to decompress the files, 2 hours for miscellaneous computation (splitting, paritioning, adding, etc). Once we have the exact files to render, it takes only 5 minutes to generate the render. Pretty neat!

So what shall our first plot be? Let's the density map, i.e. plot galactic coordinates shaded by frequency.

**In order to not crash your browser with many high resolution pictures, these are low resolution thumbnails. Click on the picture for full resolution, and explore the detail of these maps!**

<a href="/images/GaiaRenders/Export/densitymap.png" target="_blank">
  <img src="/images/GaiaRenders/LowRes Export/densitymap.png" width="1000" height="500">
</a>

Our image is remarkably similar to the official ESA image releases. For example, see the [Gaia DPAC render](https://sci.esa.int/web/gaia/-/the-density-of-stars-from-gaia-s-early-data-release-3-equirectangular-projection) by A. Moitinho and M. Barros.

Displayed in its full glory is the Milky Way's Central Bulge and the Great Rift.

On the bottom right, we see two large regions of highly dense stars. These are the LMC and SMC. We will look at them later when we do flux maps.

On the bottom left are two bright dots. These are the Andromeda and Triangulum galaxies, respectively. We will also show this later.

All over the galaxy are more bright dots, these are usually globular clusters or other local group galaxies.

For now, let's take a closer look at the center of the galaxy:

<a href="/images/GaiaRenders/Export/Sgr.png" target="_blank">
  <img src="/images/GaiaRenders/LowRes Export/Sgr.png" width="1000" height="500">
</a>

Immediately, we see the thick dust that encircles a significant part of the galactic disk. This dust blocks light from many stars, especially dim ones. As a result, Gaia sees fewer stars in those regions. However, the dust is not completely randomly spread, there is clear structure to the dust. This showcases Gaia's power to map features of dust that were previously not well documented. There are lots of small dots. As you probably guessed, these are globular clusters.

We can also see a strange stripe pattern. This is a result of the incompleteness of Gaia at dim magnitudes. Although we are on DR3 now, Gaia has still not completed its survey of the dimmest stars it can detect. These are in the range of magnitude 20-20.7. There are many of these stars, especially toward the galactic center. Future data releases will reduce this effect.

There are some diagonal overdensities as well. These are more subtle than the stripes but are still visible. They are a result of Gaia's slow rotation that sweeps out a sector of the sky. It could be said that Gaia's primary method of surveying different regions of the sky is waiting for it to rotate into view!

Directly below the center, at the bottom of the image, is a dark dust cloud. That is the Corona-Australis Molecular Cloud and is notable for being mostly isolated.

Just above and to the left of this cloud is a faint overdensity. We can see this in the first density map as well. This is actually the Sagittarius Dwarf Spheroidal Galaxy, which is our nearest confirmed galaxy. It was only discovered in 1994, and for good reason. It's quite faint as it's only made of late type stars. We can even see its central globular cluster, M54. If you are having trouble seeing it at this image's scale, go back to the first image and you should be able to see the dwarf galaxy in the same spot.

Let's go and check out Andromeda:

<a href="/images/GaiaRenders/Export/andromeda.png" target="_blank">
  <img src="/images/GaiaRenders/LowRes Export/andromeda.png" width="500" height="500">
</a>

Andromeda's arms and spiral structure is on full display here. A keen eye will also notice M110 and M32, Andromeda's satellite galaxies.

Finally, let's look at Triangulum, our other neighbor:

<a href="/images/GaiaRenders/Export/triangulum.png" target="_blank">
  <img src="/images/GaiaRenders/LowRes Export/triangulum.png" width="500" height="500">
</a>

Let's make some flux maps, where we color the pixel based on the sum of flux of all the sources there. I have adjusted the scale to produce more contrast. Recall from your stars theory that luminosity is dominated by the brightest stars, and I don't want a super bright star having a single bright pixel, and washing out the detail of the plot for all the other stars.

This also means, we should expect blue objects to have more detail, perhaps some neighbors of ours have this trait?

<a href="/images/GaiaRenders/Export/LMC and SMC.png" target="_blank">
  <img src="/images/GaiaRenders/LowRes Export/LMC and SMC.png" width="1000" height="625">
</a>

The bright spot is 47 Tucanae, which is not near SMC, but just happens to be along the same line of sight.

<a href="/images/GaiaRenders/Export/LMC.png" target="_blank">
  <img src="/images/GaiaRenders/LowRes Export/LMC.png" width="1000" height="750">
</a>

As you know, both the LMC and SMC are dwarf galaxies. However the LMC, unlike its smaller neighbor SMC, has a bar which is clearly observed here. It's the prototype for the Magellanic Galaxy type, which is characterized by having a small size with a single bar. LMC likely was its own dwarf spiral galaxy before the Milky Way started eating it up its arms.


<a href="/images/GaiaRenders/Export/LMC Zoom.png" target="_blank">
  <img src="/images/GaiaRenders/LowRes Export/LMC Zoom.png" width="1000" height="1000">
</a>

The LMC is one of the most active known regions in the night sky. You can see lots of star forming regions here! Let's zoom in one more time.

<a href="/images/GaiaRenders/Export/Tarantula Nebula.png" target="_blank">
  <img src="/images/GaiaRenders/LowRes Export/Tarantula Nebula.png" width="1000" height="1000">
</a>

At this scale you can actually tell the blue stars apart from the red ones (white dots are very bright, so blue).

Of course, flux is not the only attribute you can plot. I showcase a couple more examples. Here I plot the radial velocity map of the Milky Way.

<a href="/images/GaiaRenders/Export/radialvelocitymap.png" target="_blank">
  <img src="/images/GaiaRenders/LowRes Export/radialvelocitymap.png" width="1000" height="500">
</a>

You could derive the Oort constants from this probably, and also see how LMC and SMC are receding from us! Notice some globular clusters are approaching, while others are receding as well.

Finally, a metallicity map.

<a href="/images/GaiaRenders/Export/metallicitymap.png" target="_blank">
  <img src="/images/GaiaRenders/LowRes Export/metallicitymap.png" width="1000" height="500">
</a>

Here you can see the structure of the galaxy, including the thin disk, thick disk, bulge, and halo, with all their different metallicities.