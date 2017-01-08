# Reactive Programming Guidelines with Rx

## Why Rx?

Rx, and its reactive programming model, are extremely useful in applications that have a multitude of asynchronous calls that lead to data "modeling" and have to be orchestrated in a particular order or operation. Rx is also very composible, chain'able, encourages immutability and helps in normalizing all of the different variations of asynchronous needs in programming. It has build in error handling and a sophisticated API that can be very powerful.

## Terminology

- **Observable**: notice the big "O". This is the main object off of Rx that observes or listens to particular events. This object has creation methods, operational methods and finally a subscribe method. Don't confuse this with the rarely use "observable" with the small "o".
- **creation method**: the method of an Observable that starts the sequence by wrapping around a static data type or a dynamic, event based entity to listen for emitted values. [List of creation methods.](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/gettingstarted/which-static.md)
- **observable**: a parameter (of type object) that is passed to a few of the creation methods that are the internal hooks for "emitting" values.
- **sequence**: one or more operations with the data produced by the Observable's event completion. The are normally chained operations using array-like methods: e.g. reduce, map, concat ...
- **instance**: the single value that is emitted from the observed entity. It's normally the value that's provided to you within your sequence methods.
- **instance method**: (also called a *sequence method*) one of the array-like methods that makes up a sequence. [List of instance methods.](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/gettingstarted/which-instance.md)
- **array-like**: it's worth noting that the sequence's data is not technically an array, it's an iterable, and the array-like methods are not the native JS Array methods. There are slight differences, so use Rx's documentation for clarity.
- **iterable**: an array-like data object that is a Rx specific wrapper around the raw data
- **transform**: rather than thinking in terms of "model" and "modeling", we like to use the term transform. This describes what's happening to the data as it flows its sequence.
- **transformer**: the nickname for a module that takes a request for data as input, makes a call to request data, transforms the data by way of its sequence and then hands this data to its caller.
- **emit**: since the reactive programming model is based on events, the word "emit" will be used once in a while. Emit will refer to when an event is "fired" and a value is passed to the Observable sequence.
- **subscribe**: this is the method you call to execute a sequence. Many Observables will be inert (aka "cold") and have to be executed to be useful. Most of the time, the Observable is called when the execution reaches the `.subscribe` method of the Observable.


## Observable creation methods

These are the methods that are used to initially create an Observable. There's [a great Rx page that lists all of Rx's creation methods by use](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/gettingstarted/which-static.md), which is really handy you're getting familiar with all of them. But, it's good to understand that nearly all of them are [an abstraction of the `.create` method](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/operators/create.md).

The basics of the create method are fairly straightforward:

The `.create` needs a function that's passed into it as a parameter. This function will receive a single parameter when it's called, and that parameter is the `observable` with a small "o". This small "o", observable as three methods on it:

- `onNext`: this is called upon each value that you want to "emit" to the Observable sequence. You pass the value as the argument of this function call.
- `onError`: this is called when you want to end the sequence and roughly "throw" an error. The error value, if one exists, is passed as the functions argument.
- `onComplete`: this is called when you have no more values to pass and you want to complete the sequence. Although data can be passed in this function, it is not a typical practice.

There are times when you may want to write custom logic for your creator, but often times, the abstractions work well enough. Deciding on these methods can be difficult at times (and a bit overwhelming). But, it's important to know that all of these methods are basically a `.create` method under the covers.

### Deciding on a creation method

