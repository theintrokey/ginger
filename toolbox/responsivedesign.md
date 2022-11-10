CHAPTER 11
# Responsive Design

Responsive design is a technique for designing page layouts so that they are usable on devices with a variety of different screen sizes. Media queries are one of the main tools used for responsive design, as are flexbox and CSS Grid.

A layout that looks good on a high-resolution desktop display might not look so good on an iPhone. Media queries allow you to apply different CSS rules, or even entire style sheets, depending on the size of the viewport.

Media queries have other uses, too. For example, you can apply a different set of styles for when a page is printed than when it is displayed on a screen by using the print medium.

## The viewport meta tag

In order for a site to look correctly on mobile devices, you will need to add the viewport meta tag to your HTML inside the head element:

```html
<meta
 name="viewport"
 content="width=device-width, initial-scale=1.0">
 ```

This tells the browser how to set the page’s dimensions and zoom level. The typical value used for width is device-width; however, this could also be set to an explicit pixel width as well.

## Media queries
A media query is defined as an at-rule, @media. It specifies a medium (all, print, screen, or speech) and a condition. If no medium is specified, it defaults to all. If the condition is met, the CSS rules inside the block are applied to the document. If it is not met, the CSS rules are ignored.

Listing 11-1 has an example of a media query.

Listing 11-1. An example media query
```css
h1 {
 color: red;
}
@media screen and (max-width: 400px) {
 h1 {
 color: blue;
 }
}
```
In a viewport that has a width of 400px or less, h1 elements will be blue. Otherwise, they will be red. Media queries are constantly being evaluated and styles conditionally applied. They aren’t only calculated when the page first loads. You can test the given CSS by opening the page using it and notice the h1 elements are red. If you resize the window to below 400px, the h1 elements will change from red to blue. Resize the screen back above 400px, and they will turn red again.

With responsive design, the min-width and max-width rules are commonly used, as they are good indicators of viewport size. There are many other media query rules. For example, this rule will apply only when the user’s device is in landscape orientation:

```css
@media (orientation: landscape)
```

Some queries are based on physical attributes of the device (such as width or orientation), but others are based on settings the user has configured in their operating system. In Chapter 9, we saw the prefers-reduced-motion query. Another example of a preference-based query is prefers-color-scheme. On platforms that support “dark mode,” such as macOS, this can be used to query if the user is using dark mode:

```css
@media (prefers-color-scheme: dark)
Media queries also support logical operators such as and, or, and not:
@media screen
 and (min-width: 600px)
 and (orientation: landscape)
 ```

The only operator is also supported. Using only assures that a media query’s rules are not applied on older browsers that don’t understand the full query.

Media queries can also be used to conditionally load an entire style sheet. For example, you may want to apply an entirely different style sheet if the page is being printed using the HTML in Listing 11-2.

Listing 11-2. Conditionally loading style sheets
```html
<link rel="stylesheet"
 href="style.css"
 media="screen">
<link rel="stylesheet"
 href="print.css"
 media="print">
 ```
## Breakpoints
A breakpoint is the threshold at which a page’s layout will change due to the viewport size with a media query. Defining your breakpoints is not an exact science, as there are many different devices in use today, all with different screen sizes. It’s better to set breakpoints based on the content. That is, you should try to avoid targeting specific devices with media queries. Instead, experiment with different viewport sizes, and find the points where your layout and design start looking cramped. Then you know where to set your breakpoints.


Figure 11-1 shows an example layout, with a viewport width of 1,000 pixels.

The only CSS that has been applied is that the h1 element at the top has been set to a
font-size of 5rem. If we start to shrink the viewport, we’ll see that the heading text wraps at around 785 pixels, as shown in Figure 11-2.

Figure 11-1. An example layout

The headline takes up a lot of vertical space now, so this might be a good place for a
breakpoint. We can make its font smaller when the viewport is 785 pixels or less by using
the media query in Listing 11-3.

