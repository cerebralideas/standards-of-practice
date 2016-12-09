# TypeScript

## What it is:

Simply put, TypeScript is a *superset* of ES6 JavaScript. What that means is anything that considered valid ES6/ES2015 is valid TypeScript*.

So, when you're writing TypeScript, you're writing JavaScript. The only difference is you now have the capability to add types to code.

```
// Absurdly simple example
var name: string = 'Justin';
```

The biggest benefit is you now have static code analysis when "compiling" your code (technically, it transpiles, hence the "'s). Bugs are so often not caught in JavaScript until you run the code and realize you misspelled a property. With TypeScript, that is dramatically reduced:

```
let user = {
	firstName: '',
	lastName: '',
	dob: ''
}
user.fistName = 'Justin'; // error: property fistName does not existing on Object user
```

> But, there's no type definition in that code!!!?

Good catch, I'll get to that in a second!

## What it is *not*:

TypeScript is not another language, even though they say it is in the TypeScript docs. It's no more another language than Babel or Flowtype.

It also doesn't compile to JavaScript; it is JavaScript. It transpiles, just like Babel. So, it determines what code should be downleveled to whatever target you choose. If it's ES5, then ES6 specific code will be downleveled to ES5 compliant code.

If your target is ES6, it’s pretty much untouched.

To prove my point, here's TypeScript:

```
/**
 * Index Utility Functions
 */
function addChoicetoModel(fiList, choiceId) {
	fiList.forEach(function addChoiceData(entry) {
		if (entry.id === choiceId) {
			entry.choicePreferred = true;
			return entry;
		}
	});
	return fiList;
}
```

And this is the JavaScript it outputs:

```
/**
 * Index Utility Functions
 */
function addChoicetoModel(fiList, choiceId) {
	fiList.forEach(function addChoiceData(entry) {
		if (entry.id === choiceId) {
			entry.choicePreferred = true;
			return entry;
		}
	});
	return fiList;
}
```

See a difference? That's because there isn't one!

What if we added types:

```
/**
 * Index Utility Functions
 */
function addChoicetoModel(fiList: [FiType], choiceId: string) {
	fiList.forEach(function addChoiceData(entry) {
		if (entry.id === choiceId) {
			entry.choicePreferred = true;
			return entry;
		}
	});
	return fiList;
}
```

And this is what it outputs:

```
/**
 * Index Utility Functions
 */
function addChoicetoModel(fiList, choiceId) {
	fiList.forEach(function addChoiceData(entry) {
		if (entry.id === choiceId) {
			entry.choicePreferred = true;
			return entry;
		}
	});
	return fiList;
}
```


Now, there are a few concepts that TypeScript has that JavaScript doesn't have, but it's the exception, not the rule. It also get's converted into idiomatic JavaScript, so nothing too weird to worry about.

## So, then what is it really?

Good question, from my perspective, it’s a typed, JavaScript, *development environment*. Many developers use IDEs to help tie all the scattered code together in a way that provides a bit more ergonomics to your software development.

With the popular IDEs you get live linting, autocomplete/suggestion functionality, integrating servers and terminals ... but, there's usually something missing, a big gap.

These IDEs normally don’t give you much insight to *your* code, *especially* across modules or libraries. They just help with the native methods of the language or that file’s local code.

This is the gap that TypeScript fills. It connects all your code into an intelligent ecosystem that checks the code your writing against all the known points of the ecosystem.

[show example with moneynodeweb in Webstorm]

On top of that, it provides static code analysis, exposing many of the most common human errors that cause bugs.

```
// Type assignment
function addTwoNumbers(a: number, b: number): number {
	return a + b;
}
addTwoNumbers(1); // Compile error
addTwoNumbers('1', 2); // Compile error

// Interface definition
interface User {
	id: string,
	firstName: string,
	lastName: string,
	age?: number
}
let user: User = getUser(req);
let name = user.first_name + user.last_name; // Compile error
user.birthdate = input.value; // Compile error
```

## When should I use TypeScript?

We use TypeScript for everything we develop, but we had the advantage of writing everything from scratch. The best way to start using TypeScript is to write or convert small modules to it. That way, the footprint required to develop is small and focused, and the learning curve is not quite so daunting.

The more of these questions you answer yes to, the more you should use TypeScript:

- is this an NPM module, framework or library?
- is this project large (LoC)
- is it composed of many independent modules?
- will this product be used by developers outside of your team?
- is the proper operation of this code critical?
- is documentation of your APIs important?
- will there be a lot of developers contributing to the codebase?
- are there possibly any users of this module that leverage TypeScript?

Notice that questions allude to above is basically “enterprise” software development.

## When should I not use TypeScript

Large, existing applications are very hard to convert to TypeScript. The biggest challenge is when the project uses a lot of internal/private frameworks, libraries or modules that do not have existing TypeScript definitions, and or have non-standard APIs.

There are escape hatches that can be used, but because TypeScript is more of a typed development environment, it doesn't like not being able to identify the structure of the code it’s supposed to analyze and transpile.

[show examples of the growing number of TypeScript definitions in commonweb-setup]

## Summary

### Advantages:

- type safety
- interfaces
- static code analysis (immediate feedback)
- powerful autocomplete with type hinting
- ES6
- fewer build tools
- forces developers to *THINK* about their code

### Disadvantages:

- large, existing codebases are hard to convert
- third-party code needs to be defined for any real benefit
- defining non-standard module APIs can be really hard to get right
- learning curve
- some compile errors can be a bit hard to interpret





