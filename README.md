#bb-grid
=======

##A simple responsive Sass based grid 'thingy' to lay out UI elements

###Why?

bb-grids was borne out of the frustration of sub-pixel rounding (<a href="http://benfra.in/1z3">a blog post with more info on the issue is here</a>) when trying to layout UI elements within a grid or arbitary container.

###Summary of the need...
<a href="http://susy.oddbird.net">Susy</a> is a fantastic grid system but can exhibit additional space (where you don't want it) when multiple items are laid out in a line. This is chiefly a problem in browsers that 'round down' sub-pixels such as Safari (both Desktop and iOS variants).
<a href="http://zengrids.com">Zen grid system</a> largely solves the sub-pixel rounding issue by using container relative positioning. However, it uses padding on either side of grid elements to set the grid 'gutter'. This is problematic when laying out UI elements within containers as you get additional space either side of a row of nestetd elements. This is where bb-grid comes in...

###Definition of what bb-grid actually does
bb-grids takes the benefit of the container relative positioning used in Zen but instead uses padding on a single side of grid elements.

Using bb-grid, items can be laid in a default LTR (left to right) order or RTL (right to left) easily.

##Notes:
- bb-grid will only work with IE8+ (requires box-model: border-box;)
- bb-grid is to be used purely to layout rows of ui elements with a container. It can be used in conjunction with grid systems like Susy, Zen and Salsa but it does not replace them.

##Example usage:
Here is how you would layout 7 UI elements:

````
.bb-sevens {
	$bb-columns: 7;
	$bb-gutter-width: 1%;
	//@include bb-background;
	//$bb-flow: right;
	@include bb-container(1.5%);

	> * {
		&:nth-child(7n+1) {
			@include bb-block(1,alpha);
		}
		@for $i from 2 through 6 {
			&:nth-child(7n+#{$i}) {
				@include bb-block(1, $i);
			}
		}
		&:nth-child(7n+7) {
			@include bb-block(1,omega);
		}
	}
}
````

Let's break that down bit by bit:

````
$bb-columns: 7;
$bb-gutter-width: 1%;
//@include bb-background;
//$bb-flow: right;
````

$bb-columns - the amount of columns you want to lay out
$bb-gutter-width - the amount of space (as a percentage of the grid) to be used as gutter between grid columns
@include bb-background - a mixin you can use to show a background of the grid you are implementing (useful for debugging) - comment out when not needed
$bb-flow - set to 'left' by default - set to 'right' to reverse the flow of the grid items.

Then just use the following mixin to layout any container:

@include bb-block(<amount of columns>, <position);

The amount of columns should be passed as a number - for example, if you have a 10 column grid and you want the element to span 70% you would use '7'.

The position can be either 'alpha' (if it's the first item in a grid), a number or 'omega' (if it's the last item in a grid).

Some examples:

````
.three-columns-wide--first-item {
	@include bb-block(3, alpha);
}
.two-columns-wide--starting-at-third-place {
	@include bb-block(2, 3);
}
.one-column-wide--last-item {
	@include bb-block(1, omega);
}
````

##How to install
Just download and include, or copy and paste the _bb-grid.scss file into your project.

###Dependencies
You will need Sass & Compass to use bb-grids