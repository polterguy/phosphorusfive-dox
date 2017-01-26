# Hello World

Assuming you have already downloaded P5, and managed to get it up and running, we are going to create our first *"Hyperlambda application"* called *"Hello World"*.

Open up your Apps/CMS editor, by choosing it in your menu at the top. Click the _“+”_ button, and choose to create a new _“lambda”_ page. Then remove the existing code, if any, and paste the following Hyperlambda into your editor, for then to click _“Save”_, and _“View page”_.

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

If you try to click the button created by the Hyperlambda above, it will change its value to *"Hello World"*.

## Walking through our code

Hyperlambda is a key/value/children file format. Technically, it is not in fact even a programming language, but a file format, for declaring *"graph objects"*, or tree structures. In fact, it is quite similar to JSON, for those acquinted with it.

Above, our `create-widget:foo` parts, which is our first line of code, declares a *"node"*. The node has a name, or a key, being **[create-widget]**, and a value being *"foo"*. This creates a *"widget"* for us, which is an HTML element. Which type of element, and/or widget, this will create, depends upon which arguments you supply to it. The widget will have an ID attribute of *"foo"* though, which is later used to refer to the widget, and change or retrieve its properties and/or value(s).

Our above **[create-widget]** invocation, has three child nodes;

- **[parent]**
- **[class]**
- **[widgets]**

To declare a child of another node in Hyperlambda is very easy. All you have to do, is to indent your node with two spaces, compared to the indentation of the node you wish to declare these children on behalf of. This makes sure that your node becomes a children of the node above it, or an *"argument"* if you wish, to your original node.

The **[parent]** argument, declares which parent HTML widget you wish to inject your widget into. The **[class]** argument, declares the CSS class you wish to use for it. And the **[widgets]** argument, becomes a collection of children HTML widgets your original widget will contain.

You can use any **[parent]** you wish to use for your widget, which allows you to inject your widget, into any other pre-existing widget's collection you wish for your widget to appear within. The *"content"* parent we are using above, happens to be a generic container widget, from the main default template of the CMS of System42.

The *"col-xs-12"* CSS class value of our **[class]** argument, refers to a CSS class from Bootstrap CSS, which is a commonly used Open Source CSS framework, used in P5, out of the box.

Of all the above arguments, the **[widgets]** argument is probably the most important. The reason why, is because this argument declares which type of widget we want to create. There are three types of widgets in P5;

* Literal widgets, which are for text and/or HTML values
* Container widgets, which are widgets that can contain other widgets
* Void widgets, which are widgets that can neither have any text/HTML value, nor any children widgets

The above **[widgets]** declaration, informs our **[create-widget]** invocation, that we want to create a *"Container"* widget. Inside of a **[widgets]** collection, we can create additional children widgets, by simply referring to them with the names of **[void]**, **[container]** or **[literal]**. There is also an additional *"deferred"* way of declaring children widgets, which we will have a look at later. But for now, the above mentioned declaration will be assumed.

Inside our above `create-widget` invocation, our **[widgets]** argument, hence implies we want to create a **[container]** type of widget. Our main container widget above, happens to have one **[literal]** widget, with the **[innerValue]** of *"Click me"*.

To understand the above code, it might be beneficial to see the resulting HTML.

```xml
<div id="foo" class="col-xs-12">
    <button id="bar" class="btn btn-default" onclick="p5.e(event)">Click me!</button>
</div>
```

Above is the HTML that your Hyperlambda above will produce for you. Notice how our inner widget becomes of type *"button"*. This is because of the argument **[element]**, which declares what type of HTML widget you wish to create.

## Ajax events

In our above example, we have an **[onclick]** Ajax event. This will produce and automatically handled *"onclick"* DOM event handler for us, which once raised, will create an Ajax request, going towards our server, invoking the Hyperlambda declared as its content (children nodes).

Such Hyperlambda collections, as the one we have declared inside of our **[onclick]** event handler, is often referred to as *"lambda objects"*, or simply *"lambda"*, and are stored Hyperlambda objects, which are executed, whenever some condition is being met, or we wish to for some reasons execute our Hyperlambda.

The *"lambda"* above, simply invokes **[p5.web.widgets.property.set]**, with the ID of *"bar"*, and an **[innerValue]** argument of *"Hello World"*. This simply changes the **[innerValue]** property of our *"bar"* widget, to whatever text and/or HTML we pass in as the value of our **[innerValue]** argument.

You can change any property, and/or attribute, of your widgets by using the **[p5.web.widgets.property.set]**. If you wish, you could add up for instance `class:btn btn-primary` as an additional argument to **[p5.web.widgets.property.set]**, which would in addition to changing its value, also change its CSS class. In fact, do this, before you continue reading. Then save your page, view it again, and click the button once more.

[Chapter 3, Ajax Widgets dissected](chapter-3.md)