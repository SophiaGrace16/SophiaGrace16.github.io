---
layout: post
title:      "The Magic of CSS Grids"
date:       2021-01-27 14:39:13 -0500
permalink:  the_magic_of_css_grids
---

## Using CSS grids to create an organized layout

CSS grids are a tool that can help you organize your page so that you can get a beautiful layout. One of the trickiest parts of a CSS grid, when working with it for the first time, is knowing where to begin. Let's dive into setting up a basic CSS grid. There are two significant files you need to create your CSS grid - your .css file (App.css, Main.css, etc.) and wherever your HTML is living. 

In this article, we will tackle the CSS because that is where we have to set up our grid. 

```
.**picture**-wrapper{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  width: 100%;
}
```

*Note: Where it says picture you can rebrand that for whatever you want your grid to be named!*

Here is what it would look like rendering in your brower:

![](https://i.imgur.com/sDPOW0a.png)

Looking at that CSS, especially when working with grids for the first time, can be confusing. We will break it down line by line so we can understand what each piece is doing. Again this is the basic of basic grid set ups! At the end I will provide you some resources that can help you build a more complicated grid!

### Display: grid;

Seems simple enough, right? You are saying, "Hey, when you display this, I want you to display it as a grid!" The exact definition of display is:

''Define - Defines the element as a grid container and establishes a new grid formatting context for its contents.''

With display, there are two values you can give it, grid or inline-grid. I will simplify it here using some definitions from W3:

"grid
This value causes an element to generate a grid container box that is block-level when placed in flow layout.
inline-grid
This value causes an element to generate a grid container box that is inline-level when placed in flow layout."

If you are like me and prefer a visual comparison, this codepen.io does a phenomenal job showing the difference!

 https://codepen.io/webmadewell/pen/PRGaVM

### grid-template-columns: 1fr 1fr 1fr;

Grid-template-columns is one of the most important pieces when laying out your grid. You probably have noticed the "fr" unit; this stands for fractions. Not too long ago, most people used percentages - in place of fr units- to allow for a responsive and flexible grid. Fr is now a built-in unit for grids that provides the same responsiveness and flexibility that percentages did.

So how does it work? We use them to decide how many columns our grid will have and the proportions of those grids. In the example above, "1fr 1fr 1fr" means that the grid has three equal-sized columns. You can change the proportions of the columns by upping the number in front of "fr." For example:

![](https://i.imgur.com/RZauxYI.png)

The grid-template-columns here would look something like this: 
grid-template-columns: 1fr 2fr; 

The screen is divided into three portions,  one fraction goes to the first column, and two fractions go into the second column.

### width: 100%;

Width is the width of the grid! I use percentages here so that the grid is responsive to the screen. You do not necessarily need width. I use it when I want my grid to be contained to only a portion of the screen. 

If you would like to continue learning about CSS grids and the different attributes, you can give them below are some articles to continue your learning:

https://webmadewell.com/css-grid-basic-display-grid/

https://css-tricks.com/snippets/css/complete-guide-grid/

https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Basic_Concepts_of_Grid_Layout

https://www.w3.org/TR/css3-grid/#grid-containers

Devtools:

https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Examine_grid_layouts
