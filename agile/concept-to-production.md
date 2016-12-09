# Concept-to-Production Process

## Abstract

In the past we have had less than optimal UX making it to production, lack of iteration on complex features, chronic live bugs and, at times, frustration across teams. Many of these are symptoms of a process in need of standards and governance to ensure optimal efficiency and efficacy.

After observing our concept-to-production process, I’d like to suggest a procedural standard to how an idea goes from conception to reality. We have made some great strides in improving what we had 6 months ago, but I believe there’s still room for more improvement.

As applications become increasingly complex, it is more and more important that what we have a process that we all adhere to as functional units of product development teams. Many of our problems can be fixed if we dedicate ourselves to improvement.

This paper is going to be a suggestion for implementing an official Roadrunner’s procedural standard for remedying our concept-to-production ills.

## First, let’s define the problems

### Death by a thousands cuts

I am unsure of the cause of this issue, but our engineering team is frustrated by frequent occurrences of outdated designs, old content, lack of responsive mockups, high-fidelity mocks that confuse intention, loss of information through channels … All of this leads to many, small mistakes and setbacks that, in isolation are not that big of a deal, but add up to a unstable, unsustainable system.

### Who did what when?

When mistakes happen, we all need to ensure solid accounting of who, what, when to ensure that a similar mistake doesn’t happen again. We need a process that adds a layer of accountability to our stories and their progress to ensure that people are motivated to improve.

### Pixel perfection is toxic

There seems to be a common thread throughout that pixel perfection or absolute power of presentation is the goal of application design and engineering, but this is a myth that can quickly turn toxic. For a while, I have been trying pushing back concerning this ideal, and the times I’ve lost, the feature has become wrought with bugs and imperfections.

What’s most damaging about this is an engineer may push back on why some implementation is not a good idea, get overruled and be required to implement as specified to later be blamed when the feature is “buggy”.

A perfect example of this is the current idea from certain VPs that UI engineering lacks craftsmanship due to buggy features, and this is a very real opinion. Of course, there’s more at play here, but this pixel perfection ideal has a strong causal relationship here.

### High-fidelity designs and their consequences

This may seem counter intuitive, but all the research is pointing to the fact that if you want a substantive discussion on an idea, don’t provide a hi-fi mockup. It encourages a discussion on details and distracts from the bigger picture. When engineers look at a hi-fi concept, they inherently believe that that particular design is what’s intended to be implemented, so they pass the big picture and zero in on what they can and can’t do concerning what’s seen.

This can be mostly avoided by intentionally providing mockups that lack details and polish. They’ve found the by providing an actual pencil sketch, we tend to think about the bigger picture because we know that this is far from the final draft. Some prototyping applications intentionally use wiggly lines and handwritten typefaces to provide this context.

### Lack of responsive mockups

This is a source of much frustration within the engineering team. I’m afraid we continue to treat application design in a manner consistent with print design. We are always given a single mock, normally for the most optimal context and asked to implement this nice perfect design into the world of limitless variability. Engineers are left having to assume, wonder and guess how something is supposed to look at the half dozen other contexts that break the original mock.

### Poor iteration for complex features

In software, there is a common saying that “you’re never done”. That one should “release early and iterate often”. Unfortunately, this seems to not be the case for many of the complex features that we’ve released.

*In engineering, you have a choice: do you want quality or expediency? You can only choose one.*

From what I’ve witnessed, our upper management is demanding perfection in what we deliver, which is understandable. But, to deliver a feature at near perfection in a single release is, at best, a mythical idea. What it normally does is paralyze team members, encourage over-analysis and delay release doubling or tripling the time.

*What we are doing now is unsustainable because we are releasing new features faster than we can support them to their maturity.*

### Saying “no”

As with everyone, we like to please those that count on us to produce, but we also need to know how and when to say “no”. Not to be an obstructionist, but to ensure that we have the proper vetting of an implementation prior to development. Slowing down the process can help us catch errors or problems before they make it to production.

### Over-analysis of features from engineering

Engineers are, by nature, over-analyzers. We don’t like ambiguity and “gray-area” because such things are *impossible* to develop against. Because of this, we are known for being too critical of ideas and getting to “in the weeds” when the intention was to talk 10,000 foot view. This is frustrating from a design point-of-view because it kills creativity.

## Solutions

The suggested solution is to implement a standards process to how ideas are brought from concept to production.

### The process

