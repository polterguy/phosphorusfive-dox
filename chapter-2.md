# Hello World

Assuming you have already downloaded P5, and managed to get it up and running, we are going to create our first *"Hyperlambda application"* called *"Hello World"*. By stepping through this application, and explaining what it does, you will be armed with the knowledge required to create your own Ajax web apps.

Open up your Apps/CMS editor, by choosing it in your menu/navbar at the top of your page. Click the _“+”_ button, and choose to create a new _“lambda”_ page. Then remove the existing code, if any, and paste in the following Hyperlambda into your editor. When you have done so, make sure you click _“Save”_, and _“View page”_. Notice, you might have some sort of popup blocker enabled, preventing you from viewing the page. If you get some popup blocker notification as you click *"View page"*, make sure you enable popups on the domain from which you are developing your P5 apps. This is normally *"localhost"* or *"127.0.0.1"*, if you're on a development box, creating apps locally.

The Hyperlambda we will use can be found below.

```
create-widget:foo
  parent:content
  class:col-xs-12
  widgets
    literal:bar
      element:button
      class:btn btn-default
      innerValue:Click me
      onclick
        p5.web.widgets.property.set:bar
          innerValue:Hello World
```

If you try to click the button created by the Hyperlambda above, it will change its value to *"Hello World"*. If you wish, you can refresh your page, to reset the button's text, for then to click it again.

## Walking through the code

Hyperlambda is a name/value/children file format. It allows ut to declare *"graph objects"*, or *"tree structures"*, and is quite similar to JSON. With Hyperlambda, you can declare *"lambda objects"*. Your *"lambda objects"*, are created out of *"nodes"*. Hence, Hyperlambda declares lambda, and lambda is a collection of nodes.

Think of it like the relationship between JSON (Hyperlambda), and the JavaScript objects after the JSON has been evaluated (lambda), and properties of your JavaScript object (nodes).

### Visualizing Hyperlambda/lambda/nodes

A useful analogy for understanding the structure of Hyperlambda, is to imagine a single node as a folder on disc. Each folder can have multiple folders inside of itself. These inner folders are the equivalent of a node's children nodes. Each folder can also have files within it. These files corresponds to the *"value"* of your nodes.

Hence, Hyperlambda declares lambda. Lambda consists of nodes. Each node can have a name, and optionally a value, in addition to optionally also a list of children nodes itself.

If you still think this is difficult to understand, you can watch [this video](https://www.youtube.com/watch?v=oML2JE8kAO0), describing the relationship between Hyperlambda, lambda and nodes.

### Analyzing our code

Above, in our `create-widget:foo` parts, which is our first line of code, we first declare a *"node"*. The node has a name, being **[create-widget]**, and a value being *"foo"*. This creates a *"widget"* for us, which is an HTML element. Which type of widget this will create, depends upon which arguments you supply to it. The widget will have an ID attribute of *"foo"*, which is later used to reference the widget, and change or retrieve its properties and/or value(s).

Our **[create-widget]** invocation above has three children nodes;

- **[parent]**
- **[class]**
- **[widgets]**

To declare a child of another node in Hyperlambda is very easy. All you have to do, is to indent your node with two spaces, relative to the indentation of the node you wish to declare these children within. This makes sure that your node becomes a children of the node above it, or an *"argument"*.

The **[parent]** argument, declares which parent HTML widget you wish to inject your widget into. The **[class]** argument, declares the CSS class you wish to use. And the **[widgets]** argument, becomes a collection of children widgets.

You can use any **[parent]** you wish for your widget, which allows you to inject your widget, into any pre-existing widget's collection. The *"content"* **[parent]** we are using above, happens to be a generic container widget, from the main default template of System42's CMS.

The *"col-xs-12"* value of our **[class]** argument, refers to a CSS class from [Bootstrap CSS](http://getbootstrap.com/css/), which is a commonly used Open Source CSS framework. Bootstrap CSS is the default CSS framework in P5.

Of all the above arguments, the **[widgets]** argument is probably the most important. This argument implicitly declares which type of widget we want to create. There are three types of widgets in P5.

* **[literal]** widgets that can have HTML content
* **[container]** widgets that can *"contain"* other widgets
* **[void]** widgets that are empty, having neither of the above

The above **[widgets]** argument to **[create-widget]**, implicitly informs our **[create-widget]** invocation that we want to create a **[container]** widget. Inside of our **[widgets]** collection, we can create additional children widgets, by simply referring to them with the names of **[void]**, **[container]** or **[literal]**. Our main container widget above, happens to have one **[literal]** widget, with the **[innerValue]** of *"Click me"*.

To understand the above code, it might be useful to see its resulting HTML. Below is the HTML our Hyperlambda creates.

```xml
<div id="foo" class="col-xs-12">
    <button id="bar" class="btn btn-default" onclick="p5.e(event)">Click me!</button>
</div>
```

Notice how our inner widget is of type *"button"*. This is because of the argument **[element]**, which declares what type of HTML widget you wish to create. You can create any HTML element you wish, by changing this argument to the name of the HTML element you wish to create.

You can also add any attributes you wish to your widget, by simply adding the attribute as an argument. To add an attribute with the name of *"foo"* and the value of *"bar"* for instance, is as easy as adding `foo:bar` as an argument to our **[create-widget]** invocation.

## Ajax events

In our example above, we have an **[onclick]** Ajax event for our button. This will create an *"onclick"* DOM event handler for us, which when raised, will create an Ajax request, going towards our server, invoking its lambda.

Such lambda collections, as the one we have declared inside of our **[onclick]** event handler, is often referred to as *"lambda objects"*, or simply *"lambda"*. Lambda objects are stored logic, which are executed, whenever some condition is being met - Or we wish to for some reasons execute our lambda. The simplicity in declaring such *"lambda objects"*, is the reason why Hyperlambda got its name.

The *"lambda"* above, simply invokes **[p5.web.widgets.property.set]**, with the ID of *"bar"*, and an **[innerValue]** argument of *"Hello World"*. This simply changes the **[innerValue]** property of our *"bar"* widget, to whatever HTML we pass in as the value of our **[innerValue]** argument.

## Additional studying, video tutorial

If you still struggle with some of the parts we walked through in this chapter, you might benefit from watching [this video](https://www.youtube.com/watch?v=O9ek7JH7Ptw), where we play around with the **[create-widget]** Active Event. In this video we demonstrate how to parametrize our **[create-widget]** invocation, to create whatever HTML we need to create. In addition, we will associate our widget with Ajax events on the server, and do some basic changes to the state of our page, from within our Ajax event handlers.

In case you are reading this book in paper format, you can find links to the videos referred to in this chapter below.

* Hyperlambda 101 - https://www.youtube.com/watch?v=oML2JE8kAO0
* Ajax Widgets 101 - https://www.youtube.com/watch?v=O9ek7JH7Ptw

[Chapter 3, Ajax Widgets dissected](chapter-3.md)