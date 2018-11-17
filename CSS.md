# CSS Questions

Yangshun - 63 questions

1. What is CSS selector specificity and how does it work?



2. What's the difference between "resetting" and "normalizing" CSS? Which would you choose, and why?

Resetting and Normalizing CSS are NOT the same

#### Resetting CSS - removes all default browser styles. i.e unstyles everything 
makes everything homogenous 

ex: font-size for all elements are made the same
the bold text and font size differences between h1 and h6 are removed
all the same

#### Normalizing CSS - removes many CSS defaults but keeps useful defaults the same
It is a minimal reset, preserves useful default

ex: h1 and h4 retain their differences


I would use normalize for most sites except reset when I have an unconventional site, not sharing any need for defaults


3. Describe floats and how they work.

Float is a positioning property in css
Floats keep the item in flow, for example, text wraps around floating div, rather than being unaffected
Moves item to left or right, and the remaining elements move to fill in space.


Position absolute removes from flow. 


### Float - Four values: direction to float

- Left
- Right
- None (default)
- Inherit (from parent)


Clear prevents item from filling in space left by float
Clear both, therefore, prevents filling in both sides

For example, floating left leaves space on right for rest of elements to fill in
vice versa

clear left prevents elements from filling that space, the right


### Clear - Four values also: direction to go to avoid float

- Left
- Right
- None (default)
- Both
- Inherit (not supported by ie)

float right, the text clears left by default
float left, clear right


### To prevent text from going with flow, we clear it in same direction, or both
clear: same direction
or 
clear: both

this causes element to drop beneath the floats


### Problems:

- If parent div only contains floats, it will have a height of 0


### Solutions:

- If it contains any non floats, or clears, it will be fine and take full height of children
- add an empty div to end with clear both property (<div style="clear: both;"></div>)
- overflow method
- clearfix method: puts invisible ".". This is added to the *parent* element


### Clear Div method

- place empty div with clear: both property after all the floats


https://css-tricks.com/all-about-floats/

4. Describe z-index and how stacking context is formed.

### Stacking order - refers to order of overlapping elements along z-axis, i.e which one is on top


### Stacking context - refers to order of elements/stacking order *within* a common parent
outside of parent, different stacking order

z-index is not as simple as higher, on top and lower, on bottom.

### Rules: 

	1. Order on dom: lower, on top, if no z-index, no position
	2. position property, creates stacking context
	3. z-index, (only applicable if position property) higher z-index places element higher on context, relative to other children. This comparison does NOT extend across other contexts, or to the children of divs outside of parent
	4. opacity + z-index, places greater priority than mere z-index, if opacity < 1 Ex: opacity: 0.99;
	5. Once z-indexes within context or parent element are compared, move up node and compare upper elements.


z-index is only within stacking context, and parent, even if z-index is higher than children's, still beneath, because different stacking context

https://stackoverflow.com/questions/34755770/modal-appear-behind-fixed-navbar

### If modal appears over heaeder :
Instead of placing modal in footer, place modal in header, so it will be in same stacking context and a higher z-index will place modal over header


5. Describe BFC (Block Formatting Context) and how it works.



6. What are the various clearing techniques and which is appropriate for what context?



7. Explain CSS sprites, and how you would implement them on a page or site.

### CSS sprites is a single large image that contains many smaller images/image collection
It is used commonly with icons


To use:

	1. use sprite generator to combine into collection
	2. Set same background image for multiple css classes
	3. Set background-position, height, width, to show only part of sprite
	4. Usually automated background-position and h and w using gulp and other tactics


Pros:

	1. Faster image loading



### Summary

Positioning properties


#### in flow - affects positioning of other elements
#### out of flow - removes element from other elements, positioning of others not affected


position: relative, float, margins, paddings, keep element inside flow, so other elements acts as if still there

position: absolute, removes from flow


display: inline-block, block, inline, visiblility: visible, visiblity: hidden, all keeps in flow


display: none, removes from flow




position relative, and positon absolute: on resizing, does not float closer, but is covered

vs

floats: allows reflow on resizing