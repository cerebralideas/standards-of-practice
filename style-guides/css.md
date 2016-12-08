# CSS Styleguide

## Whitespace Rules

1. Never mix spaces and tabs; this is the **law**!

	If you are starting a project, and you have a choice, **USE TABS**. I personally believe tabs give more control to those that adopt the project. Many code editors and IDE's are now allowing users to customize the width of a tab.

	For readability, and if your editor allows, I recommend setting your editor's tab size to be equivalent to four spaces. This will help align multi-line declarations and conditions.

1. Never leave whitespace at line ends or within blank lines. Many editors and IDE's have a setting to remove all unnecessary white-space.

1. If your editor supports it, always work with the "show invisibles" setting turned on. The benefits of this practice are:

	- Enforced consistency
	- Eliminating end of line whitespace
	- Eliminating blank line whitespace
	- Commits and diffs that are easier to read

1. Set your line length at a maximum of 120 characters

1. Insert line-breaks, `\n`, after tag closures, `</>` or closing quote for attributes.

1. Double line-breaks should be used to separate same level elements from one another for increased readability.

## Beautiful Syntax

### Use multiple lines for CSS rules

Don't do this:

	.listElement{color:#ffff00;background:#000;}

Do this instead:

	.listElement {
		color: #ffff00;
		background: #000;
	}

### Use Shorthand when possible

Don't do this:

	.primaryHeader {
		font-family: serif;
		font-size: 2em;
		font-weight: 700;
		font-height: 1.5em;
	}

Do this instead:

	.primaryHeader {
		font: 700 2em/1.5em serif;
	}

### Use numeric version for values, not names

Don't do this:

	blockquote {
		background: lightgray;
		color: darkred;
		font-weight: bolder;
	}

Do this instead:

	blockquote {
		background: #ccc;
		color: #8D0A08;
		font-weight: 900;
	}

### Wrap URL's with single quotes

Don't do this:

	body {
		background: #333 url(/images/background.png);
	}

Do this instead:

	body {
		background: #333 url('/images/background.png');
	}

### Use line-breaks after commas to improve readability

Don't do this:

	.listEl, .anotherEl, .someQuote, #randomImg, .anotherThingy {
		font-family: serif;
	}

Do this instead:

	.listEl,
	.anotherEl,
	.someQuote,
	.anotherThingy {
		font-family: serif;
	}

### NEVER USE HACKS IN CSS STYLESHEETS

If you need to alter CSS for IE 8-, use HTML5 Boilerplate's method and use a conditional comment to add a class of ieX to the HTML tag.

Example:

	<!--[if lte IE 7]>
		<html class="ie6-7">
	<![endif]-->

## Conventions

### Multi-Column Layout

1. **Floats Should Rarely be Used, if ever.**

	Floats are the reason for many cross browser issues, can increase cross browser testing and development time, they break document flow and can be unpredictable at times. They also require a lot of hacking to ensure that they interact with their container and neighbors properly.

	Float was never designed to be used for laying out a website or web app. It was originally designed to be used for images within text blocks to allow content to flow around the image, not blocking the content's natural flow.

1. **Inline-Block Should be Used Most, if not All of the Time.**

	Inline-block was specifically designed for creating multi-column layout. It follows document flow, behaves very predictably across all broswers and requires only the most minimal code to work with IE 6-7 (hack shown below).

1. **Whitespace associated with Inline-Block.**
	Inline-block elements preserve any space in the HTML between the opening and closing brackets, and are treated like words within a sentence, so it has a natural space between each `inline-block` element. As long as your web designs don't require seamless backgrounds on each individual element, then this is never a problem and will not need any correction.

	Example:

		<ul>
			<li>First</li>
			<li>Second</li>
			<li>Third</li>
		</ul>

	Since there is whitespace between the closing and opening `li` there will be a small space between the elements in the browser view. There are ways to fix this, but remember that whitespace issues can be easily solved by just rethinking the problem.

	Placing the background on the `ul` and not the `li`'s eliminates the need for seemless backgrounds. If you need a hover state, just use a background on the `:hover` or active `li`, but leave the other `li`'s without a background. Again, just rethink how you solve problems and 90% of them go away.

1. **Whitespace Hacks**

	**Remember: Don't hack the stylesheet** to fix this; you may win battles but never the war. Just alter the HTML using one of the suggestions below.

	1. Comment method: It's a great method for when you have just a few elements that require zero whitespace. If you are doing it for more than two or three elements, then use a different method. Make sure to leave a note as to why the comment is there.

			<body>
				<header>Header Stuff</header>
				<section>Body Stuff</section><!-- Remove whitespace
			 --><aside>Third</aside>
			</body>

	1. Don't leave whitespace: This is good for small, simple elements that need seamless backgrounds. Repeating small elements that don't have any internal HTML elements work well with this method. Again, make sure to comment why you are doing this.

			<ul class="nav">
				<!-- Leave all inline -->
				<li>Design</li><li>Development</li><li>Launch</li><li>Support</li>
			</ul>

	1. Misc Method: This works well if you have internal HTML elements within the `inline-block` element, like an anchor tag. Like the above, leave a note for others.

			<ul>
				<!-- Don't add space or line-break between li's -->
				<li>
					<a href="#">First</a>
				</li><li>
					<a href="#">Second</a>
				</li><li>
					<a href="#">Third</a>
				</li>
			</ul>

## Comments

### Commenting a Main Section

Use multi-line style separating unrelated sections of code and text should be ALL-CAPS with a double line-break afterwards. The next line of code should be nested after comment.

	/**********************************
	* THIS STARTS A NEW SECTION *
	***********************************/

	footer …

### Commenting Subsections

Default style should be a the single line comment above the code that is subject. Comments for subsections should be capitalized with a double line-break and indentation.

	/* This Is A Subsection */

	footer .someElement {
		color: #000;
	}

### Commenting for Communicating Intent

This comment should be single line and single line-break with no indentation.

	/* this is a comment */
	footer .someElement {
		color: #000;
	}

### End of Line Comments (Very Rarely Needed)

These are allowed if very short (~4 words)!

	footer .someElement {
		line-height: 1.5em; /* 20px */
	}

## Performance

1. GZip your CSS
1. Don't have Multiple CSS Files
1. Minify your CSS
1. Too many Redundant Declarations
1. Use a Reset Stylesheet
1. For More Details …

	See [Stubbornella's top five mistakes in CSS.](http://www.stubbornella.org/content/2010/07/01/top-5-mistakes-of-massive-css/)