Listing 11-3. Applying a media query to make the heading font smaller
```css
@media screen and (max-width: 785px) {
 h1 {
 font-size: 3rem;
 }
}
```
Figure 11-3 shows the resulting layout. Now when we view the site at that viewport size, the heading is smaller and takes up less vertical space, since it doesn’t wrap.

Figure 11-2. The heading text wrapped

This will result in more content being visible on devices with a smaller viewport. If we start resizing the viewport again, we’ll find that the heading is wrapping again at around 480 pixels, as shown in Figure 11-4.


Figure 11-3. The heading text is smaller at this viewport size


Figure 11-4. The heading is wrapping again


We can specify another breakpoint here to again prevent the heading from wrapping
in Listing 11-4.

Listing 11-4. Adding another media query
```css
@media screen and (max-width: 785px) {
 h1 {
 font-size: 3rem;
 }
}
@media screen and (max-width: 480px) {
 h1 {
 font-size: 2rem;
 }
}
```

The result is shown in Figure 11-5, where the heading text is very small. At this breakpoint, the image looks really big compared to the heading size. We can make the image a little smaller at this breakpoint inside the same media query. This is done in Listing 11-5.

Figure 11-5. The heading text gets even smaller at this viewport size

Listing 11-5. Adjusting the image size
```css
@media screen and (max-width: 785px) {
 h1 {
 font-size: 3rem;
 }
}
@media screen and (max-width: 480px) {
 h1 {
 font-size: 2rem;
 }
 img {
 width: 250px;
 }
}
```
The resulting layout is shown in Figure 11-6, where the image is smaller.

Figure 11-6. The image is smaller at this viewport size

Now, the image looks better sized relative to the rest of the content.


### Responsive layouts with flexbox
Some responsive layouts can be achieved without even using media queries. For example, we can use the flex-wrap property on a flex container to automatically wrap elements to the next line if the viewport is too narrow, in order to prevent the need for horizontal scrolling. Listing 11-6 contains an example flexbox layout.

Listing 11-6. An example layout
```html
<style>
 .container {
 display: flex;
 flex-direction: row;
 justify-content: center;
 background: skyblue;
 padding: 0.25rem;
 }
 .item {
 background: red;
 color: white;
 text-align: center;
 margin: 0.25rem;
 font-size: 2rem;
 }
 .wide {
 width: 300px;
 }
</style>
<div class="container">
 <div class="item">Flex Item 1</div>
 <div class="item wide">Flex Item 2</div>
 <div class="item">Flex Item 3</div>
 <div class="item">Flex Item 4</div>
 <div class="item wide">Flex Item 5</div>
 <div class="item">Flex Item 6</div>
</div>
```
With a wide enough viewport, this results in the layout shown in Figure 11-7.

This looks pretty good. Let’s see how this looks with a narrower viewport, shown in Figure 11-8.

Now it’s looking a little cramped. Let’s go even narrower, like if we were viewing this layout on a mobile device, shown in Figure 11-9.

The flex items have shrunk as much as possible, but the viewport still isn’t wide enough, so the first and last items get cut off. We can easily solve this problem by setting flex-wrap to wrap on the container. This is shown in Listing 11-7.

Figure 11-7. The rendered layout with a wide viewport

Figure 11-8. The layout with a narrower viewport

Figure 11-9. The layout with an even narrower viewport

Listing 11-7. Adding flex-wrap: wrap
```html
<style>
 .container {
 display: flex;
 flex-direction: row;
 justify-content: center;
 flex-wrap: wrap;
 background: skyblue;
 padding: 0.25rem;
 }
 .item {
 background: red;
 color: white;
 text-align: center;
 margin: 0.25rem;
 font-size: 2rem;
 }
 .wide {
 width: 300px;
 }
</style>
<div class="container">
 <div class="item">Flex Item 1</div>
 <div class="item wide">Flex Item 2</div>
 <div class="item">Flex Item 3</div>
 <div class="item">Flex Item 4</div>
 <div class="item wide">Flex Item 5</div>
 <div class="item">Flex Item 6</div>
</div>
```
The resulting layout is shown in Figure 11-10, where the layout items now wrap.

