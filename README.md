# Phosphorus Five, the guide

Welcome to the book about [Phosphorus Five](https://github.com/polterguy/phosphorusfive). Phosphorus Five, also referred to as P5 in this guide, is a lot of different things. It is a simple design pattern, it is an Ajax library, it is a programming language, and it is a framework. Some would also argue that it is a web operating system. What you choose to refer to it as, is really quite irrelevant. The point is that it solves your problems, particularly the ones you’re having, as you try to create rich and interactive web apps. This book aims at being your _“one stop guide”_, as you start out with P5. A beginner’s introduction. Starting out at the _“for dummies level”_, and hopefully moving you onwards to the expert level.

## The objectives of the book

During this book, you will learn everything you need to know, to create your own contact database, to keep track of your friends' emails, phone numbers, etc. My aim is to bring you up to this knowledge in P5, in less than a day. That way, the book becomes very practical, and hands on, progressing rapidly, and you can feel that you have done something constructive fast. Then as we proceed, we will revisit this application, slowly making it better, until it becomes a generalized app, and solves all of your CRUD needs.

Every construct we go through, will have a practical application for you. The book is a hands on guide, intended to ignite your own creative processes. As we create these practical solutions, we will also discuss the software architecture theory behind our choices. After reading this book, you can consider yourself a senior software architect, easily capable of discussing software architecture, with some of the best architects on the planet.

## Prerequisites for reading

This book assumes some basic knowledge about HTML, but does not require you to know JavaScript and/or C# from before. However, some basic knowledge of JavaScript and C#, might be beneficial, since we will dive into these technologies in some of the chapters. You can still perfectly take advantage of it, even if you have never created as much as a single line of code in neither JavaScript, C#, nor any other programming languages. This book does not assume you're a programmer from before, although it sometimes helps having done some programming earlier. Some basic CSS knowledge, is also beneficial, however not required.

## Technologies visited

The main programming language in P5 is called *"Hyperlambda"*, and will be the programming language used for almost all of our examples. Even if you have no interest in learning Hyperlambda, the book will still be valuable for you, since it is also a guide to software architecture theory in general. In addition, Hyperlambda is easily extended through C#, so a C# developer will also benefit from reading this book.

In addition to this, we will also touch upon HTML, CSS, and some general programming theory throughout this book. However, most of the book, is dedicated to hands on, practical examples, of actual useful applications, you could probably benefit from having access to, regardless of whether or not you read the book or not.

## A guide to the guide

The book's convention, is created carefully to allow you to understand what is being described. First of all, any property or attribute from Hyperlambda is referenced like **[this]**, where *"this"* assumes a node's name. This convention is used whenever a node is referenced inline in the text. Emphasized and important points, are written like *this*.

Inline code is written like `this` and multiple lines of code is written like the following illustrates.

```
howdy-world
  this-is:A piece of Hyperlambda code!
```

### How to read the book

Advanced topics, which are not necessary to understand, are explicitly marked as such. You will often find a link close to where a topic has been marked as advanced, allowing you to easily skip the advanced parts. Often the advanced topics of P5, is given inline to preserve context. This means, that advanced topics, are equally easily found in the beginning of the book, as they are found at the end of the book.

You can easily skip these advanced topics in your first read, for later to refer to them as the need surfaces. This ensures that the book is not only a beginner's guide, but also of use for the *"Shaolin Ninja P5 master developer"*.

In general, there are 3 different ways of reading this book. There is the *"beginner's guide"*, which doesn't require you do read any of the advanced chapters. This allows you to rapidly get up to speed in your understanding of P5 and software architecture design principles. This type of reading can probably be done in a day or two, following simple copy and paste examples. These examples are intended to demonstrate some idea, while also incorporating some important software architecture design principle. This allows you to gain terrain very rapidly, as you read the book, while also understanding the underlaying theory for our choices.

Then there's the *"master's read through"*, which is intended for a second reading of the book. This reading will give you a more detailed vision of both P5, and software architecture design principles in general. This way of reading the book expects you to read the *"advanced topics"*.

Then, finally, there's the *"reference"* version, allowing you to use the book as a reference guide, when you need to repeat your knowledge of some particular subject, or look up some concept in your daily work as a software developer and architect.

If this is your first encounter with P5, I would encourage you to skip all the *"advanced chapters"*, to get you up to speed as fast as possible. This type of reading actually expects you to start out your reading at [chapter 2](chapter-2.md). This *"track"*, is created to rapidly make you gain ground, while staying in the flow, with highly applicable and useful examples, intended to leave you with something real and tangible - In addition to teaching you some very specific and useful concepts.

Sometimes, the book will also include links to YouTube videos, which you can watch, to further increase your understanding of some concept. This are created as additions to the chapters, and often we analyze the code we looked at in the chapters where these videos are included.

### Introduction to the introduction

This might sound weird, but the book's introduction can actually be found in [chapter 8](chapter-8.md). My reasoning for doing this, is that I want you to have some hands on experience with P5, before we introduce it from a conceptual point of view. I have therefor chosen to wait with the introduction of the book, until you're almost midway through the book.

### Downloading the book

Periodically, I will create a download of the book, which you can read locally. This will be in the formats offered by GitHub, such as .zip and .tar.gz. These downloads are the *"raw source"* of the book, which is in Markdown format. It could probably be beneficial for you to use a Markdown viewer, to read the book. I personally use *"MacDown"* for writing the book. Another great viewer for Windows is [Markdown Monster](https://markdownmonster.west-wind.com/).

This way of distributing the book, allows you to create inline comments as you read it, providing answers for exersizes, and comments, etc. It also allows you to easily create patches and additions to the book. In addition, it makes it easy for you to document your own systems as *additions* to this book, having a great foundation for the documentation of your own systems. Which means that as you start out creating value on top of P5, you can start documenting your system, from the point where the book ends. Hence, there might, and should, exist a *"gazillion"* versions of this book out there, where every version of the book, is equally unique as the system it is describing.

My email address is thomas@gaiasoul.com, and you can find the book's main source at [GitHub](https://github.com/polterguy/phosphorusfive-dox), which is the place where I prefer you to submit feedback about the book, if you have any.

## Chapters

- [Chapter 1, Ajax - Advanced topic](chapter-1.md)
- [Chapter 2, Hello world](chapter-2.md)
- [Chapter 3, Ajax widgets - Advanced topic](chapter-3.md)
- [Chapter 4, Your first Ajax form](chapter-4.md)
- [Chapter 5, Lambda expressions - Advanced topic](chapter-5.md)
- [Chapter 6, Changing your tree](chapter-6.md)
- [Chapter 7, Your first real application](chapter-7.md)
- [Chapter 8, Introduction, The pan galactical gargle blaster](chapter-8.md)
- [Chapter 9, The bug](chapter-9.md)
- [Chapter 10, Active Events preludium](chapter-10.md)
- [Chapter 11, Active Events](chapter-11.md)
- [Chapter 12, Eval is not (necessarily) evil](chapter-12.md)
- [Chapter 13, Hyperlambda leads to Hyperhumble](chapter-13.md)
- [Chapter 14, Your second real application](chapter-14.md)
- [Chapter 15, FYI, P5 is fork friendly and free-fusable](chapter-15.md)
- [Chapter 16, Reusable GUI components](chapter-16.md)

## Appendix

- [Appendix, Expression iterator](appendix-expressions-iterators.md)
- [Appendix, Boolean algebra on expressions](appendix-expressions-boolean-algebra.md)

## Version

The current version you are reading, was created around the same time as Phosphorus Five version 1.0 was released. The book might be updated, as changes occurs in Phosphorus Five, and new releases are being created. The book's current version itself is; 0.5. Meaning, the book is still in *"alpha release"*. However, the book will inevitably change as P5 changes.

## License and copyright

The book is licensed under the terms of the GPL, version 3, and copyright Thomas Hansen, thomas@gaiasoul.com, 2017.

I could have chosen another license, such as Creative Commons, which probably would be a more *"logical"* choice. However, partially as a funny detail, and partially out of respect for P5 and the GPL - I have chosen to license it as GPL, to make sure the book stays open.

This choice of license also easily allows you to create patches to the book, and supply to me, at the main GitHub project site for the book - Which can be found [here](https://github.com/polterguy/phosphorusfive-dox).

*"Sharing is caring"*

And remember; *"Mostly harmless, and don't panic!"* ... ;)