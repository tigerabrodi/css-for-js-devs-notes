# Fundamentals Recap:

- Pseudo-elements — these selectors target elements in the DOM that we haven't explicitly created with HTML tags.

- Use rems for typography due to the accessibility benefits. Users may higher their default browser font size.


# Rendering Logic 1:

- Browser treats inline elements as typography, hence line-height is applied to those elements.

- Inline-block elements internally act like block elements, but externally act like inline elements. The parent container will treat it as an inline element, since it's external. But the element itself can be styled like a block.

- Fit-content behaves like max-content, though if the content is too wide to fit in the parent, it add line-breaks as-needed.

- There are 7 layout modes in CSS, such as Grid and Flexbox layout. In Flow layout, the default layout mode, every element will use a display value of either inline, block, or inline-block. 

- Only vertical margins collapse. Margin collapse is unique to Flow layout. Nesting elements doesn't prevent collapsing. Margins can collapse in the same direction. More than two margins can collapse.

- Be aware of how you use margins. Don't set the specifically on components, in such cases it is better to use layout components. For reusable components, we want them to be as unopinionated as possible.


# Rendering Logic 2:

- If an absolute element does not have an anchor, it sits in its default in-flow position.

- You can center a positioned element by giving it a margin of auto and setting an equal distance from each edge.

- Positioned elements will always render on top of non-positioned ones. If both elements are using position, then the DOM order wins.

- One way to create a stacking context is to set position absolute or relative and a z-index to an element. You can also use position fixed or sticky by itself. Another way would be to give the isolation property a value of isolate.

- If a parent or grandparent uses the transform property, it becomes the containing block for the fixed element, essentially transforming it into an absolutely-positioned element.

- With sticky positioning, the value of top/left/right/bottom controls the minimum gap between the element and the edge of the viewport while the container is in-frame.


# Responsive and Behavioural CSS:

