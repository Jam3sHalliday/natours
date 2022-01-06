# Lecture 32.

SASS.

    - current sass architecture is design to handle large multi page website or web app
    - for small project like this, it is a bit too much

**base** is for ...

**abstract**only code that is not gonna output any css (variables, mixins, ...)

**components**one file for each component

**layouts**for global header, footer, ...

<br>

# Lecture 33.

## Responsive Principle
<br>

Fluid layouts

    - allow webpage to adapt to the current viewport width (or even height)
    - use % (or vw / vh) unit instead of px for elements that should adapt to viewport (usually layout)
    - use max-width instead of width

Responsive units

    - use "rem" instead of px for most length
    - to make easy to scale the entire layout down (or up) automatically
    
Flexible images

    - by default, images don't scale automatically as we change the viewport
    - alway use % for image dimensions, together with the max-width property

Media queries

    - to change css styles on certain viewport widths

# New stuffs

    - two face card
    - box-decoration-break for text
    - perspective for card flip transition
    - background-lend-mode blend color image
    - clip-path to draw polygon

    - shape-outside make text flow around shape
    - filter for image

    - custom transition with cubic-bezier(need, 4, params, here), but ~ easing.net or cubic-bezier.com can solve it :D
    - use a <span> and its before + after to create animation nav icon
    - transform-origin: define where the animation start


# Pop-up

    - :target pseudo-class
    - display: table-cell;(use for item of display:table) vertical-align is used for display table cell
    - column-count: define how many column, column-gap: space between column, column-rule: line between column

    - hyphens: auto; need to define languge in html tag <html lang="en">

# Responsive

## Desktop-first
We create for large screen first and use media queriy + max width to responsive

## Mobile-first
Star writing CSS for mobile devices (small screen);

Use media queries to expnd design to a large desktop screen

Forces us to reduce websites and apps to the absolute essentials

### Pros
    - 100% optimised for the mobile experience
    - Reduces websites and apps to the absolute essentials;
    - Results in smaller, faster and more efficient products;
    - Prioritizes content over aesthetic design, which may be desirable

### Cons
    - Desktop version might feel overly empty and simplistic;
    - More difficult and counterintuitive to develop;
    - Less creative freedom, making it more difficult to create distinctive products;
    - Clients are used to see a desktop version of the site as a prototype;
    - Do your users even use the mobile internet? What's the purpose of your website?

## Unit in responsive
We're not gonna use px in @media max-width, because if user change default font-size in the browser, then media queries would not be effected by that 

We use em / rem because in media queries, they are not effected by root font-size setting (html { font-size: 62.5% }), that mean 1em or 1rem in media query always = 16px (browser font-size) and if user change browser font-size, 24px for example ~, 1em/rem = 24px

And in this Natours, we'll use em in media query, because rem will fail in some browser

## Responsive image
    The goal of responsive images is to serve the right image to the right screen size and device, in order to avoid downloading unnecessary large  images on smaller screen

    - Resolution switching: decrease image resolution on smaller screen

    - Density switching: half the iamge resolution on @1x screen (pixel density is the amount of pixels found in an inch or a centimeter)
    
    - Art direction: happen when you don't just want to serve the same image but in smaller resolution, but a whole different image for a different screen size

### HTML
Using ```<picture>``` and ```<source>``` for responsive in HTML

```
    <picture class="footer__logo">
        <source srcset="img/logo-green-small-1x.png 1x, img/logo-green-small-2x.png 2x" media="(max-width: 37.5em)">
        <img srcset="img/logo-green-1x.png 1x, img/logo-green-2x.png 2x" alt="Full logo" class="footer__logo">
    </picture>
```

use ```<picture>``` to specify multiple source for one image, and inside it, we can write a media query just like CSS, with ``` media="(max-width: 37.5em)```, we force the browser use the image srcset (screen-width < 600px), otherwise, browser uses the ```<img ...>``` below => it called **ART DIRECTION**

### CSS
Responsive image with CSS by detecting the screen resolution (using ```min-resolution```), render smaller image on low resolution device

```
    @media (min-resolution: 192dpi) and (min-width: 37.5em),  (min-width: 125em) {
        background-image: linear-gradient(
            to right bottom,
            rgba($color-secondary-light, 0.8),
            rgba($color-secondary-dark, 0.8)),
            url(../img/hero.jpg);
    }
```

### Graceful degradation
Currently `backdrop-filter`` is not working on Chrome, so we can write like this, it worked as well!
```
    @media (min-resolution: 192dpi) and (min-width: 37.5em),
        (-webkit-min-device-pixel-ratio: 2) and (min-width: 37.5em), // safari
        (min-width: 125em) {
        background-image: linear-gradient(
            to right bottom,
            rgba($color-secondary-light, 0.8),
            rgba($color-secondary-dark, 0.8)),
            url(../img/hero.jpg);
    }
```

Different between `backdrop-filter` and `filter` is `filter` apply to the element itself, `backdrop-filter` is just applied to the element behind