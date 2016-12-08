# HTML Styleguide

## Whitespace Rules

1. Never mix spaces and tabs; this is the **law**!

	If you are starting a project, and you have a choice, **USE TABS**. I personally believe tabs give more control to those that adopt the project. Many code editors and IDE's are now allowing users to customize the width of a tab.

	For readability, and if your editor allows, I recommend setting your editor's tab size to be equivalent to four spaces. This will help align multi-line declarations and conditions.

1. Never leave whitespace at line ends or within blank lines. Many editors and IDE's have a setting to remove all unnecessary white-space.

1. If your editor supports it, always work with the "show invisibles" setting turned on. The benefits of this practice are:

	* Enforced consistency
	* Eliminating end of line whitespace
	* Eliminating blank line whitespace
	* Commits and diffs that are easier to read

1. Set your line length at a maximum of 120 characters

1. Insert line-breaks, `\n`, after tag closures, `</>` or closing quote for attributes.

1. Double line-breaks should be used to separate same level elements from one another for increased readability.

## Know Your Elements

### Block Elements

Common block HTML4 elements:

`<html>` `<body>` `<div>` `<ul>` `<li>` `<p>` `<blockquote>` `<h1> - <h6>` `<table>` `<form>` `<fieldset>`

New block HTML5 elements:

`<header>` `<section>` `<article>` `<footer>` `<aside>`

Block-level elements represent a horizontal section of a document. These elements span the whole width of their container or parent element. Block-level elements can contain other block-level elements.

Block level elements do not need a break tag, `<br/>`, afterward to ensure any element falls below.

Don't do this:

	<div><!-- stuff --></div><br/>

The break tag is not needed since block elements naturally take up the whole width of the container element.

### Inline Elements

Common inline HTML4 elements:

`<a>` `<span>` `<strong>` `<img>`

Inline elements have no inherent width. These elements can be zero pixels wide to the full width of the container element. They get their width by whatever they are containing. So, if you have, say, an `<img>` element, it will just in herent the width of the actual image file it contains.

Their height is also dictated by what they contain. Inline elements can't (and won't follow) any top or bottom margin and padding; you can't set any height either.

Inline elements should not contain block elements.

### Inline-Block Elements

There are no natural `inline-block` elements (at least not within the current HTML5 standard), but block elements are best to convert to `inline-block`. These elements are created by the `display: inline-block;` property in CSS. These elements have properties of both block elements and inline. `inline-block` elements can contain any kind of element — block or inline.

`inline-block` elements take on the width of whatever they contain, unless specified otherwise. If an `inline-block` element contains a block element, then it will take up the full width of its container. If it contains an inline element, it is the width of whatever it contains. Therefor, if you place a block-level element within an `inline-block` element, you'll need to set a width.

### Style (Block) Element

Rarely, if ever, use the `<style>` block element. There are very few reasons to write css within style tags in HTML. Always use external stylesheets!

### Script Element

Including inline or in-page JavaScript should be avoided as much as possible. This again is going back to not mixing languages. JavaScript should be in .js files, CSS should be in .css files and HTML should be in .html files. So, if you have some page specific JavaScript that you don't want on your `site.js` file, create a separate `page.js` file and include it in just that page.

Don't do this:

	<script type="text/javascript">

		// Bunch of JS functions and specific to your page.

	</script>

	Do this instead:

		<script type="text/javascript" src="/js/page.js"></script>

But remember, cache anything that is used frequently throughout the site. If you are including different .js files throughout your site, find ways to write more reusable JavaScript so that you include it once and for all.

## Attributes

### Classes

Classes are traditionally used to add the hooks necessary for CSS styling, but not exclusively. When you use classes for selection in JS, then it's best to use a separate class with the prefix of `js_` so that other developers know which classes are used for styling and which are used for the JS. If you don't, another developer could easily change the class to alter styling, and accidentally break the site's JS. You should also have a `test_` class for selection in end-to-end tests.

### ID's

ID's must be unique and not shared with any other element in the document, they should follow the same naming pattern as classes and you can only have one ID per element. ID's should be rather permanent and not modified often. ID's should be reserved for JavaScript, and never used in CSS.

Why should you try to avoid using ID's in CSS? Well, because it's easy to get into a messy CSS specificity issue as ID's take precendence over other selector types.

### Style

Inline style attributes should rarely be used! Their use does have value for element animation.

### Events

Inline events like `onclick=""` should never be used. Use your view's or DOM selector library's event handlers.

## Conventions

### Use unordered lists for more than just text lists.

If you have repeating, related content, whether they are menus, multiple articles, images, videos, links … use unordered lists as elements.

Don't do this:

	<div>
		<div>Stuff</div>
		<div>Stuff</div>
		<div>Stuff</div>
		<div>Stuff</div>
		<div>Stuff</div>
	</div>

Do this instead:

	<ul>
		<li>Stuff</li>
		<li>Stuff</li>
		<li>Stuff</li>
		<li>Stuff</li>
		<li>Stuff</li>
	</ul>

By using this convention, you'll have better control over the elements since they have a natural parent child relationship. Much can be done without the need for classes.

### Use the least amount of elements as possible.

For maintainablity purposes and performance reasons, the least amount of elements to create the needed structure, the better. To accomplish this, use CSS3 to remove the need to redundant element wrapping, like for rounded corners and such.

## Know Your HTML5 Elements

Coming soon …