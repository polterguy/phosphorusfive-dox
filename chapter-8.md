# Introduction - The pan galactical gargle blaster

This introduction is to a large extent written for developers. It is an introduction to some of the features of P5, from an altitude of 10.000 feet. This introduction contains some *"advanced developer lingo"*. If you don't understand everything, relax and enjoy the parts you do. Rest assured, most developers don't understand everything here either.

**Warning**; Everything you thought you knew, is wrong!

To be honest with you, I find it difficult to explain P5 to developers, from an abstract point of view, without having them believe I am bullshitting them - Or at the very least exaggerating. I have therefor chosen to put the *"introduction"* to the book in the middle. This makes sure you've had some *"hands on experience"* with the system, before I explain it from an abstract point of view.

If you find this part to be *"rubbish"*, I would encourage you to start out with [chapter 1](chapter-1.md), and come back to this part later, as your brain have been aclimatized, to the feeling of having a lemon, wrapped around a brick, and having the said brick smashed through your brain, leaving nothing but a faint echo of your previous existence behind ... ;)

## Lambda, the last type you'll ever need

As you may have noticed at this point, there are no traditional *"OOP mechanisms"* in Hyperlambda. This is because OOP is largely rendered obsolete with P5. There are simply no reasons for any interfaces, because everything is a plugin anyway. There are no reasons to implement any abstract factories, to instantiate interfaces - Simply because you can supply a lambda object, with some expectations in regards to its input/output arguments, and in such a way, have the same Active Event, parametrized with two different lambda callbacks, do something completely different. Alternative, supply a simple string, which is being used as an Active Event reference, etc. There are no needs for polymorphism, when you can simply modify a string, and interchange your event invocation, with a completely different event, etc, etc, etc. I know this sounds absurd, but with P5, OOP is effectively *obsolete*! Active Events largely replaces all traditional OOP mechanisms, and creates better encapsulation and polymorphism, without types or cross component references.

To illustrate how far this idea goes, realize that you can easily, with a single line of code, create a web service endpoint, that allows for the invoker to *safely and securely* supply his own lambda, doing whatever he wants to do, on your server. Notice the emphasiz on *safely and securely*. This makes it possible for you, to create what I refer to as *"lambda web services"*, where the responsibilities between the client and the server are completely reversed, and the client supplies the code to be executed by the server. A web service endpoint, where the client gets to decide which code to execute on your server endpoint. This fact of course, literally *explodes* the possible number of permutations, for interaction between your server, and other people's apps, facilitating for a much richer, and more easily implemented heterogenous server park.

With P5, you can in fact invoke a file, with arguments, and return values back from the invocation of said file. Semantically, there are no differences between a static C# Active Event, a temporarily dynamically built lambda object, a file, some content from your database, or some piece of text, supplied over HTTP, within a web service context. Everything behaves like an Active Event in P5, if you want it to behave that way. With P5, you could evaluate the number *"42"* if you wish, and have it yield *"57"*.

## Monster scaling

The above ideas facilitates for what I like to refer to as *"monster scalability"*. Creating a heterogenous environment, consisting of millions of servers, each participating in some sub-portion of a humongous single task, executing a smaller fraction, of a single larger problem - Is literally *a walk in the park*. To illustrate this fact, realize that you can *"scale out"* your **[else]** invocations to a server in China, having your **[if]** events executed in USA, and aggregate the converged results down to China, running your database in Sibir, and your GUI in Denmark. Such a scenario wouldn't even be difficult to implement with P5.

And yes, even the keywords of the language are implemented as Active Events!

## Still, KISS

Still, creating code, making the system perform some task, is arguably *ridiculously simple*! One of my key design goals with the system, was to so significantly reduce the bar in regards to the creation of web apps, to such an extent, that even children, or your grandma for that matter, could easily learn how to create simple apps.

In one of its early versions, I created a fully fledged visual IDE, for creating code, declaratively, without the need of understanding the concept of code what so ever. Although, this was taken out, since I couldn't agree with myself how I wanted things to be - It still illustrates the point, which is that the *"art of programming"* in P5, is often so easy, that even your computer can do it.

## Metacognition on steroids

Meta, meta, meta, and then some more meta! The system is designed in such a way, that it can automate its own understanding, with meta capabilities, that superseeds anything else in existence that I am aware of.

If you want to know the number of nodes in your System42 folder, a script could probably be made in 20 minutes, to calculate this. If you are curious about the statistic relationship between how many times your system invokes **[insert-before]**, versus **[insert-after]**, another 20 minutes, and you'd have the answer. Interested in knowing how many invocations to **[load-file]** your System42 folder contains? An additional 20 minutes of work!

I find this to be difficult for developers to understand. However, *"Hyperlambda actually understands Hyperlambda"*! This means that the system itself, easily can be setup such, that it creates and maintains its own code. At least in theory.

If I download an application from the web for instance, I can use the *"Meta"* button in my CMS, and analyze the app, before as much as a single line of code from within it has been executed - Which allows me to among other things, look for suspicious pieces of code, to avoid executing malicious code on my server. This process is also easily automated.

If I wish to go one step further, I can even execute some code downloaded from somewhere, within a *"sandbox"*, by creating a **[whitelist]** of Active Events my downloaded code can legally execute. If some *"dangerous"* event is being raised by this code, it will throw an exception, and prevent further execution.

The metacognition capacity of P5, is quite staggering, and in the long run, probably the single feature that will please you the most. Arguably, P5 is an implementation of everything you expect from a kernel, to create your own Silicon Valley.

## Agile programs, a "feminine" programming language

If you've only created code in static programming languages previously, some of the agility you gain by switching to Hyperlambda, can probably be felt as quite staggering. Even for people who have developed in extremely dynamic programming languages, such as JavaScript and Lisp, Hyperlambda can still be experienced as *"surprisingly dynamic"*.

In Hyperlambda, as we've already vaguely touched upon, creating a piece of code, that dynamically changes, and *"morphes"* in accordance to its environment, is as common as declaring a class in an object oriented programming language. In general terms, it can be argued, that Hyperlambda has a much more *"vague"* border, between what a single construct's responsibilities are, and what its environment's responsibilities are. This facilitates for what I'd like to refer to as *"living code"*, where the code changes, and mutates, according to the expectations of its environment. Without any larger risks of executing malicious constructs. Meaning, your code's borders are less *"rigid"*, yet still, your code is still perfectly safe.

You will notice, as you start getting used to Hyperlambda, that a single lambda object, is often much more versatile, and can be used in much more different scenarios, if deviced carefully - Than that of which for instance a class from traditional OOP can. I often tend to refer to Hyperlambda as *"the woman of programming languages"*, since it feels like it has *"feminine qualities"*, to a much larger extent than most other programming languages does.

## Active Events

All things from the previously mentioned constructs, are built around a simple axiom; Active Events. This simple design pattern, is the facilitator of everything previously mentioned, and so easy to grasp, that an hour or two of reading, will easily make you understand all of its intrinsic details.

You can easily create an Active Event yourselves, either in C#, or in Hyperlambda. This allows you to extend the language, with your own domain specific keywords, implemented either in C# for efficiency, or in Hyperlambda for simplicity. In the next chapter, we will have a look at how to create a custom Active Event in Hyperlambda.