0. Conceptualization, brainstorming, concepts sketched out, diagramming, flowcharting … all done by design and co. Whether design brings in engineering at this time is dependent on the complexity of the feature. The more complex, the more benefit from bringing in engineering sooner rather than later.
1. **Idea is brought to engineering for discussion (Grooming)**: Depending on what needs to be discussed at this stage, engineering should be presented with a low-fidelity (lo-fi) mock. Lo-fi is best if the idea is complex and needs discussion without the distraction of details. Lo-fi mocks can literally be pencil sketches or rough mocks with Comic Sans as the typeface and no color or style. In addition to this, engineering will prevent over-analyzation of ideas and stay non-critical as long as we are aware that this is a future looking idea, and not intended to be implemented within the next Sprint or so. The purpose: communicate the idea that this is **not final** and the goal is to discuss more general areas of implementation.
2. **Post grooming**: After #1 above, the result of the conversation is written down in the notes section of the upcoming story. Information is then disseminated to the proper team members.
3. **Sprint pre-planning**: Final mocks with responsive variants are produced, content is finalized and acceptance criteria is written. For stories to be considered for a sprint, they must meet the following criteria:
3.1. **The core design mock** provided should be a hi-fi mock that represents exactly what will be implemented and *also* matches the final content spec. The delta of the mock and the current app should only concern the feature and not have any “look-ahead” designs or elements that are not intended to be implemented. If the design does, it should be “censored out”. This should be the common *tablet landscape* design.
3.2. **Responsive variants** are included in lo-fi to represent how the feature responds to the variable environment. The required responsive, lo-fi mocks include *phone portrait, tablet portrait* and *full-width “common” laptop*.
3.3. **Content** is final and provided in plaintext format included in the story. This is to ensure that engineers can copy and paste text. Retyping text introduces possible errors. This content doc should be reflected in the design mocks provided. There should be no discrepancies.
3.4. **Summary, description and acceptance criteria** of story is complete.
3.5. **Sign off by accountable parties**. The PO ensures that the responsible designer(s) and content author(s) have signed-off on their work within the story, signifying that it is complete and up-to-date. *[Without the above, the story will not be accepted into the upcoming sprint, unless an exception is agreed upon by the team.]* If the design is not complete, but intended to be implemented, then the sign-off is accompanied with a note that the next version of the design will be provided in X days or will be implemented next sprint.
4. **Sprint planning**: In planning, discussions take place to ensure engineers, designers and product owners are in agreement and understanding of the story. One crucial aspect to this is that concerns from engineering are taken with the appropriate gravitas. *[There have been instances when concerns have been raised and met with much antagonism. In the past, this has resulted in bug ridden features that raise concerns of “engineering quality”. Any concerns that are overruled will be documented in story for record keeping.]*
4.1. **Complex features**: These are stories that are large or questionable; ~8+ story points. To ensure that we deliver features in a timely manner, we need to be able to release imperfect implementations. *This is law.* To ensure that we also produce a quality product, we need to set subsequent sprints to harden and bug fix. *This too is law.*
4.1.1. **Release early and iterate often**: We have the first part, but we are lacking the second. We release early, knowing that it isn’t perfect, but there are times where we don’t follow up enough to fix known issues as we are too busy trying to add new features.
4.1.2. **Sustainable system**: We are implementing new features faster than we can maintain the old.
4.1.3. **Solution**: We need to split all complex stories into iterations. First sprint: original delivery; second sprint: feature hardening; third sprint: correct all reported bugs.
That means new features are implemented slower so that we can concentrate on ensuring the ones we do have are properly built. *This is a good thing!*
4.2. **Simple features**: These are stories that can be implemented in one sprint and are normally 2 to 5 story points.
5. **Post planning**: The story becomes locked and immutable. Any modifications, comments or communication happen through the story’s discussion feature. *[If any changes occur after planning, those changes are added as discussion items for time-stamping, the original story should be left untouched. These changes are not guaranteed to be included in current sprint, and implementation of change is left to the discretion of the team.]*
6.  **Development**: During development, the engineer will communicate often with product and design to ensure the implementation is aligned with expectations. This is best done in an asynchronous manner through HipChat or Email. This will be in the form of screenshots, screen recordings and demos. Engineers will initiate this process as early as possible and with the appropriate mechanism for demonstration. The more complex the feature, the more the need for a remote VM instance for designers to interact with.
7. **Delivery**: All delivered features will abide by the definition of done, have the proper time for code reviewing, demonstration to product and testing.

## Suggested breakdown of sprint time

- ~60% for New Features
- ~20% for Last Sprint or Two’s Features (hardening and cleanup)
- ~20% for Tech Stories

By dedicating ourselves to always following up on last sprint’s stories, we can ensure that we don’t “let things slide” and ensure that visual defects are addressed up-front and bugs are fixed.