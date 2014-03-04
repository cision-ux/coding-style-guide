PR NEWSWIRE UX CODING STYLES
==================

Welcome to the PR Newswire coding styleguide. We use this small set of guidelines within our team to keep our code consistent and readable. A lot of the rules in this document were borrowed from the Github's and Google's coding styleguides, Javascript: The Good Parts by Douglas Crockford, and Javascript Patterns by Stoyan Stefanov. All of these are excellent additional reading material, especially the two Javascript books.

If you are working on a project that an outside team has previously been working on, do not use this guideline, but conform to the style of the code already in place.

## Organization of projects

All current work should be tracked with svn.

File structure can be largely dependent on the type of project and framework you are using. However, in general all Javascript files should be placed in a `js` folder, all CSS in a `css` folder within the `stylesheets`, and all images in an `img` folder. LESS files should be place in a `less` folder within the `stylesheets` folder, like so `stylesheets/less/`.

## Code Editors
Configure your editor to "show invisibles". This will allow you to eliminate end of line whitespace, eliminate unintended blank line whitespace, and avoid polluting commits.

## CSS

Before reading this, you should have a good understanding of CSS specificity, and the [LESS](http://lesscss.org/) syntax. As a rule of thumb, don't nest further than 3 levels deep. If you find yourself going further, think about reorganizing your rules (either the specificity needed, or the layout of the nesting).

- Use two-space, soft-indentation (`  `).
- Use LESS on everything you can.
- Use dashes in class names (`.navbar-top`).
- Use meaningful class names (`.button-primary` instead of `.yee-1901`). Classes should define why that style is there not what it looks like.
- End every declaration with a semicolon (`;`) for consistency and extensibility reasons.
- Each selector should be on its own line, ending in either a comma or an opening curly brace. Add a single space after selectors and colons in style definitions like so:
```css
.selector-1,
.selector-2,
.selector-3 {
  background: #fff;
  color: #000;
}
```
- Not like this:
```css
.selector-1, .selector-2, .selector-3 {
  background: #fff;
  color: #000;
}

.selector-1 { background: #fff; color: #000; }
```
- Put a blank line between rules.
- Use single quotation marks (`''`) instead of double quotation (`""`) marks for attribute selectors (`h2[rel='friend']`) or property values. Do not use quotation marks in URI values (`url()`).
- Use underscore (`_`) for images, no camelCase.
- Only underline links.
- when possible use margin-bottom instead of top
- use a “last-of-type” or “first-of-type” class when you need to remove styling on the first or last element (LOOK INTO AND SHARE AN EXAMPLE IN USE)

### LESS
Divide your CSS styling in to separate LESS files following the boostrap setup.
- alerts.less
- badges.less
- breadcrumbs.less
- button-groups.less
- buttons.less
- carousel.less
- close.less
- code.less
- component-animations.less
- dropdowns.less
- forms.less
- grid.less
- input-groups.less
- jumbotron.less
- labels.less
- list-group.less
- media.less
- mixins.less
- modals.less
- navbar.less
- navs.less
- normalize.less
- pager.less
- pagination.less
- panels.less
- popovers.less
- print.less
- progress-bars.less
- responsive-utilities.less
- scaffolding.less
- tables.less
- theme.less
- thumbnails.less
- tooltip.less
- type.less
- utilities.less
- variables.less
- wells.less

### Pixels vs. Ems

Use `px` for `font-size`, because it offers absolute control over text. Additionally, unit-less `line-height` is preferred because it does not inherit a percentage value of its parent element, but instead is based on a multiplier of the `font-size`.

    li {
      font-size: 16px;
      line-height: 1.3;
    }

### Specificity (IDs vs. Classes)

Do not use ID selectors in your CSS, only use classes. When in doubt, use a class name. IDs, however, can still be used in your HTML for Javascript hooks and fragment identifiers.
- Good candidates for ids: header, footer, modal popups.
- Bad candidates for ids: navigation, item listings, item view pages (ex: issue view).

When styling a component, start with an element + class namespace (prefer class names over ids), prefer direct descendant selectors by default, and use as little specificity as possible. Here is a good example:
```html
<ul class="category-list">
  <li class="item">Category 1</li>
  <li class="item">Category 2</li>
  <li class="item">Category 3</li>
</ul>
```
```css
ul.category-list { // element + class namespace

  &>li { // direct descendant selector > for list items
    list-style-type: disc;
  }

  a { // minimal specificity for all links
    color: #ff0000;
  }
}
```
- If you must use an id selector (#selector) make sure that you have no more than one in your rule declaration. A rule like #header .search #quicksearch { ... } is considered harmful.
- When modifying an existing element for a specific use, try to use specific class names. Instead of .listings-layout.bigger use rules like .listings-layout.listings-bigger. Think about ack/greping your code in the future.
- The class names disabled, mousedown, danger, hover, selected, and active should always be namespaced by a class (button.selected is a good example).
- Try your absolute hardest to never use the `!important` flag, except for in rare occasions; it is always a better idea to use specificity in your selectors than using `!important`.


## Markup
A proper Doctype which triggers standards mode in your browser should always be used. Quirks mode should always be avoided.

For simplicity we will use the `html5` doctype, which is easy to remember.
```
<!DOCTYPE html>
```
### Page structure
```
html
├── head_include <head>
│   ├── <meta>
│   └── <link>
├── nav_include <nav>
├── <body>
│   ├── <div class="section"> (this will divide the content with border)
├── footer_include <footer>
└── scripts_include
    ├── <script>
```
- Paragraphs of text should always be placed in a `<p>` tag. Never use multiple `<br/>` tags.
- Items in list form should always be in `<ul>`, `<ol>`, or `<dl>`, Never a set of `<div>` or `<p>`
- Every form input that has text attached should utilize a `<label>` tag. *Especially radio or checkbox elements*.
- Even though quotes around attributes is optional, always put quotes around attributes for readability.
```html
<p class="line note" data-attribute="106">This is my paragraph of special text.</p>
```
- Make use of `<thead>`, `<tfoot>`, `<tbody>`, and `<th>` tags (and Scope attribute) when appropriate. (note: `<tfoot>` goes above `<tbody>` for speed reasons. You want the browser to load the footer before a table full of data.)
```html
<table summary="This is a chart of invoices for 2011.">
  <thead>
    <tr>
      <th scope="col">Table header 1</th>
      <th scope="col">Table header 2</th>
    </tr>
  </thead>
  <tfoot>
    <tr>
      <td>Table footer 1</td>
      <td>Table footer 2</td>
    </tr>
  </tfoot>
  <tbody>
    <tr>
      <td>Table data 1</td>
      <td>Table data 2</td>
    </tr>
  </tbody>
</table>
```
- Use `title=""` in `<a>` tags.
- Close tags with comments (`<!--.row-->`).
- Use `alt=""` and `title=""` in <img> tags.
- Use `<col-sm-#>` as a base for your grid.
- Do not use `.row` for full width items like H tags unless necessary.
- All subheads should be in `<small>`.
- Do not treat H tags like a container by putting elements inside (`<h1>`).
- Do not use in-line js/jQuery.



## Javascript

Liberally comment your code to keep it readable and maintainable. Avoid using multiline block comments (`/* ... */`), use singleline comments instead (`// ...`).

Avoid global variables. A good way to do this is to declare a single object variable to act as a container for your entire javascript application.

    var MyApp = {};

    MyApp.init = function() {
      ...
    };

When retrieving and setting values from objects, use dot notation (`yourObject.yourKey`) instead of bracket notation (`yourObject["yourKey"]`) wherever possible. Dot notation is more compact and reads better.

Declare all variables used in a function at the very top of the function in a single `var` declaration.

    function func() {
      var a = 1,
          b = 2,
          c = {};

      // function body
    }

This is a good practice because it helps with readability and reduces the possibility of logical errors caused by hoisting. When using the single `var` declaration each new variable name should be on it's own line and indented to be inline with the first variable name.

When chaining or cascading method calls on an object, each method call should be on it's own indented line.

    $('#element')
      .height(300)
      .append('<img />');

### Style

- **NEEDS TO BE DECIDED** Do not rely on semicolon insertion. VS Do your best to never use a semicolon. This means avoiding them at line breaks and avoiding multi-statement lines. For more info, read [Mislav's blog post](http://mislav.uniqpath.com/2010/05/semicolons/).
- Use two-space, soft-indentation.
- Use camelCase for naming variable and function names, except for constructor functions that need to be called with the new prefix. For these use Capitalization.
- Try to prefix all javascript-based selectors with `js-`. This is taken from [slightly obtrusive javascript](http://ozmm.org/posts/slightly_obtrusive_javascript.html). The idea is that you should be able to tell a presentational class from a functional class. Most of the codebase doesn't do this, let's try and move toward it.


## Words
Act more like a human and less like a computer. Respect the reader, act like a human and use fewer words.

For example, instead of:
```
Successfully deleted the #{branch_name} branch.
```
Perhaps choose something like:
```
Okay, the #{branch_name} branch has been deleted.
```
## In Conclusion

Be consistent!



If you’re editing code, take a few minutes to look at the code around you and determine its style. If they use spaces around all their arithmetic operators, you should too. If their comments have little boxes of hash marks around them, make your comments have little boxes of hash marks around them too.

The point of having style guidelines is to have a common vocabulary of coding so people can concentrate on what you’re saying rather than on how you’re saying it. We present global style rules here so people know the vocabulary, but local style is also important. If code you add to a file looks drastically different from the existing code around it, it throws readers out of their rhythm when they go to read it. Avoid this.
