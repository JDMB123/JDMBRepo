# AA Times Continued

## Make Sure you finish Phases 1-3 before continuing!

### Phase 4: The Main Content

For the next phase we will add the latest App Academy Times news using a
flexible grid system. The `docs/copy` folder contains the content for each
section, which we will copy and paste. We will building the HTML structure
around the content, like we did for the Masthead. But first let's make sure we
have a flexible application by implementing a custom grid system.

## Custom Flexible Grid

Grids are much less complicated than they sound and are commonly used throughout
the web. Popular style frameworks like `bootstrap` by Twitter and `material-ui` inspired by
Google all use flexible grid systems. For App Academy Times, hand-roll a
simple grid just like you did in the [CSS Homework][css-grid-homework].

Define your grid's CSS in the `grid.scss` stylesheet. Make sure to include the
media query with a nice break point that maintains your design like `1000px`,
so that it behaves like so:

![custom-grid](https://assets.aaonline.io/fullstack/html-css/projects/aa_times/solution/docs/screenshots/grid.gif)

**N.B.**: Please don't just copy and paste any code. Writing out and debugging
CSS/HTML is the best way to learn!

[css-grid-homework]: http://assets.aaonline.io/fullstack/html-css/assets/custom_grid.css


## News Content

[News Content Mockup](http://assets.aaonline.io/fullstack/html-css/projects/aa_times/solution/docs/screenshots/main_content.jpg)

Copy and paste all the content from `docs/copy/main_content.txt` to
`views/shared/_main_content.html.erb`. Start by using your newly defined grid
classes with `section` elements to structure the content into flexible columns.

Use the following code snippet to embed the video content from YouTube:

```html
<iframe width="560" height="315" src="https://www.youtube.com/embed/ARe9FupzuOA" frameborder="0" allowfullscreen></iframe>
```

**N.B.**: Iframes define a frame that contains another website's content. They
allow you to put that other site's content on your website. Many content
services want other sites to use iframes present their information because
they allow them to maintain control over access to their content.

Once you have all of your content defined in flexible columns, follow the mockup style. Add additional HTML elements if necessary. Here are some guidelines:

- Headers like "Opinion Pages" and "Cat Academy" are bold.
- `.hr-top` and `.hr-bottom` defined in `layout.scss` can be used to get the
double lines that separate different content.
- We used a pseudo content `:after` and `content = ''` to create the blue
square next to the comments link.
- Using `flex: 1` on the input element will force it to grow or shrink to take
up all the space next to it's flex sibling Sign Up button
- Place the `new_office.jpg` image inside of a div with a class like
`thumbnail`. This way you can reuse this `thumbnail` class with a styled
`height` in px and then make all images `width: 100%` & `height: 100%`. Use
`object-fit: cover` on all images inside `thumbnail` to assure the images cover
the containing div correctly.
- Try to put as many of the application-wide selectors into the `layout.scss`
file as possible. Selectors such as `h1, h2, img, small, hr, .thumbnail` etc.
make more sense in the layout file because we will likely reuse them.

**Get A TA to Review your page before continuing**

---

# Phase 5: The Sections Sidebar

Now try resizing the window. Notice that our flexible website breaks a bit
because we don't have flexible fonts. We will leave this discussion for another
time and instead use media queries to complete our responsive design. Notice how
the amount of links in the Sections Nav is too big for smaller screen sizes (ie.
mobile screens). Let's adjust for mobile!

[Mobile Mockup](http://assets.aaonline.io/fullstack/html-css/projects/aa_times/solution/docs/screenshots/mobile.png)

- Write a media query similar to the one used in the `grid.scss` to hide the
sections nav at the same viewport width that the columns convert to `100%`.
- Write a similar media query to hide the Language Nav.
- Finally hide the "Subscribe" button, "Login" button and take the margin off the `.left-nav` in the `main_nav` styles. We added a bit of padding as well.

**N.B.** With just these few media queries and a flexible grid system we have a completely responsive website!

Now let's code a Sections Sidebar so that mobile users still have a way of
navigating all of the different App Academy Times sections. Style it according
to the mockup.

[Sections Sidebar Mockup](http://assets.aaonline.io/fullstack/html-css/projects/aa_times/solution/docs/screenshots/sections_sidebar.jpg)

- Copy and paste the HTML from the `sections_nav.html.erb` file into the
`sections_sidebar.html.erb` file to use as a skeleton and guide.
- Take a look at the `app/assets/javascripts/components/sidebar.js` to see how
the Sidebar functions.
- Add the `<%= render partial: 'shared/sections_sidebar' %>` to the
`_main_nav.html.erb` as a child of the corresponding list element with
`id="sections-sidebar-btn"`. - In `_sections_sidebar.scss`, start with a
selector to style the `opacity: 0` normally and `opacity: 1` when it has the
additional `.expand` class.

**N.B.** We use opacity here instead of display because it is transition-able.

This is the effect we are going for:

![Sidebar Example](https://assets.aaonline.io/fullstack/html-css/projects/aa_times/solution/docs/screenshots/sidebar.gif)

- Copy and paste the content from `docs/copy/sidebar_submenus.txt`.
- Add the remaining HTML to the `sections_sidebar` by nesting `ul` elements
within the `li` elements that require an additional dropdown.

Create pure css dropdowns with the following example code:

```html
<section class="dropdown">
    <ul>
        <li>lorem ipsum</li>
        <li>Lorem ipsum dolor</li>
    </ul>
</section>
```

```css
.dropdown {
    position: relative;
}
.dropdown > ul {
    display: none;
    position: absolute;
    /* use top, left, right, bottom to position */
}
.dropdown:hover > ul {
    /* applies the following style to uls inside .dropdown */
    /* but only when .dropdown is being hovered over */
    display: block;
}
```

Use pseudo element [css triangles](https://css-tricks.com/snippets/css/css-triangle/) on top of triangles to create
the arrows for the menu items as well as the submenu dropdown triangles. This
code could apply right arrows to the list items in the dropdown HTML from
above:

```css
.dropdown li {
    position: relative;
}
.dropdown li:after,
.dropdown li:before {
    content: "";
    position: absolute;
    right: 0;
    top: 25%;
    border-left: 5px solid gray;
    border-top: 5px solid transparent;
    border-bottom: 5px solid transparent;
    width: 0;
    height: 0;
}
.dropdown li:after {
    right: 2px;
    border-left: 5px solid white;
    z-index: 1;
}
```

---

# Phase 6: Search Modal

[Search Modal Mockup](http://assets.aaonline.io/fullstack/html-css/projects/aa_times/solution/docs/screenshots/search_modal.jpg)

Modals are distinct from dropdowns because they appear to float independently
over the application. A common characteristic of a modal is also that the app
beneath becomes more opaque and clicking away from the modal will close it.

Take a look at the `search-modal.png` screenshot to get a better idea of what
this is supposed to look like. Use the `search-modal.js` file to get the id
necesary for the search button, modal and overlay.

Create the HTML in the `_search_modal.html.erb` file and style in
`_search_modal.scss`. We created a `<section id="overlay" class="overlay
hidden"></section>` at the bottom of the `main_content` section.

Here is a trick to making content take up the full width of the viewport even
when inside of a smaller container by using viewport units (`vw = viewport
width, vh = viewport height`). You can read more about viewport units and full width containers
in limited width parents [here][css-tricks-containers].

```css
  position: absolute;
  width: 100vw;
  left: calc(-50vw + 50%);
```

- We used this trick both to make the full width search modal and overlay
- `height: 100%` is not transitionable...use `max-height` instead
- Inset box shadows with `box-shadow: inset 2px 3px 3px rgba(0,0,0,0.07);`

Before continuing **Call over a TA for review**.

[css-tricks-containers]: https://css-tricks.com/full-width-containers-limited-width-parents/

# Bonus: A Fixed Header

Use what you have learned to create a Fixed Header. When scrolling past the
`sections_nav` a `fixed_sections_nav` should appear. Use the
[NYTimes](http://nytimes.com) as an example.

# Additional Reading

Additional reading from today's project:
+ [guard][guard-livereload]
+ [sass][sass-features]

[guard-livereload]: https://mattbrictson.com/lightning-fast-sass-reloading-in-rails
[sass-features]: https://github.com/rails/sass-rails#features