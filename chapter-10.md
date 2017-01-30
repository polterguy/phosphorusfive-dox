# Active Events preludium

In this chapter, we will start discussing the *"heart"* of P5; Active Events. So far, we have used this name many times during the book, but never formalized it, or explained it in any ways. After having read this chapter, you will have a 10.000 feet astronaut's overview of the answer to the question; *"Why Active Events"*.

## Definition

Active Events are first and foremost a *"design pattern"*. It is however a design pattern, that largely replaces most other design patterns in this world. Simply because, it solves the same problems as dozens of other design patterns do combined. Active Events also happens to solve these problems in a much more beautiful way, making sure you are able to create better cohesion in your software, while retaining a larger degree of encapsulation, and end up with increased means to apply polymorphism. Hence, arguably, it also largely becomes a replacement to OOP.

An Active Event is an alternative way of invoking functionality. It in such a way, becomes a replacement to what traditional programming refers to as *"functions"* and *"methods"*. Among its defining traits, is the fact that every Active Event, can accept the same set of arguments. In fact, they all have the same input signatures, which can be condensed down to *"a bunch of nodes"* or *"lambda"*. They also all return the exact same stuff, which again, you guessed it, is *"lambda"*.

This makes any Active Event, at least in theory, substitutable with any other Active Event. Hence, any Active Event, could in theory, replace any other Active Event. This is why Active Events facilitates for superior *"polymorphism mechanisms"*.

**Definition 0**; *"OOP"* is an acronym - Developers love acronyms - And it means *"Object Oriented Programming"*. Its main design, is based upon the assumption, that things in software, can be *"classified"*, and *"types"* can be created, that encapsulates everything related to some part of your application. Its foremost problem though, is that not everything can be *"classified"* into belonging to neither *"this"* nor *"that"*. Often things are a *"little bit of this"* and a *"little bit of that"* - Which results in that OOP does not resemble the real world, and hence often, creates more problems, than that which it solves. A whole subject of science, has over the years, ever since OOP's conception in the late 1960s, tried to solve these problems, by inventing elaborate schemes, such as multiple inheritance, and so on, attempting to solve these problems.

**Definition 1**; *"Polymorphism"* is the art of substituting one piece of functionality with another piece of functionality. Preferably such that any old functionality, is not broken as a consequence of applying the new functionality. Polymorphism is about having old code, invoke new functionality, without breaking.

**Definition 2**; *"Encapsulation"* is the art of being able to hide the internals of your components. This is crucial to be able to create large scale software systems, without forcing the software engineer to understand every minute detail of the system he or she is maintaining. It is arguably a prerequisite for creating systems, where more than one developer, is contributing to the system.

**Definition 3**; *"Cohesion"* is the art of making a piece of logic become *"self sufficient"*, and not dependent upon some other prerequisite, increasing its dependency. For instance, if I say; *"New years eve is booring. But the fireworks was nice this year"*. The last sentence cannot be isolatet, without loosing a crucial parts of its understanding. If you drop the first sentence, the reader will not know if you're talking about new years eve, or the 4th of July. Hence, the last sentence, is said to have *"bad cohesion"*.

All of the above, are concepts you would want to increasingly take advantage of, as you create more and more complex systems. A software system, lacking any of the above, is often referred to as being *"badly designed"*. A software architect, and developer, should strive to *"increase cohesion"*, *"apply encapsulation"*, and *"facilitate for polymorphism"*. If he does not, the results are often referred to as *"spaghettic code"*. Arguably, Hyperlambda entirely replaces the concept of *"spaghetti"*, substituting it with *"lasagne"*, largely making it impossible to create *"entangled systems"*.

Things in your software should preferably be *"substitutable with other things"* (polymorphism), *"hide their internals from the rest of the system"* (encapsulation) and *"create value on their own"* (cohesion). If they do, you have created reusable software, easily maintained and understood by others - And the system is said to have a *"solid and sound architecture and design"*.

Active Events, just so happens, to drastically increase all of the above parameters. Or at the very least, make it much easier for you, to accomplish the above. Which often comes as a suprise to software developers, used to other programming languages - Since they are often taught that the above concepts, can only be achieved using OOP. Hyperlambda *have no OOP mechanisms*. Hence, arguably, it *"refactors"* our best practices, and instigates the creation of an entirely new way of thinking about software architecture, and software design. While paradoxically not loosing anything, since you can easily combine it with OOP, and *"traditional"* programming.

One example of this (there exists hundreds), is how OOP for instance, during the creation of objects, forces you to decorate these objects. Already at this point, you have lost cohesion. Another example is how OOP often requires you to pass in an object to a method, which requires you to instantiate this other object, at which point you've lost all cohesion. A third example, is how a method in an OOP language has a signature, which means you've already lost the ability to substitute your method invocation, with most other methods in your application, and you have lost the ability to apply polymorphism.

By completely dropping the concept of OOP, we have very effectively *eliminated* a whole dimension of potential problems related to encapsulation, polymorphism, and cohesion.

The perfect object, according to the rules of encapsulation, has no public methods, properties, or fields. It cannot be instantiated, and hence cannot do anything wrong. In addition, it can be substituted with any other object in your system, facilitating for 100% perfect polymorphism. This just so happens to largely be the definition of a *"lambda object"*.

With that in mind, let's move on to the next chapter, where we will look at the internals of Active Events, and start creating some for ourselves.

[Chapter 11, Active Events](chapter-11.md)


