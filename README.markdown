
SEMI-LIQUID-GRID
============

A mixin for [the compass framework](https://github.com/chriseppstein/compass) that lets you mix fixed and variable width elements while still thinking in terms of columns.

Requirements
============

You'll need a good working knowledge of [compass](https://github.com/chriseppstein/compass) for any of what follows to make sense. If you aren't using compass already then, trust me, you should be. Check out the excellent docs at http://compass-style.org/

Usage
=======

Take a look at [example 1](examples/example_1) to see how you can add some semi-liquid goodness to your project (hint: take a look at index.html in a browser to get an idea what semi_liquid_grid actually does).

Basically, you drop _semi_liquid.scss into your partials folder and then import it into your screen.scss file with:

    @import 'partials/semi_liquid';

You'll then be able to call a number of mixins that generate the semi-liquid css for you. See [_three_col.scss](examples/example_1/src/partials/_three_col.scss) to see how these are used in example 1. Usage is very similar to the blueprint or liquid-blueprint mixins that ship with compass.

To create a white, full-width container we would use:

    #my-container {
      @include liquid-container;
      background-color: white;
    }

This creates a container based on default blueprint settings which, as in example 1, you can override (see [_base.scss](examples/example_1/src/partials/_base.scss)). For example 1 we use:

    $blueprint-grid-columns: 24;
    $blueprint-container-size: 950px;
    $blueprint-grid-margin: 10px;

To add a liquid column that spans the full container width we could write:

    #my-header {
      @include liquid-column(24,24,true);
      background-color: #ccc;
    }

The first argument is the number of columns wide we want this element to be, while the second argument is how many columns the parent element has. The last argument is optional (defaults to false) and indicates that this is the last element in a row.

To describe a row with two liquid columns of equal width, we could use:

    #left-col {
      @include liquid-column(12,24);
      background-color: red;
    }
    #right-col {
      @include liquid-column(12,24,true);
      background-color: blue;
    }

We can divide a liquid column into multiple sub-columns like this:

    #parent-col {
      @include liquid-column(12,24);
      #sub-cols {
        #left-sub-col { @include liquid-column(4,12); }
        #right-sub-col { @include liquid-column(8,12,true); }
      }
    }

We can also mixin a standard FIXED 'column' like this:

    #parent-col {
      @include liquid-column(12,24);
      #sub-cols {
        #fixed-sub-col { @include column(4,12); }
        #liquid-sub-col { @include liquid-column(8,12,true,4,left); }
      }
    }
    
Noting that we have to pass two additional parameters to liquid-column when we mix fixed and flexible child columns within a parent element. We have to say how many fixed columns there are next to the liquid-column (4 in this case), and where the fixed columns are relative to the liquid one (left in this case).

The liquid-column mixin covered here is the most useful mixin, but semi-liquid-grid also includes additional mixins equivalent to those in the standard compass blueprint package (append, prepend, border etc.). Check out the source code to see how these work.

Aknowledgements
================
* heavily based upon the original liquid blueprint (docs: http://compass-style.org/reference/blueprint/liquid/)
* the one and only [compass](https://github.com/chriseppstein/compass)
* haml and sass, always a pleasure to work with you guys

Future
================
when I get a chance I'll try and bundle this as a proper compass extension and include the tool I use to generate the pngs in the test grid
