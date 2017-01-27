# Chapter 1, Ajax

This is an *"advanced topic"*, and not necessary for the understanding of P5. If you wish, you can skip this part, and refer back to it later, when you want to understand the internals of the Ajax parts of P5. If so, then feel free to skip to the [next chapter](chapter-2.md).

## What is Ajax

Ajax is a technology for incrementally applying changes to an HTML page. It is an acronym, although still commonly referred to, and written like the header of this chapter writes it. It means _“Asynchronous JavaScript and XML”_, and its name is actually highly misleading, since it rarely have anything to do with XML.

Ajax allows us to change parts of the view in a web page, by fetching data from a server, and using this data to modify parts of what the user is seeing on his page. It is for the most parts used as a part of what’s often referred to as UX in its broader sense, or User eXperience, and is what allows us to create rich web applications, where your web pages _“comes alive”_, and becomes interactive.

Phosphorus Five contains a _“managed Ajax library”_, which can be found in the project called _“p5.ajax”_. This Ajax library is built upon WebForms from ASP.NET, but don’t let this scare you away from it, since it has little in common with traditional WebForms applications.

## Managed Ajax

Managed Ajax simply means that the use of JavaScript are for the most parts optional. With p5.ajax, you do not need to use JavaScript at all to create rich interactive Ajax web pages. You *can* use JavaScript if you wish, and using JavaScript is in fact surprisingly easy in combination with P5. However, if you do not wish to use JavaScript, you can still create stunningly rich interactive web pages. There are almost no places in P5, out of the box, that contains any explicitly written JavaScript parts. Hence, we refer to the technology used in P5 as _“managed Ajax”_.

The Ajax library in P5 uses JSON to return data from the server to the client. JSON is another acronym, and means _“JavaScript Object Notation”_. Don’t worry if you don’t understand what this is, since the understanding of JSON is in no ways necessary to be able to use P5 to its fullest. However, JSON is simply just a way of creating JavaScript objects, which are easily transferred from for instance your server to its clients. In fact, the reason why Ajax almost never has anything to do with XML, is because JSON has almost entirely replaced XML as a data transmitting mechanism. A more correct word for Ajax, would therefor in fact be _“Ajaj”_, implying _“Asynchronous JavaScript and JSON”_.

In P5, these parts are however perfectly hidden for you, and there are rarely, if ever, any need to understand what goes on underneath the hoods of the Ajax engine, nor to in any ways modify, or interact with these parts of P5. You can easily interact with these parts of P5 though, and extend it if you wish, but you will rarely find a need to do so.

When a request is created from your client, and transmitted to the server, the client creates an HTTP FORM POST request towards the server, using standard HTTP mechanisms. The server internally process this request, incrementally tracks all changes done during the request, and returns the changes back to the client as JSON. If you turn on the _“Inspect”_ features of Google Chrome for instance, and open the _“Network”_ tab, you can see for yourselves exactly what is sent to the server, by clicking any one of the requests that are created towards your server, and switch between the _“Headers”_ and _“Response”_ tab of your request. If you do this in a P5 Ajax request, you will see a _“Form Data”_ section in your _“Headers”_ section, containing all HTTP FORM element values, and the resulting JSON in the _“Response”_ tab. You can also choose to look at the _“Preview”_ tab, to more easily navigate the returned JSON from the server.

All of the above mentioned things, are 99.9% of the time, completely irrelevant for you, as a P5 developer, but might be of interest, if you’re curious about just how P5 does what it does. It might also be of interest, if you need to do something *"advanced"* with P5.

## Ajax internals

The Ajax engine internally in P5, actually uses what’s referred to as *"ViewState"* in ASP.NET. P5 however, uses the ViewState in a very intelligent manner, exclusively keeping it on the server, among other things. This completely eliminates all traditional ViewState problems, which you can see, if you do a quick Google search for *“ViewState”*. This means that a P5 Ajax request, is often several orders of magnitudes smaller in size, than an Ajax request created in for instance ASP.NET AJAX. This makes P5 a perfect framework for creating highly rich Ajax applications, for devices that does not have a high bandwidth internet connection. Examples includes web apps intended to run on smart phones, etc.

The caveat though, is that this must mirror everything from the client, on the server. The server is hence keeping the entire _“state”_ of your web page, such that it can keep track of which changes are done to your page, during an Ajax request/response. Another caveat, is that this also means that the entire HTTP FORM must be submitted upon every single Ajax request. These two caveats, have few, if any practical side effects for you, in your day to day use of P5 though. However, this is what allows P5 to create its stunningly beautiful architectural model, for incrementally updating your web pages the way it does.

## Bandwidth usage

Due to the above mentioned technologies, the amount of bandwidth used by P5, is often *"magically small"*. Often P5 will use orders of magnitude less bandwidth, than its competing technologies. Both in its initial request, meaning the initial loading of your page, and in its consecutive Ajax requests, where you want to fetch additional data from the server, to modify your page's state in some ways. The main JavaScript portions of P5, is for instance in fact, no more than roughly 3KB in size, after minification and GZipping.

Other competing technologies, often requires hundreds, and sometimes in fact thousands of kilobytes of JavaScript, to do what P5 allows you to do with 3 kilobytes of JavaScript.

[Chapter 2, Hello World](chapter-2.md)