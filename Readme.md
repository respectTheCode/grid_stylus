# 960 Grid in Stylus

An implementation of the 960 grid system ported to the stylus language
and based on the work at [960.gs][1] and Chris Eppstein's work porting
960.gs to the [Compass][2] framework.

This project approaches the 960 grid system as a set of styles that should
be semantically mapped into your html by an intermediate stylesheet.

stylus_grid also includes a basic css reset which can also be included
in your project to normalize platform inconsistencies and give you a
solid baseline from which to construct your grid system.  These files
are not interdependent, however.  Take it or leave it.


[1]: http://960.gs
[2]: http://compass-style.org/

### Creating an intermediate semantic map

Your page itself shouldn't have to be cluttered up with grid framework
classing.  Using an intermediate stylesheet to map elements in your
pages into a grid-based layout encourages a clean, semantic html 
structure while providing a separation that can be exploited more
easily when making changes down the road (like switching from a 16
column grid to 12, or vice-versa).

Consider the following standard (:P) page setup.  Notice the elements
classed as "clear" below, these are a vestige of platform normalization
in the original 960.gs codebase.

	<!DOCTYPE html>
	<html>
		<head><title>Example!</title></head>
		<body>
			<div id="primarylayout">
				<h1 id="pageheader">Example!</h1>
				<span class="clear"></span>
				
				<div id="content">Some Content ...</div>
				<div id="sidebar">Sidebar info ...</div>
				<span class="clear"></span>
			</div>
		</body>
	</html>

Below is an example of an intermediate stylesheet that maps these common
elements into a 16 column grid layout:

	@import "grid_stylus/_reset.styl"
	@import "grid_stylus/_grid.styl"

	var_grid_columns 16
	var_grid_gutter 20px
	var_grid_width 960px

	div#primarylayout
		container()
		#pageheader
			grid_(16)
		
	div#content
		grid_(11)
	
	div#sidebar
		grid_(5)
		