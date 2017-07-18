# Design Principles for CXP-Web Platform

## 1. Universal Rendering

Both server and client rendering/route handling. No client-only rendering and/or routing. This ensure progressive enhancement for applications.

## 2. Widgets are read-only UI components

A widget is a read-only, informational UI component. Any extended functionality will still be read-only, i.e. open an overpanel for additional information. No flows contained within a widget.

## 3. Embrace "sharable flows"

Flows like change a primary email address, link a bank, send money ... should all happen within the respective application that hosts the functionality:

- Changing an email address happens in Settings, a fully autonomous applications managed by that domain team.
- Link a bank happens in Wallet
- Send money happens in P2P

All of these flows will eventually be exclusive routes for rendering our flow specific functional. These will leverage the commonweb-flow library allowing for redirection both into and our of the flow without any disruption in UX.

## 4. Performance for under-powered, low-bandwidth contexts

Due to company priority on under-developed or developing nations and providing services to these regions, delegation of resources have to be server-side as much as possible.

Memory usage and expansion of browser capabilities should be minimized as much as possible.

## 5. Technology agnosticism

## 6. Libraries not frameworks

## 7. Composability over singular solutions

## 8. API over environments

## 9. Functional programming design

## 10. Unidirectionality and strong separation of concerns

Using somewhat of a Flux-like design, components of the application should execute in a unidirectional manner with no two-way binding or multi-directional dependencies.

We also embrace a strong separation of concerns be separating all async needs in our app from sync needs.

Avoiding MVC like architectures is a great way to embrace this principle.

## 11. No classical architecture or paradigms

Avoidance of `this` and vertical inheritance is paramount to building a predictable, reliable application to scale. This also relates strongly to the Functional design to our codebase.

## 12. Testability is absolutely key to success

Being able to effortlessly recreate application state for testing and being able to unit test all aspects of the application without servers, mock environments is key to producing quality applications.

## 13. TypeScript is king