First, you need to decide what the source type is you are wanting to "observe" for emitted values: static or dynamic. One of the most powerful things about Rx is that these two things are equivalent (don't pay too close to the details, just notice how widely different the are):

```js
// static creation from a basic, static array
var static$ = Rx.Observable.from([1, 2]);

// dynamic creation from two separate async creation methods
var dynamic$ = Rx.Observable.merge(
	Rx.Observable.fromCallback(function (cb) { cb(1); })(),
	Rx.Observable.timer(1000).map(function () { return 2; })
)
```

When the two different creation methods are subscribed to (say assigned them to a `var` `sequence`, the result is the same:

```js
static$.subscribe(
	function next(value) { console.log(value); },
	function error(err) { console.log(err); }
	function complete() { console.log('All done.'); }
);
// console
1
2
All done.

dynamic$.subscribe(
	function next(value) { console.log(value); },
	function error(err) { console.log(err); }
	function complete() { console.log('All done.'); }
);
// console
1
2
All done.
```

Once you've wrapped an entity in an Observable, it's behavior is the same whether it's a single, static, synchronous value, or many, dynamic asynchronous values over time, the behavior and predictability is the same. It normalizing any data type or behavior through Rx's API.

To communicate a particular variable is an observable, we append a `$` to its name to denote "sequence". You can see this used in the above example. That's how a developer knows that this particular variable has a predictable API and behavior.

### `fromNodeCallback` or `fromCallback`?

This can be a tricky thing that is many times can be a "gotcha". `fromNodeCallback` can seem like the perfect creation method for converting a node-style callback (error first parameter) API into a predictable Observable, and it is, unless you deal with services that, at times, use error HTTP codes for non-error statuses.

An example of a error code for a non-error status: 404 for a collection query that resulted in no entities. Say, you call a get banks endpoint and the result of the query is no banks (or `[]`). This is not an actual error, so you wouldn't want the following execution to follow your code's error path. You would just want to continue on with nothing more than a successful call that resulted in an empty array.

If you use `fromNodeCallback`, you will get false positives on errors if there is ever a chance the `err` object is truthy when the status is not an actual error. If you can guarantee that a truthy `err` is always a true error, then your golden. But, if you can't, use `fromCallback` instead.

The only problem with `fromCallback` is it is up to you to properly handle errors. Rx will ignore the `err` object.

### Values over time or all values at once?

This is another decision to make in some instances. The difference is would you like the `next` function to be called when each value is emitted and finished the sequence, or would you like `next` function called when ALL of the values have been emitted and the sequence has completed?

A good example is the difference between `.merge` and `.forkJoin`:

```js
Rx.Observable.merge(
	Rx.Observable.timer(5000).map(function () { return 1; }),
	Rx.Observable.timer(3000).map(function () { return 2; }),
	Rx.Observable.timer(1000).map(function () { return 3; })
).subscribe(
	function next(value) { console.log(value); },
	function error(err) { console.log(err); },
	function completed() { console.log('All done.'); }
);

// Console
3
2
1
All done.
```

```js
Rx.Observable.forkJoin(
	Rx.Observable.timer(5000).map(function () { return 1; }),
	Rx.Observable.timer(3000).map(function () { return 2; }),
	Rx.Observable.timer(1000).map(function () { return 3; })
).subscribe(
	function next(value) { console.log(value); },
	function error(err) { console.log(err); },
	function completed() { console.log('All done.'); }
);

// Console
[1, 2, 3]
All done.
```

Notice how the forkJoin returns all values in an array at once and within the same order as was provided in the method's arguments, but the merge returns the values over time when they are emitted? This "all values at once" is pretty useful when you have multiple data queries going on at once in a non-deterministic order and you don't want to worry about building the final object correctly.

There are also instance methods that provide the same "all values when complete", like `concat`, `reduce` and `toArray`, but we'll try to get to that in the instance method section.

## Observable instance methods

Most observable instance methods act just like their native Array counterparts. These you can use without much cognitive overhead. But, there are some that will leave you scratching your head.

The biggest principle to follow when writing logic for your sequences is to ensure you're not writing side-effects in your instance methods. This ensures you're writing in a less "mutable" fashion and following the "reactive" way. This means your instance methods should be pure, stateless functions as much as possible.

Chaining these instance methods is recommended and just pass values along the chain, building it as it falls through. Just ensure you're not operating on data that is referenced outside of the values passed within the sequence.

### Operating on static versus dynamic data

Most of the time, your sequence starts with a async request and then your sequence just transforms the data as it falls through the sequence. But, there are times when your sequence needs to make additional async requests within an existing sequence.

Let's start with static operations:

```js
// `getIds` is a callback function that makes an async request
Rx.Observable.fromCallback(getIds)
	.map(function (value) {
		// instance logic
	}).subscribe(
		function next(value) { console.log(value); },
		function error(err) { console.log(err); }
	);

// Console
[ 88587, 23436 ]
```

Now, let's say that the original `asyncFunc` returns an array of IDs that then need to be converted into additional async requests for the full details according to that ID.

```js
// `getIds`: async callback function
Rx.Observable.fromCallback(getIds)
	.concatMap(function (id) {
		// `getDetails`: async callback function
		return Rx.Observable.fromCallback(getDetails)(id)
			.map(function (data) {
				// instance logic
			});
	}).subscribe(
		function next(value) { console.log(value); },
		function error(err) { console.log(err); }
	);

// Console
[ { id: 88587, user: "Barbara" }, { id: 23436, user: "Jim" } ]
```

Here, we have one async call that leads to multiple async calls, and as we iterate through the original array, we need to convert  each static ID to an async call that returns more data related to each ID.

#### `flatMap` versus `concatMap`

If you're wondering what the difference is between `concatMap` and `flatMap`. `concatMap` guarantees the order of the values according to the original source, and `flatMap` just returns values in the order of completion.

### Dealing with side-effects

If you want to do some logging on values as the fall through a sequence or some other "side-effect" like action, then use the `do` operator. It works almost exactly like the `subscribe` method without affecting the values or sequence at all.

### Error handling

Within any instance method, if you encounter something that you need to halt execution and place the code in the error path, you can `throw` an `Error`. Rx listens for all thrown errors and uncaught exceptions and, as long as the `subscribe` as the `error` function, executes the `error` function.

If your instance method expects another Observable returned, then you can use `Rx.Observable.throw(err)`, which will have the same affect.

### Ending a sequence

When you are done transforming your data, make sure to convert it to the appropriate data type that your consumers would expect. E.g.: a particular Observable is used for requesting a single instance, have your final sequence method convert the data to an object. Or, if you intend to return a primitive value, reduce to that primitive value.

If you don't covert the data type, technically, the type will always end up being an array. But, often times, an array is not appropriate. This is not always obvious when you are subscribing to a single Observable, because the `next` function always returns the value itself. And, if your request results in a single value, you'll magically have that one value.

This is not necessarily wrong or bad, but it can inhibit composition. If you compose this Observable with other Observables, then all your single instances will be wrapped with an array. Here's an example:

```js
Rx.Observable.forkJoin(
	asyncCallOne$,
	asyncCallTwo$
).subscribe(
	function next(value) { console.log(value); },
	function error(err) { console.log(err); }
);

// Console
[
	[ { id: 97634, name: "Barbara" } ],
	[ { id: 84597, name: "Jim" } ]
]
```

That's not really what you want, most of the time. What you want is an array of the objects themselves without the unnecessary wrapping array. So, you have your final sequence method reduce the value to the object type:

```js
Rx.Observable.forkJoin(
	asyncCallReduceOne$,
	asyncCallReduceTwo$
).subscribe(
	function next(value) { console.log(value); },
	function error(err) { console.log(err); }
);

// Console
[
	{ id: 97634, name: "Barbara" },
	{ id: 84597, name: "Jim" }
]
```

Ahh, much better!

## Keeping sequences flat and simple

In most sequences you create, you want to keep them as flat and shallow as possible and have each method doing one thing, and one thing well. Don't have a single map function doing a ton of logic transforming the data.

As long as your iterable isn't hundreds and hundreds of instances long, doing multiple loops over the data isn't going to affect performance. If each method is simple and "to the point", then it's easier to maintain, read and also move around and compose.

### `fromCallback`/`fromNodeCallback` and collection requests

It's worth noting that in times when you have a collection request, and you need to do operations on each instance in the collection, a simple `fromCallback` or `fromNodeCallback` is not sufficient. That would be because the collection is being emitted as a single value:

```js
// `getCollection`: async callback function
Rx.Observable.fromCallback(getCollection)
	.map(function (data) {
		// `data` at this point is the whole collection:
		// [ 1, 2, 3, 4 ]
		// So, to operate on each instance, you have to have
		// another `map` within this `map` ...
		// not good :(
	});
```

To fix this, the core `.create` creation method to the rescue!!!

```js
// `getCollection`: async callback function
Rx.Observable.create(function (observable) {
		function cb(err, collection) {
			// Check for error
			if (err) {
				// Call error path
				observable.onError(err);
			} else {
				// iterate over collection
				collection.forEach(function (instance) {
					// emitting each instance individually
					observable.onNext(instance);
				});
			}
			observable.onCompleted();
		}
		// Call the async function
		getCollection(cb)
	).map(function (data) {
		// `data` now represents each instance
		// We no longer need to nest `map` functions ...
		// simple and flat :)
	});
```

This is obviously a bit more code to deal with, but it keeps your observables flat, and there's no reason why we can't create a reusable "collection create" method as an abstraction like any other method. So, rather than `fromNodeCallback`, we could call it, `fromCollectionCallback` ... boom!








