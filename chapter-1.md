# Chapter 1, Ajax

This is an *"advanced topic"*, and not necessary for the understanding of P5. If you wish, you can skip this part, and refer back to it later, when you want to understand the internals of the Ajax engine in P5. If so, then feel free to skip to the [next chapter](chapter-2.md).

## What is Ajax

Ajax is a technology for incrementally applying changes to an HTML page. It is an acronym, although still commonly referred to, and written like the header of this chapter writes it. It means _“Asynchronous JavaScript and XML”_, and its name is actually highly misleading, since it rarely have anything to do with XML.

Ajax allows us to change parts of the view in our web pages, by fetching data from a server, and using this data to modify parts of what the user is seeing on his page. It is often referred to as GUI in its broader sense, meaning Graphical User Interface, and is what allows us to create rich web applications, where your web pages _“come alive”_, and becomes interactive.

Ajax is built around a simple idea, which is the ability to use what's often referred to as the *"XHR object"*, or the *"XML HTTP Request object"*. The XHR object allows you to asynchronously retrieve data from a server. This combined with the ability to dynamically modify the DOM, or *"Document Object Model"*, allows for the experience of *"interactive web pages"*. DOM is what your HTML is creating when it is being evaluated by your browser.

## Managed Ajax internals

Phosphorus Five contains a _“managed Ajax library”_, which can be found in the project called *“/core/p5.ajax/”*. This Ajax library is built upon WebForms from ASP.NET. If you have heard about ASP.NET and Web Forms before, then don’t let this scare you away from P5. Phosphorus Five has little in common with traditional WebForms applications.

Managed Ajax simply implies that the use of JavaScript are for the most parts *optional*. With p5.ajax, you do not need to use JavaScript at all to create rich interactive Ajax web pages. You *can* use JavaScript if you wish, and using JavaScript is in fact surprisingly easy in combination with P5. However, if you do not wish to use JavaScript, you can still create stunningly rich interactive web apps. There are almost no places in P5, out of the box, that contains any explicitly written JavaScript parts. Hence, we refer to the technology used in P5 as _“managed Ajax”_.

The Ajax library in P5 uses JSON internally to return data from the server. JSON is another acronym, and means _“JavaScript Object Notation”_. JSON is a technology for creating JavaScript objects, which are easily transferred from your server to its clients. The reason why Ajax almost never has anything to do with XML, is because JSON has almost entirely replaced XML as a data transmitting mechanism. A more correct word for Ajax, would therefor in fact be _“Ajaj”_, suggesting _“Asynchronous JavaScript and JSON”_.

In P5, these parts are perfectly abstracted away for you, and there are rarely, if ever, any need to understand what goes on underneath the hoods of the Ajax engine. Nor is it necessary to in any ways modify, or interact with these parts of P5. You *can* easily interact with these parts of P5 though, and extend these parts if you wish - But, you will rarely need to do such a thing.

The above makes P5 a perfect beginner's Ajax framework, significantly simplifying the process of creating rich Ajax applications. While also, due to its extensibility, and ability to allow the developer to tap into its core - Also a perfect framework for the seasoned architect and software developer. Arguably, in general, P5's design, is all about *"bridging"* - Which you will discover as you proceed.

### Debugging Ajax requests

When an HTTP request is created from your client, and transmitted to the server, the client creates an HTTP FORM POST request towards your server, using standard HTTP mechanisms, through the XHR object. The server will internally process this request, incrementally track all changes done during the request, and return the changes back to the client as JSON. If you turn on the _“Inspect”_ features of Google Chrome, and open the _“Network”_ tab, you can see for yourselves exactly what is sent to the server, by clicking any of the requests that are created towards your server, and switch between the _“Headers”_ and _“Response”_ tab of your request. If you do this in a P5 Ajax request, you will see a _“Form Data”_ section in your _“Headers”_ section, containing all HTTP FORM element values, and the resulting JSON in the _“Response”_ tab. You can also choose to look at the _“Preview”_ tab, to more easily navigate the returned JSON from the server.