Now, it looks much better in the narrow viewport. If we go even narrower, the layout
will change to accommodate the new size, as shown in Figure 11-11.

## Fluid typography
Earlier, we saw how to leverage media queries to adjust the font size as the viewport size changes. With fluid typography, it’s possible to automatically scale the font size to viewport size without having to use media queries.

Earlier in the book, we discussed the vw unit, which is equal to 1% of the viewport width. We can use vw to specify a font size as a proportion of the viewport width. For example, for a 1,000-pixel-wide viewport, 1vw is equal to 10px. Suppose that we want 

Figure 11-10. The wrapped layout with a narrow viewport

Figure 11-11. The layout on an even narrower viewport

our header to have a font size of 48px for a 1,000-pixel-wide viewport. We can specify the
font-size as 4.8vw. Figure 11-12 shows what that looks like. However, there’s a problem. If the viewport becomes very wide, the font size of the heading becomes very large – at a viewport size of 2,000 pixels, the font size becomes 96px. Look at the font size of the heading in Figure 11-13 compared to the body text size.

On the other extreme, if the viewport is very narrow, the heading’s font size becomes
very small – almost as small as the body text, shown in Figure 11-14.

Figure 11-12. Using a variable font size proportional to the viewport width
Figure 11-13. A very large font size

### The clamp function
We can fix this by using the clamp function. clamp takes three arguments: the minimum size, the preferred size, and the maximum size. We can keep our font size of 4.8vw as the preferred size and add a lower bound of 48px and an upper bound of 64px: font-size: clamp(48px, 4.8vw, 64px);
Now the font size adjusts automatically with the viewport width as before, but now it will never drop below 48px or go above 64px.

## Responsive images
Previously, we used a media query to change the size of an image if the viewport was narrower than a certain threshold. There is another technique we can use that allows images to scale with the viewport width without using media queries.

Figure 11-15 shows our layout from before, using an image that is 800 pixels wide.
Figure 11-14. The heading font is very small for a narrow viewport


It looks good at this width, but what happens if the viewport is less than 800 pixels
wide? This is illustrated in Figure 11-16.

At this viewport size, the image is cut off and requires horizontal scrolling to view the
rest of it. We can change this behavior so that the image resizes along with the viewport
(or its container) with two CSS properties:
```css
img {
 max-width: 100%;
 height: auto;
}
```
Figure 11-15. An 800 pixel wide image

Figure 11-16. The image with a viewport width of less than 800 pixels

This sets the image so that its width never exceeds the width of its container. The height: auto makes sure that the image retains its aspect ratio.

Now, as we resize the viewport, the image is resized and maintains the proper aspect ratio, as shown in Figure 11-17.

After making these changes, the CSS for our responsive page is very simple, shown in Listing 11-8.

Listing 11-8. The final CSS for this layout
```css
img {
 max-width: 100%;
 height: auto;
}
h1 {
 font-size: clamp(48px, 4.8vw, 64px);
}
```

## Adapting a layout with media queries
There are still good use cases for media queries with responsive design, however. Let’s
look at the page layout in Listing 11-9.

Figure 11-17. The image now resizes with the viewport

