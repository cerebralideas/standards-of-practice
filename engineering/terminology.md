## Programming terms frequently used within organization

**functional programming** = use of functions rather than procedural programming to operate on data.

**implicit state** = state that lives in the environment, not within the function as input.

**pure function** = is a function that operates only on the data it receives from its parameters.

**stateless function** = is a function that does not hold any state after its execution.

**higher-order functions** = function that satisfies one or both of these things: function that returns a function or a function that receives a function as data/parameter.

**closure** = an internal function references a variable within it's parent function.

**IIFE** = Immediately Invoked Function Expression. E.g. (function () { /* body of function */ }());

**Lambda** = comes from Lambda Calculus. It's an anonymous function passed as data/as an argument.

**Primitives** = e.g. string, number, boolean, symbol, null, undefined. All of these are *passed by value*, meaning the variable onto which they are assigned are given a COPY of the value, not a reference to the original.

**Passed by value** = All of these are *passed by value*, meaning the variable onto which they are assigned are given a COPY of the value, not a reference to the original.

**Passed by reference** = Rather than providing a copy of the value, a reference pointer is passed to the variable being assigned, so that it references the original.

**Arrow functions** = functions written with as `() => {}` that do not have a `this` context, and therefor delegate the reference of `this` to its parent function. It also automatically returns its value if it has no function body.