All of the above mentioned things, are 99.9% of the time, completely irrelevant for you as a P5 developer - But might be of interest, if you’re curious about just how P5 does what it does. It might also be of interest, if you need to do something *"advanced"* with P5.

### Ajax technology choices in P5

The Ajax engine internally in P5, actually uses what’s referred to as *"ViewState"* in ASP.NET. P5 however, uses the ViewState in a very intelligent manner, exclusively keeping it on the server. This completely eliminates all traditional ViewState problems, which you can see, if you do a quick Google search for *“ViewState”*. This means that a P5 Ajax request, is often several orders of magnitudes smaller in size, than an Ajax request created in for instance ASP.NET AJAX. This makes P5 a perfect framework for creating highly rich Ajax applications, for devices that does not have a high bandwidth internet connection. Examples includes web apps intended to run on smart phones, etc.

The caveat though, is that this must mirror everything from the client, on the server. The server is hence keeping the entire _“state”_ of your web page, such that it can keep track of which changes are applied to your page during an Ajax request/response. Another caveat, is that this also means that the entire HTTP FORM must be submitted upon every single Ajax request. These two caveats, have few if any practical side effects for you. However, this is what facilitates for P5's stunningly beautiful architecture and development model, for incrementally updating your web pages the way it does.

The above technology, allows you to modify any *"widget"* on your page, from an event raised by any other *"widget"*. This facilitates for a significantly less complex development model, for applying changes to your page. Which is why knowledge about JavaScript becomes *optional* when you use P5.

When creating a P5 web app, you will in fact feel as if you are developing a Desktop Windows app, due to the above mentioned features. In fact, creating a highly rich Ajax app in P5, is possibly even easier than creating something similar in WinForms, Xamarin forms, Qt, or similar technologies.

## Bandwidth usage

Due to the above mentioned technologies, the amount of bandwidth consumed by P5, is often *"magically small"*. P5 will often use orders of magnitude less bandwidth than its competing technologies. This is true both for its initial page loading, and its consecutive Ajax requests. The main JavaScript portions of P5, is no more than roughly 3KB in size. The average Ajax request, is often not more than 1KB.

Other competing technologies, often requires hundreds, and sometimes even thousands of kilobytes of JavaScript, to do what P5 allows you to do with 3 kilobytes of JavaScript. The difference in performance between P5 and some of its competing technologies is often several orders of magnitudes. Some parts of P5 have been profiled against some of the major player's technologies in this area, and shown how the *"competititors"* often use as much as 150 times the amount of bandwidth as P5 does to solve the same problems. This makes P5 a perfect framework for developing web apps with bandwidth constraints.

## Server side performance and security

In a stateless web app, often your database must be more frequently queried, or some other expensive resource must be polled upon every single postback to your server. Although Hyperlambda is an extremely *"high level programming language"*, it often due to these facts, performs surprisingly well, compared with other technologies. In addition, without state, a whole range of security issues becomes much more prevalent, broadening the *"attack surface"* of your server. P5 is *secure by default*, and you'll actually have to consciously do something wrong, to create security holes.

An example can be illustrated by editing some item from a database. Completely stateless, a web app must store this value, associated with the client somehow. This can be done through a cookie, an invisible input HTML element, or some other value transferred to the client, which the server expects the client to return, when it is done editing the record. Nothing prevents a malicious client from changing this ID, making the server side code, edit a completely different item. In P5, you'd store this ID on the server, making it impossible to modify for a malicious client.

Security issues like the examples above, *can* be fixed in a more stateless model of developing web apps. In P5 however, they're completely non-existent, significantly reducing the complexity of creating rock hard secure web apps, without introducing complex architecture, or pages up and down of *"remember to do this"* lists, to check before you deploy your app into production.

Several books, arguably multiple libraries, with *"security concerns"* - Are simply not relevant what so ever with P5.

[Chapter 2, Hello World](chapter-2.md)