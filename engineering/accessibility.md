# Accessibility Baseline

*There are basically two ways a screen reader interacts with a web page. 1) the "action mode" navigated by the tab key; 2) the other is the "reader mode" which is navigated by the arrow keys (opt + alt + arrow key for VoiceOver, or VO for short) and uses headers or landmarks to jump around. Both of these states need to be understood and supported by the implementing engineer. The question is to what point to we implement, test and manage the support for these two modes*.

## tl;dr

Here are the things we will support by default on all stories:

1. Using the right interactive elements: `<a>` versus `<button>`. Don’t confuse styling with semantics; just because it looks like a link doesn’t mean it should have an `<a>` element. This is basic support for action mode.

2. Using the right HTML semantics: `<li>` versus `<p>` versus `<h2>`. Again, don’t confuse styling with semantics. Only use `<div>` and `<span>` if the element is *only* used for styling or layout. This is basic support for reader mode.

3. Managing focus both for static features and dynamic features in and out of modes. This is moderate support for action mode and leads to better support for reading mode.

The advanced support for accessibility that will not be default on all stories, but should be called out on larger stories that will require this kind of support is …

*Managing the reading of content and the ARIA state for more complex features. A good example of this is the use of `aria-label`, `aria-controls`, `aria-describedby`, `aria-expanded`* …

## Action Mode Support

The most basic level of support is to use the correct elements for interactivity. Here’s a list of the basic support for “action mode”:

1. Anchor tag: `<a>`. This tag is conventionally used for the purpose of routing the user to a different set of information. That means that if a `<a>` is used, it should have a meaningful href attribute. If it does not have a meaningful href, we should use the `<button>` element (see below). If an `<a>` is needed, but the result of it is not *technically* navigating to a new page, then a role of button should be applied (e.g. `role=“button”`). This, like the `<button>` tag, communicates to the screen reader user that they are not leaving the page, but interacting with a particular part of the page.

2. Button tag: `<button>`. This tag usually denotes interacting with elements existing on the page. It has no href attribute, so it does not result in any “navigation”. This element also provides more options for interaction, like the spacebar, as opposed to an anchor tag.

3. If inputs exist on the page, they should be wrapped in a `<form>` tag and end with a submit button (e.g. `<button type=“submit”>`. Larger forms should utilize the `<fieldset>` and `<legend>` elements to logically group form elements and label them.

4. Every `<input>` and `<textareas>` should always have a accompanying `<label>`, even if they are not visually presented to the user. *A placeholder attribute is not a replacement for a label*. Labels are paired with their inputs with the `for` attribute; this is done with the `<label for=“myId”>My label</label><input id=“myId”>`.

5. All forms should have feedback when errors exist. To ensure those that use screen readers are made aware of the error that is, at times, only visually added to the page, the use of aria-live is required to force the readout of the error message. E.g.:

	```html
	<div class="alert" aria-live="assertive" role="alert">
		There was an error with your form
	</div>
	```
6. When form inputs have inline help or error text, the `aria-describedby` and `aria-invalid` attributes should be used so the informative text is read aloud to the user when they focus on the input:

	```html
	<input type="text" aria-invalid="true" aria-describedby="inline-error">
	<div id="inline-error">Please check your account number and try again.</div>
	```

7. Ensure HTML order is logical. We can always change the order visually while preserving the tabbing order for keyboard users.

### Advanced

More advanced support is utilizing ARIA attributes for content and state management for interactive elements on the page. For example, the Engagement Module uses `aria-controls` to signify that a particular element controls another element on the page, `aria-expanded` denotes that a particular element has been opened or expanded, and `role="alertdialog"` is used throughout to ensure the user is aware of the state and intent of the elements.

If you are injecting dynamic elements into the page, like a modal or "lightbox", then managing focus is critical. To do this, make sure you programmatically focus on the newly created modal. To do this, you need to use the `tabindex="-1"` to ensure you can programmatically focus the `div` that you're likely using. Lastly, ensure that you use the `aria-labelledby` and use the id of the header of the modal.

When you close the modal, ensure you place focus back to the element that first triggered the modal. If this isn't possible, drop the focus on a portion of the application that relates closely to the previous action

## Reading Mode Support

This boils down to good ol’ HTML semantics. I won’t go too much into this, other than saying, “don’t confuse styling with semantics!” Make sure you pick the right element for the job. Just like it’s important to pick the `<a>` or `<button>` element depending on intent, the same is for picking `<div>` or `<p>`. Use as few elements as possible and use the most semantically valid ones.

If an element is purely for no other reason other than style or layout control, and is not describing content, then a `<div>` is used if it’s block level and `<span>` if it’s inline should be used. *Note that inline elements should normally not contain block-level elements.*

Another important aspect to support reading and exploratory actions with screen readers is to have appropriate header hierarchy, and structural elements and aria role attributes to create the appropriate "landmarks" to the page. Here are a few rules:

1. Only one h1 per document
2. h2 and h3 elements should reflect the hierarchy of the page and mark the relevant and important sections of the page/app.
3. Structural element like `<navigation>`, `<main>`, `<footer>`, `<aside>`, `<banner>` should be used throughout the application.
4. Aria roles can be used as well to help if the native, semantic element isn't available or possible. The `role=""` attribute can have the values of search, banner, navigation, alert, alertdialog, footer ...

### Advanced

More advanced support is using ARIA’s labeledby and describedby attributes to help add contextual meaning to elements on the page. Examples are `aria-labeledby` and `aria-describedby`. This allow the dev to provide the meaning of an element by referencing another element on the page. This is used in the activity list.

## Conclusion

The best way to support accessibility is to engineer the UI with good semantics, clear intent and concise communication. The end result is not to have just a good looking interface, but to also have well engineered code supporting the UI. Sight-challenged users depend heavily on the underlying implementations much more than sighted users. Bad engineering equals poor accessible experiences.