Listing 11-9. A page layout
```html
<style>
 body {
 margin: 0;
 }
 .container {
 display: flex;
 flex-direction: column;
 height: 100vh;
 }
 .header {
 background: orange;
 padding: 1rem;
 }
 .main {
 display: flex;
 flex-direction: row;
 flex-grow: 1;
 }
 .content {
 background: salmon;
 padding: 1rem;
 flex-grow: 1;
 }
 .sidebar {
 display: flex;
 flex-direction: column;
 background: skyblue;
 padding: 1rem;
 }
 .sidebar a {
 margin: 1rem;
 padding: 0.5rem 2rem;
 border: 1px solid black;
 }
 .sidebar2 {
 background: lime;
 padding: 1rem;
 }
 .footer {
 background: beige;
 padding: 1rem;
 }
</style>
<div class="container">
 <header class="header">Header</header>
 <main class="main">
 <nav class="sidebar">
 <a href="/home">Home</a>
 <a href="/about">About</a>
 <a href="/photos">Photos</a>
 </nav>
 <div class="content">
 Hello world!
 </div>
 <div class="sidebar2">
 Sidebar 2
 </div>
 </main>
 <footer class="footer">Footer</footer>
</div>
```
This results in the layout shown in Figure 11-18.

If we decrease the viewport width, the main content area gets squashed between the two sidebars, as seen in Figure 11-19.

Figure 11-18. The rendered layout

Figure 11-19. The narrow layout

We can improve this by adding a media query and making a few overrides. Let’s set the breakpoint at 700 pixels. Below this threshold, we’ll change the main element to have a flex-direction of column rather than row. This will stack the three regions vertically, allowing them each to take up the full width of the container. The media query is shown in Listing 11-10.

Listing 11-10. Adding a media query to the main element
```css
@media screen and (max-width: 700px) {
 .main {
 flex-direction: column;
 }
}
```
Now the content takes up the full width and is no longer constrained horizontally, as shown in 

Figure 11-20. The new layout takes effect at 700 pixels or less.
Figure 11-20. The adjusted layout at its threshold of 700 pixels

The navigation is taking up a lot of vertical space now, though. We can add another override inside the media query, shown in Listing 11-11, to change the navigation links to be horizontal.

Listing 11-11. Adding another override
```css
@media screen and (max-width: 700px) {
 .main {
 flex-direction: column;
 }
 .sidebar {
 flex-direction: row;
 justify-content: center;
 }
}
```
The resulting layout is shown in Figure 11-21.

Figure 11-21. The navigation links laid out horizontally

This responsive layout looks a lot better with a narrower viewport. But this is still a wider viewport than that of a mobile device. Let’s shrink it down further, to 350 pixels, in Figure 11-22.

Now the navigation links are overflowing the viewport. We can fix this by setting flex-wrap to wrap in Listing 11-12.

Listing 11-12. Adding flex-wrap: wrap
```css
@media screen and (max-width: 700px) {
 .main {
 flex-direction: column;
 }
Figure 11-22. The layout as it might appear on a mobile device
Chapter 11 Responsive Design
251
 .sidebar {
 flex-direction: row;
 justify-content: center;
 flex-wrap: wrap;
 }
}
```
In Figure 11-23, we can see that the navigation links now wrap.

This looks better – the navigation links no longer overflow the viewport. There are still some other ways we could improve on this design. For example, at the narrow viewport size, we could replace the navigation links with a dropdown or popup menu. This would probably involve some JavaScript and DOM manipulation for toggling the menu.

Figure 11-23. The wrapped navigation links

We could also try to get this to fit on one line by making the navigation links smaller, removing the padding, as shown in Figure 11-24. This would work, but would probably be frustrating for mobile users, as the touch targets on the screen would be very small.

Figure 11-24. The layout with smaller links, which are not ideal for mobile

In this instance, the best option would probably be to add a menu of some kind in place of the navigation links on a narrow viewport like on a mobile device.

## Summary

We have seen just a few of the tools at your disposal to adapt your layouts and designs to
different screen sizes:

- Media queries allow CSS rules to be applied conditionally.
- A breakpoint is a threshold used in a media query, where there is a layout change.
- An element’s font size can be proportional to the width of the viewport and limited by using the clamp function.
- Sometimes, only minor changes are needed inside a media query, such as setting flex-wrap to wrap or the flex-direction from row to column in a flex container.
- Images can automatically resize to the viewport by setting max-width to 100% and height to auto.
