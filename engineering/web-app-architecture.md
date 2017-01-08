# Application Architecture Guidelines

## URL Design

The URL should reflect the resource being acted on and the state of the interaction. The **resource** is reflected in the path and the **state** is reflected in the parameters.

### RESTful

URLs are written in a RESTful manner. Strict adherence will be applied for API queries; semi-strict adherence will be for browser URLs as they lack the POST, PUT and DELETE methods. For more [information on REST, view this video](https://youtu.be/mZ8_QgJ5mbs). Any deviation from REST is reflected in URL parameters, *not in the path*.

### Routing

The route handler is step zero in initiating all things necessary for rendering the UI. The router maps the route to a set of function calls and initiates the flow of execution, so routes and route design is the most publicly visible parts of the API to your application.

Each route should describe the resource requested in the RESTful convention mentioned above. They act similarly to a controller, but not nearly as broad in responsibility. It's recommended that it has no, or the most minimal, middleware, and ends in a single function call that it can "fire and forget".

### Path, Parameter, Body and Verb

Resource is the location of information. This is declared by the URL’s path. State is non-persisted information, and should be within the URL’s parameters, if it needs to be re-rendered. Data is persisted information (saved to DB) and is passed in the body of requests, naturally.

- Path = Resource. E.g.: `/cards/123`
- Parameter = State. E.g.: `?data=expanded`
- Body = Data. E.g.: `{ expiryDate: "12/18" }`
- Verb = Action. E.g.: `POST`

So, the design should follow something like this:

```
{application}/{collection}/{resource}/{subresource}?{key}={state}
```

Some server rendered examples of this would be:

- `GET /money` – request and render full application
- `GET /money/cards` – request and render cards
- `GET /money/cards/new` – request and render the form resource for adding new card
- `GET /money/cards/CC-12345` – request and render card CC-12345
- `GET /money/cards/CC-12345/update` request and render the form resource for updating a card

- `POST /money/cards` – add a new card to collection and server render success
- `POST /money/cards/CC-12345` – update card within collection and server render success

Some AJAX, data only examples of this:

- `GET /api/money/cards` – request all cards, data only
- `GET /api/money/cards/CC-12345` – request card CC-12345, data only

- `POST /api/money/cards` – add a new card to collection and return data only
- `POST /api/money/cards/CC-12345` – update card within collection and return data only

## Universal Development (aka Isomorphism)

With a few exceptions, listed below, application code written should be executable in both server and client environments. This means we avoid duplicating logic for a server env and a client env. This also reduces the number of paths code execution can follow.

What this means is all your technologies, view library, utilities, state stores should all be designed for universality. Examples of this are React, Redux, Rx, Superagent, React-Router ...

Technologies that are not universal, and therefor should be avoided, are jQuery, Angular, Backbone ... basically anything that is dependent on a live DOM, `window` or `document` object. Or, the reverse, libraries that are dependent on server properties like `req`, `res` or `process`.

As mentioned above, there are some examples of when you *don't* want universal code. This is to ensure you have modules that allow you to do environment specific setup. Here are the best locations:

- Routing. Here you'll have server routing and client routing, though the actual route paths will be the same.
- Modules that interact with Service APIs. Since the client can never directly interact with Services, this is unavoidable.
- Initial data modeling will be server only. This is where you trim unnecessary data off the model before sending it to the client. This is critical for PII information and performance.
- UI handlers will obviously be client only
- Single top-level application entry point (e.g.: client.js and server.js) will be specific to the environment. This is where you do your client or server specific

## Data Management

### Modeling (Application) Layer Versus Data (Business) Layer

Modeling Layer is responsible for the preparation of rendering. This is sometimes called a "store". This layer should be executable within the client and server. It’s specific to the application context.

This Modeling Layer does most of the data modeling for rendering, and can act as the application's sole source of state. Immutability is exercised at this layer (read Immutability section).

The Data Layer, on the other hand, is involved with orchestrating service calls, providing a clean restful API to applications and abstracting common business logic. The Data Layer does not model data in any substantial way and acts more like a funnel taking multiple streams of data and funnels it into a single, actionable, data object.

This Data Layer is tech agnostic and should return plain old JavaScript objects with pure functions as an API. This ensures that as many consumers as possible can leverage these modules, and not require the adoption of any particular technology.

### Immutability

Within the Modeling layer, immutability provides a stable, predictable behavior to data/state management. The store (aka model) should always return a new object after any change.

That way, straight object comparison can be the way to detect “mutation”, rather than deep object comparison or relying on event listening. This severely decreases the need for imperative programming with lots of event binding.

### Single store (aka model)

Rather than having multiple stores spread throughout the application, decentralizing and complicating data/state management, making sharing data too difficult at scale, one large immutable store is to be used.

All Views have access to this single store and detect the need to re-render if previous !== current. This follows the pub-sub philosophy.

### Avoid Classical Programming Paradigms

Avoid the psuedo-class constructors, or the class keyword, and the Object Oriented approach. A more functional technique with factory functions and pure functional APIs will be preferred.

### Avoid the `this` keyword

`this` implies external mutable state. This is to be avoided. Methods should be passed in everything they need for operation in it's parameters.

## Complexity Management (Flux)

### Unidirectional Flow

Following the “Flux” philosophy, the flow of data and execution should be one way only. Starting with the URL and ending with rendering. Views should never initiate or push data upstream.

> route -> reqhandler -> transformer -> reducer -> store -> view

### The Asynchronous and Synchronous divide

An application should be divided into two parts: asnyc and sync. This helps determine where one does what in an application. Asynchronous code should happen in parallel and together. Once this part of the code is done, the rest of the application should be kept synchronous.

Example of async:

- Routing
- UI event handing
- Service requests
- File reads

Example of sync:

- Modeling and cache
- View rendering

### Centralization of State

As mentioned in the "single store" section, centralization of state into a single entity, like a Redux store reduces overhead and complexity. Once of the most complex issues in application development is the complex mental model of the affect of immutable and decentralized state.

## Core Tech Stack

### Kraken

For obvious reasons, but Kraken should always be used as the core of any web application. Do not try to reinvent the wheel. Utilize all the necessary authentication and authorization utilities provided out of the box.

### TypeScript

The biggest benefit is you now have static code analysis when "compiling" your code (technically, it transpiles). Bugs are so often not caught in JavaScript, or missed by syntactic linters, until you run the code and realize you misspelled a property. With TypeScript, that is dramatically reduced.

There are other great benefits to TypeScript, but I'll leave them here.

### Webpack

Webpack will be the build system of choice because of it’s universality, TypeScript support and module resolution. [Read the docs here](http://webpack.github.io/docs/what-is-webpack.html).

### Utility Libraries

Utility libraries are to be heavily leveraged and to be agnostic of technology. These should do one thing and do it well. Libraries should not force consumers to use a particular framework or other dependency.

### Libraries Over Frameworks

Frameworks are to be minimized as much as possible. Libraries that have a very-small focus should be leveraged as much as possible.

The application itself should be a framework of libraries, interchangeable legos that can be swapped out. The key is agile evolution, and allowing the most flexibility for change.