
# Variable Boilerplate



A proposal for tighter integration between our Figma design system and Half Helix's [DNA Starter Kit](https://github.com/halfhelix/dna "DNA Starter File").

Frontend Demo: [Variable Boilerplate Preview](https://variable-boilerplate.vercel.app/ "Live Preview")




## Fluid Scaling

Our design system is built on fluid responsiveness. This means we implement dynamically resized elements where possible, as opposed to breakpoints. The current implementation uses fluid values for both **Typography** and **Spacing**.

Because our designs are created at static sizes, this system allows us to input fixed values from designs and interpolate between them based on viewport width. To do this, we first ensure the variables for viewport sizes match the width of the desktop and mobile designs:

```css
  --viewport-desktop: 1440;
  --viewport-mobile: 400;
```
Then, for each of our **Typography** or **Spacing** values, we set the desktop and mobile values. These are used for calculations, so we leave off the `px` units.

```css
  --h2-font-size-desktop-hh: 64;
  --h2-font-size-mobile-hh: 40;
```
These values are then taken into a `calc()` function that determines what size a value should get based on the viewport size. The logic here is that mobile represents our minimum values, while desktop determines the proportion we should scale relative to viewport.

These calculated values can get larger than the desktop values as viewport extends beyond the desktop design viewport, allowing us to fluidly scale to larger screens with minimal tweaking. 


## Colors

Our colors are mostly standardized across all projects. In addition to any brand colors, we have a fixed system of greyscale colors, ranging from **Ink** to **Reverse**:

**`Ink`** - Our darkest color, commonly black. Should be ADA compliant when set against **Reverse** & **Light**.

**`Subdued`** - Lighter than **Ink**, but should be ADA compliant when set against **Reverse**.

**`Neutral`** - A utilitarian color used for borders and other areas where ADA compliance is not a consideration. Commonly grey or a color with medium darkness.

**`Light`** - Darker than **Reverse**, but should be ADA compliant when set against **Ink**.

**`Reverse`** - Our lightest color, commonly white. Should be ADA compliant when set against **Ink** & **Subdued**.

In addition, brand specific colors are added separately and follow the pattern of Primary, Secondary, Tertiary, etc. Color contrast for these is handled on a project-by-project basis.

We also use a set of Utility colors for common UI patterns:

**`Focus`** - Generic color used for various focus states. Commonly a vibrant shade of blue, but can be customized per brand within reason.

**`Danger`** - Used to communicate errors or risky user behavior. Commonly a hue of red.

**`Success`** - Used to communicate successful or complete user behavior. Commonly a hue of green.

**`Overlay`** - A special color used for page overlays (behind modals for example). Should support alpha, so `RGBA()` is commonly used here.

## Typography

To compliment the concepts of Fluid Scaling referenced above, we use units relative to font-size wherever possible.

`Line-height` is set as a percentage. Figma provides this as a base-100 percent (90%) while CSS requires us to convert this to a base-1 percent (0.9).

`Letter-spacing` is currently set using `rems`, but this is an area where further development could be done. To truly get consistent letter-spacing as type scales, we'd likely need to use ems but Figma doesn't give us a good way of getting those values.

`Margin` is set in ems, making them relative to the `font-size`a t it scales fluidly. We remove `margin-top` and only use a bottom margin.

Each font-family is stored in a variable as well, with all type styles referencing one of our "--font-family-XXX" variables. This makes it easier to manage fallback fonts and reduces chance of errors.

## Spacing

We should have roughly the same **Spacing** tokens across all projects, ranging from **2XS-3XL**. These follow the same Fluid Scaling as **Typography**, so we'll pull values from both mobile and desktop designs which are then interpolated based on viewport.

For this system to work as intended, it's important that designers think consistently across desktop & mobile. For example, if an element uses `--space-md` on desktop, it should also use it on mobile though the value will be different. This does require more planning for the designer, but makes the structure much cleaner and more consistent.

## Additional variables

Our Figma design system includes variables for many other attributes such as button height, form field spacing, etc. but not all of these are mirrored in CSS variables to keep things cleaner. This may change over time as we find new ways of bringing these into code, but for now we've included some of the more global utility tokens such as:

· Border Radius sizes

· Icon sizes

· Grid gap

· Page margin