- To access localhost on your phone, in order to properly test on mobile, you can use a tunnelling service like "ngrok" (https://www.npmjs.com/package/ngrok#global-install). You can then visit the "Forwarding" URL.

- You can remotely debug your site on a mobile too, i.e. for Android: https://developer.chrome.com/docs/devtools/remote-debugging/.

- Common breakpoints: 0-550px — Mobile, 550-1100px — Tablet, 1100-1500px — Laptop, 1500+px — Desktop.


# Typography and Images:

- -webkit-line-clamp allows you to show ellipsis on a specific line of the text.

- columns sets the number of columns to use when drawing an element's contents and those columns' width.

- The text-indent CSS property sets the length of empty space (indentation) that is put before lines of text in a block.

- You can get the benefits of self hosting fonts while still using the fonts from Google by downloading the font files and only using the "latin" font faces within the CSS file which contains the font faces.

- You can get font weight from 100 to 900 by specifying it in the URL which Google Fonts give you. Example which includes doing it for italic and non-italic ones too: "Raleway:ital,wght@0,100..900;1,100..900".

- object-fit can be used to set the size of an image (img). Cover value keeps its ratio and fills the entire space, you can even set specific width and height if the images have different ratios but you still want them to be of the same size.

- object-position can be used to set the position of an image.

- For background images, to render the approriate resolution of the image, you can use @media and check for the min-resolution, the value it should take in this case would be dots per Pixel, dppx, i.e. 2dppx. Safari doesn't support this property though, hence, in the @media rule, we also have to check for -webkit-min-device-pixel-ratio, which would be the syntax for Safari, though it takes simple numbers as value.


# CSS Grid:

- Default value of grid auto flow is row, can be set to column.

- In CSS Grid, there's no such thing as a "primary axis" or a "cross axis". Rows are stacked on top of each other. Columns are inside the rows horizontally aligned beside each other.

-  Like display: flex, display: grid changes which layout mode its children use.

- We can use repeat to avoid duplication. Takes in the amount in number as first argument and size as second, i.e. height or width.

- Grids are composed of tracks and lines.

- auto-fit will span the elements if remaining space exist. auto-fill will try to keep its minimum size and keep filling in new rows or columns, even if no elements are in those spaces.

- repeat(
        auto-fill/fit,
        minmax(size, 1fr)
	);

- For size you can use "min" which CSS offers in order to make sure the items don't overflow on smaller screens, example: grid-template-columns: repeat(auto-fit, minmax(min(320px, 100), 1fr)).

- The place-content property will set both justify-content and align-content at the same time.

- A grid child can use z-index even if it doesn't change the position property.

- A trick: If your columns are growing beyond the viewport, you can use minmax(0px, auto) as value for them. This will ensure that the columns grows as needed, the width of their children, though will shrink to fit the viewport.


# Animations:

- When we use a percentage value in translate, that percentage refers to the element's own size, instead of the available space in the parent container.

- Ease-out transition is often used when something is entering off the screen, starts fast but ends slow, as if something came hustling from far away.

- Ease-in is for element that ends off screen.

- Doom flicker behaviour: Transform the child of the element that you transformed, to avoid the flickering from appearing when wanting to transform the element.

- Alternate direction ping-pongs between normal and reverse on subsequent iterations.

- Backwards fill mode allows us to apply the animation's initial state backwards in time.

- Fill mode of value "both" is best. The initial value is the start value of the animation, and the end of the animation, that value gets persisted.

- The animation-play-state CSS property sets whether an animation is running or paused.

- If you are using positoning such as bottom, top etc. and want your animation's transform to move in a specific direction, you may need to add the positioned value to the transform's translate.

- Inline elements can't be animated, a solution is to set them to inline-block, then you can animate them.

- Transform origin can help making an animation look more realistic.

- Will-change lets us be intentional about which elements should be hardware-accelerated. Everything comes with trade-offs, be intentional where you use will-change. Use it on elements that actually animate!

- You can achieve 3D transforms by using perspective. It is set on the parent of the element that gets transformed. The higher the value, the further a way the user is, the more it looks less 3D so to speak.

- There is also the perspective() function which you can set within the transform, in order to set the perspective for a specific element.

- The backface-visibility CSS property sets whether the back face of an element is visible when turned towards the user.

- Whenever we are doing anything with the layout, it makes more sense to have a display of block compared to inline.

- The transition's time within the state such as hover or active will be the one used when that particular state gets triggered. The original time and delay of the transition, set to the element, will be the one used once the element exists the state and returns back to its original position/style.

- When we apply transform-style: preserve-3d, we create a 3D rendering context. This is similar in philosophy to a stacking context. Due to a Firefox bug you may need to set transform-style of inhert on the direct child of the parent which has transform-style.

- Transitions look better if they are quicker when entering the state, and when leaving they are slower.

- When adding overflow of hidden, add a comment why you put it there so you don't forget next time why you used it in that place.


# Little Big Details:

- Filter can do a lot of cool visual manipulations to the element.

-  Applying hue-rotate(60deg) increases the hue of all colours by 60deg.

- You can clear like a blur glow effect on an element, i.e. an image. This requires you having both elements within a wrapper, centering both of them, and using blur on one of them. By having two or even more elements in a wrapper, you can accomplish quite neat things with the filter property.

- Nested Radiuses. A common mistake people do is to set the same value of border radius for both elements, both parent and child. This makes the elements not using the same center point, hence it doesn't look right. We would have to sum up the inner circle's radius as well as any padding or other spacing. We can use CSS variables to add the padding to the inner radius to the parent, the radius the child element is using.

- The first trick for cohesive shadows: every shadow on the page should share the same ratio. This will make it seem like every element is lit from the same very-far-away light source, like the sun.

- By layering multiple shadows, we create a bit of the subtlety present in real-life shadows.

-  The ::selection CSS pseudo-element applies styles to the part of a document that has been highlighted by the user (such as clicking and dragging the mouse across text).

- The backdrop-filter CSS property lets you apply graphical effects such as blurring or color shifting to the area behind an element.

- We can increase the tap size of an element by using a pseudo element, that is absolutely positioned and has the values top, left, right and bottom set to the same negative value.

- The pointer-events property allows us to set an element to be a hologram: you can see it, but you can't touch it.

- The clip-path CSS property creates a clipping region that sets what part of an element should be shown. Parts that are inside the region are shown, while those outside are hidden.

- You can animate and transition clip path, but it must have the same points, both before and afterward.

- Polygon, first value of a point represents the X axis, the second value of a point represents the Y axis.

- One straightforward way of transitioning or animating by using clip-path is to have the same elements within a parent, and for example on hover one will be revealed via clip-path, the element being revealed would have to have its position set to absolute.

- Scroll snap. scroll-snap-type — this controls the direction and precision of the scroll snapping. scroll-snap-align — this controls which part of the child we want to snap. 

- The shape-outside CSS property defines a shape—which may be non-rectangular—around which adjacent inline content should wrap. It also accepts a URL. Is used in combination with the float property.
