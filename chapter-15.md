# FYI, P5 is fork friendly, and free-fusable

Linguistics are funny, when you start dissecting them from a poetic point of phew ;)

One interesting feature of the database layer we created in the previous chapter, is that it is *100% generic*. Which means that we can *extract* its core parts, and create a 100% perfectly encapsulatet re-usable set of components, which helps us accommodate for future change - *Without* breaking the rules of *"YAGNI"*.

**Definition**; YAGNI means *"You Ain't Gonna Need It"*, and implies you should never implement something you'll probably never need. This important design rule, contradicts the core design principles of OOP, which is that you should accommodate for future change - And hence often becomes a contradiction, and an oxymoron by itself, to other important design *"rules"*. Hence, the art of balancing *"YAGNI"* with the design principles necessary for us to implement, such that we can accommodate for future change - Often times seems like an impossible task in traditional OOP-based programming languages.

I often times refer to this oxymoron's insanity, by stating how according to the rules of *"SOLID programming"* (Google it) - The perfect type has no public interface, and cannot be instantiated. Which of course translates into that the perfect class is the one that *doesn't exist*.

## How Hyperlambda solves this balance

TODO ...
