#bb-grid
=======

##A simple responsive Sass based grid 'thingy' to lay out UI elements

###Why?

bb-grids was borne out of the frustration of sub-pixel rounding (<a href="http://benfra.in/1z3">a blog post with more info on the issue is here</a>) when trying to layout UI elements within a grid or arbitary container.

###Summary of the need...
Susy if a fantastic grid system but can exhibit additional space (where you don't want it) when multiple items are laid out in a line.
Zen grid system largely solves the issue by using container relative positioning but uses padding on either side of grid elements to set the grid 'gutter'. This is problematic when laying out UI elements within containers as you get additional space either side of a row of nestetd elements.

###Definition of what bb-grid actually does
bb-grids takes the benefit of container relative positioning used in Zen but amends the padding issue.
Insted, bb-grid uses padding on a single side of each UI item.
Items can be laid in a default LTR (left to right) order or RTL (right to left) easily.

##Notes:
- this will only work with IE8+ (requires box-model: border-box;)
- This is purely to layout rows of ui elements with a container. It can be used in conjunction with grid systems like Susy, Zen and Salsa but it does not replace them.

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