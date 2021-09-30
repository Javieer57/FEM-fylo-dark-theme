# Frontend Mentor - Fylo dark theme landing page solution

This is a solution to the [Fylo dark theme landing page challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/fylo-dark-theme-landing-page-5ca5f2d21e82137ec91a50fd). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Table of contents

-   [Overview](#overview)
    -   [The challenge](#the-challenge)
    -   [Screenshot](#screenshot)
    -   [Links](#links)
-   [My process](#my-process)
    -   [Built with](#built-with)
    -   [What I learned](#what-i-learned)
    -   [Continued development](#continued-development)
    -   [Useful resources](#useful-resources)
-   [Author](#author)

**Note: Delete this note and update the table of contents based on what sections you keep.**

## Overview

### The challenge

Users should be able to:

-   View the optimal layout for the site depending on their device's screen size
-   See hover states for all interactive elements on the page

### Screenshot

![](./thumb.png)

### Links

-   Solution URL: [https://www.frontendmentor.io/solutions/fylo-landing-page-using-flexbox-and-css-grid-sMHUWtBLe](https://www.frontendmentor.io/solutions/fylo-landing-page-using-flexbox-and-css-grid-sMHUWtBLe)
-   Live Site URL: [https://javieer57.github.io/FEM-fylo-dark-theme/](https://javieer57.github.io/FEM-fylo-dark-theme/)

## My process

### Built with

-   Semantic HTML5 markup
-   CSS custom properties
-   Flexbox
-   CSS Grid
-   SCSS
-   Mobile-first workflow
-   [Feather Icons](https://feathericons.com/)

### What I learned

The project's design had containers with differents widths that I wanted to follow but, it was hard to make everyone responsive. So I make a mixin that can handle that and only need the maximum width I want in the container.

```scss
/**
* This mixin makes responsive a container.
* $size [px] arg1 [maximum width for container]
*/
@mixin containerResponsive($size) {
	// For mobile, add a 25px padding
	padding-left: 25px;
	padding-right: 25px;

	// Remove the padding when the specified width plus 50px is reached. Change the padding to an auto margin.
	@media screen and (min-width: $size + 50px) {
		margin-left: auto;
		margin-right: auto;
		padding-left: 0;
		padding-right: 0;
		max-width: $size;
	}
}
```

I realized that the design works with margin from 5px to 5px up to 40px in their elements (like text or images). So created a little loop with sass to avoid writing every class separately.

```scss
/**
* This loop creates margin classes from 5 to 5 up to 40.
*/
@for $i from 1 through 8 {
	.mb-#{$i * 5} {
		margin-bottom: ($i * 5px);
	}
}
```

To work with texts and titles styles, I added two mixins and only need the font size and the line height for each class.

```scss
@mixin textTemplate($font-size, $line-height: normal) {
	font-family: var(--text-font);
	font-size: $font-size;
	line-height: $line-height;
}

@mixin titleTemplate($font-size, $line-height: normal) {
	font-family: var(--title-font);
	font-size: $font-size;
	line-height: $line-height;
	font-weight: bold;
}

.text {
	&--16 {
		@include textTemplate(rem(16), 24px);
	}
}

.title {
	&--18 {
		@include titleTemplate(rem(18), 24px);
	}
}
```

During this project, I learned more about how to use flexbox and the flex-basis and flex-grow properties. I used them specifically to make the testimonials cards responsive, without any media queries. It was helpful.

```scss
.element {
	flex-grow: 1;
	flex-basis: 280px;
	max-width: 360px;
}
```

In the beginning, I doesn't have consistency in the typography styles and repeated the same styles in different classes. I copied a little of the Bootstrap syntax (-sm-) to have more consistency in the typography styles.

```scss
.text {
	&--16 {
		@include textTemplate(rem(16), 24px);
	}

	@include breakpoint(small) {
		&--sm-16 {
			@include textTemplate(rem(16), 24px);
		}
	}
}
```

Related to the typography styles, I also learned to separate the font styles from others like margin or padding to have more clean styles.

```html
<h1 class="title--18 mb-30">All your files in one secure location, accessible anywhere.</h1>
```

```scss
.title {
	&--18 {
		font-family: var(--title-font);
		font-weight: bold;
		line-height: 36px;
		font-size: rem(24);
	}
}

.mb-30 {
	margin-bottom: rem(30);
}
```

### Continued development

I'll like to improve the styles of the project because it has little details related to the layout that I found a little confused.

I tried to follow the Figma design but it doesn't have a column-based layout, which results in specific styles for every section container. Maybe I'll change that in the future and add general styles for the sections.

### Useful resources

-   [Px to Em Functions](https://css-tricks.com/snippets/sass/px-to-em-functions/) - This function is specifically helpful to have more control over the breakpoints

```scss
$breakpoints: (
	"small": "39.9375em",
	"medium": "63.9375em",
	"large": "87.4375em",
);

@mixin breakpoint($size) {
	@media (min-width: map-get($breakpoints-up, $size)) {
		@content;
	}
}
```

## Author

-   Frontend Mentor - [@Javieer57](https://www.frontendmentor.io/profile/Javieer57)
-   Github - [@Javieer57](https://github.com/Javieer57)
-   Instagram - [@javieer57](https://www.instagram.com/javieer_57/)
