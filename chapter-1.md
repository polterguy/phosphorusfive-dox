# Phosphorus Five, the beginner's guide

Welcome to the book about Phosphorus Five. Phosphorus Five, also referred to as P5 in this guide, is a lot of different things. It is a simple design pattern, it is an Ajax library, it is a programming language, and it is a framework. Some would also argue that it is a web operating system. What you choose to refer to it as, is really quite irrelevant. The point is that it solves your problems, particularly the ones you’re having, as you try to create rich and interactive web apps. P5 is explicitly created to ease your burden when you wish to create rich interactive, single page web apps. This book aims at being your _“one stop guide”_, as you start out with P5. A beginner’s introduction. Starting out at the _“for dummies level”_, and hopefully moving you on to the expert’s level.

## Chapter 1, Ajax

Ajax is a technology for incrementally apply changes to an HTML page. It is an acronym, although still commonly referred to, and written like the header of this chapter. It means _“Asynchronous JavaScript and XML”_, and its name is actually highly misleading, since it rarely have anything to do with XML.

Ajax allows us to change parts of the view in a web page, by fetching data from a server, and using this data to modify parts of what the user is seeing on his page. It is for the most parts used as a part of what’s often referred to as UX in its broader sense, or User eXperience, and is what allows us to create rich web applications, where your web pages _“comes alive”_, and becomes interactive.

Phosphorus Five contains a _“managed Ajax library”_, which can be found in the project called _“p5.ajax”_. This Ajax library is built upon WebForms from ASP.NET, but don’t let this scare you away from it, since it has little in common with traditional WebForms applications.

### Managed Ajax

Managed Ajax simply means that the use of JavaScript are for the most parts optional. With p5.ajax, you do not need to use JavaScript to create rich interactive Ajax web pages. You can use JavaScript if you wish, and using JavaScript is in fact surprisingly easy in combination with P5. However, if you do not wish to use JavaScript, you can still create stunningly rich interactive web pages. There are almost no places in P5, out of the box, that contains any explicitly written JavaScript parts. Hence, we refer to the technology used in P5 as _“managed Ajax”_.

The Ajax library in P5 uses JSON to return data from the server to the client. JSON is another acronym, and means _“JavaScript Object Notation”_. Don’t worry if you don’t understand what this is, since the understanding of JSON is in no ways necessary to be able to use P5 to its fullest. However, JSON is simply just a way of creating JavaScript objects, which are easily transferred from a server to a client. In fact, the reason why Ajax almost never has anything to do with XML, is because JSON has almost entirely replaced XML as a data transmitting mechanism. A more correct word for Ajax, would therefor in fact be _“Ajaj”_, implying _“Asynchronous JavaScript and JSON”_.

In P5, these parts are however perfectly hidden for you, and there are rarely, if ever, any needs to understand what goes on underneath the hoods of the Ajax engine, nor to in any ways modify or interact with these parts of P5. You can easily interact with these parts of P5 though, and extend it if you wish, but you will rarely find a need to do so.

When a request is created from your client, and transmitted to the server, the client creates an HTTP FORM POST request towards the server, using standard HTTP mechanisms. The server internally process this request, incrementally tracks all changes done during the request, and returns the changes back to the client as JSON. If you turn on the _“Inspect”_ features of Google Chrome for instance, and open the _“Network”_ tab, you can see for yourselves exactly what is sent to the server by clicking any one of the requests that are created towards your server, and switch between the _“Headers”_ and _“Response”_ tab of your request. If you do this in a P5 Ajax request, you will see a _“Form Data”_ section in your _“Headers”_ section, containing all HTTP FORM element values, and the resulting JSON in the _“Response”_ tab. You can also choose to look at the _“Preview”_ tab, to more easily navigate the returned JSON from the server.

All of the above mentioned things, are 99.9% of the time, completely irrelevant for you, as a P5 developer, but might be of interest, if you’re curious about just how P5 does what it does.

### Ajax internals

The Ajax engine internally in P5, actually uses what’s referred to as ViewState in ASP.NET. P5 however, uses the ViewState in a very intelligent manner, exclusively keeping it on the server. This completely eliminates all traditional ViewState problems, which you can see, if you do a quick Google search for _“ViewState”_. This means that a P5 Ajax request, is often several orders of magnitudes smaller in size, than an Ajax request created in for instance ASP.NET Ajax. This makes P5 a perfect framework for creating very rich Ajax applications, for devices that does not have high bandwidth internet connection. Examples includes web apps intended to run on smart phones, etc.

The caveat though, is that this must mirror everything from the client, on the server. The server is hence keeping the entire _“state”_ of your web page, such that it can keep track of which changes are done to your page, during an Ajax request/response. Another caveat, is that this also means that the entire HTTP FORM must be submitted upon every single Ajax request. These two caveats, have few, if any practical side effects for you, in your day to day use of P5 though. However, this is what allows P5 to create its stunningly beautiful model, for incrementally updating your web pages, the way it does.

### The trinity of Ajax widgets

There are in fact only three main Ajax widgets in P5, and they all inherit from the same base class internally. These widgets are as follows;

+ The Container widget, that can have children widgets of itself
+ The Literal widget, that can only contain text and/or HTML
+ The Void widget, that can have neither children, nor text/HTML content

The Container widget, serves as a container for other widgets. It can contain children widgets of itself, through its _“Controls”_ collection in C#, or its *[widgets]* collection in Hyperlambda.

The Literal widget, serves as a placeholder for a piece of text, and/or HTML, and can have its content manipulated through its _“innerValue”_ property in C#. To set its value in Hyperlambda, use the *[innerValue]* property. Hence, both Hyperlambda and C# uses the same property name for changing this widget’s content.

The Void widget, does not have any content at all, and is often used for HTML elements such as the _“br”_ tag, _“hr”_ tag or HTTP FORM _“input”_ elements. These are HTML elements that cannot have any content at all.

Which widget you should use, depends upon your needs. If you create an _“input”_ or _“br”_ HTML element for instance, then you must use a void widget. If you try to use any of the other widgets, an exception will be raised during execution. If you want to create a _“textarea”_ HTML element, you must use a Literal widget. A _“select”_ HTML element, requires you to use a Container widget.

Most other HTML elements though, allows you to freely choose between the Literal and Container widget, as you see fit. Which widget you choose, depends upon whether or not you only need to reference the content of your widget as a single piece of text and/or HTML, at which case you should use the Literal widget - Or if you need to have individual access to parts of its content, at which turn you should use a Container widget.

### Your first Ajax Widget

If you open up your Apps/CMS editor, and click the _“+”_ button, and choose to create a new _“lambda”_ page, you can paste the following Hyperlambda into your editor, for then to click _“Save”_, and _“View page”_.
