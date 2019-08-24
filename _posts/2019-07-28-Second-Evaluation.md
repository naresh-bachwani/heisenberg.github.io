---
layout: post
title: Second Evaluation.
image: /img/first-evaluation/Employee-evaluation.jpg
---
I have successfully passed my second evaluations.During this I completed working on the Projection Visualizer. It is one of the biggest PR that I have worked on. Projection Visualizer is the base class for the upcoming Principal Components Visualizer and Manifold Visualizer. It basically implements the basic underlying common functions of both the visualizer.
All the work related to Projection Visualizer are done [here](https://github.com/DistrictDataLabs/yellowbrick/pull/908).

## Projection Visualizer:

As both of the above techniques, PCA and Manifold, are dimensionality reduction technique, both of the visualizers have a lot of things in common. Also implementing these So, here are the common functionality that I implemented in the Projection Visualizer.

###  Draw Method:

Both the functions draw a scatter plot for reduced features in either two or three dimensions. It is supposed to extend the functionality of three-dimensional plots in Manifold too. A sample plot of the both is provided below.

#### Manifold
![Manifold](/img/second-evaluation/Manifold.png)

#### PCA
![PCA](/img/second-evaluation/PCA.png)


### New Layout

The new layout manually draw legends for discrete target and colorbar for continuous target. The colorbar is drawn on new axes which is created by divider axes. The continuous target calls a function `layout()` to achieve the division of axes. The formal code of this function is provided below:
```python
def layout(self, divider=None):

    if (
        self._target_color_type == TargetType.CONTINUOUS        
        and self.projection == 2
        and self.colorbar
        and self._cax is None
        ):

    if make_axes_locatable is None:
        raise YellowbrickValueError(
             (
                "Colorbar requires matplotlib 2.0.2 or greater "
                "please upgrade matplotlib"
                )
            )
    # Create the new axes for the colorbar
    if divider is None:
        divider = make_axes_locatable(self.ax)

    self._cax = divider.append_axes("right", size="5%", pad=0.3)
    self._cax.set_yticks([])
    self._cax.set_xticks([])
```
The new layout looks like this:
![](/img/second-evaluation/Colrbar.png)
