# Ajax widgets

This chapter contains some fairly advanced study topics. If this is your first encounter with P5, you would probably benefit from skipping it for now, and rather move on the to [next chapter](chapter-4.md). Later when you wish to dive really deep into P5, you can come back to this chapter, to acquire an understanding of all the gory details.

An Ajax widget is always defined as one single HTML element. Advanced extension widgets, which we will have a look at later, might have children widgets of themselves. But all the native main widgets, corresponds to a single HTML element on your page. By cleverly combining the **[void]**, **[literal]** and **[container]** widgets, you can create any HTML markup you wish. Contrary to other Ajax frameworks, you have 100% perfect control over your resulting HTML markup in P5.

## Widget attribues

When you create a widget, you often want to add up some attribute for it. This is easily done, by simply adding the attributes as a key/value argument to your widget. Consider the following code, which creates an HTML5 video element for you.

```
create-widget:my_video
  element:video
  width:320
  height:240
  controls
  src:http://www.w3schools.com/html/movie.ogg
  type:video/ogg
  innerValue:Your browser needs to be updated
```

In the above code, almost all arguments will create some sort of attribute. The resulting HTML will resemble something like the following.

```xml
<video 
  id="my_video"
  width="320"
  height="240"
  controls
  src="//www.w3schools.com/html/movie.ogg"
  type="video/ogg">
      Your browser needs to be updated
  </video>
```

All nodes you add to a widget, that does not have some special meaning, will simply translate into an HTML attribute, with its name becoming the name of the attribute, and its value becoming its attribute value. P5 actually knows nothing of any *"video"* element, but the ability to dynamically declare any attributes you wish, combined with being able to control the HTML element used for rendering the widget, allows you to easily create any HTML you wish.

In fact, in the above code, the only arguments which is handled by P5 as *"non-attribute arguments"* are **[element]** and **[innerValue]**. All the other arguments are assumed to be attributes to the resulting HTML. Notice the `controls` declaration above, that translates into an *"empty attribute"*. If you wish to create XHTML compliant HTML, you can exchange it with `controls:controls`.

### Widget Ajax events

You can associate an Ajax event with your widget the exact same way. P5 will determine if what you're creating is an attribute, or an Ajax event, depending upon its name. If your attribute starts out with the string *"on"*, it will be assumed to be an Ajax event. When you create an Ajax event, then whatever children nodes of the event you create, will become the lambda object that is executed, when the Ajax event is raised.

Notice, you are responsible yourselves for making sure your Ajax event actually is associated with a legal DOM event on the client side yourself. You could easily create an Ajax event called *"onxyz"* if you wish. However, this will result in non-conforming HTML, and serve no purpose for you, besides from creating malformed HTML. The same is true for attributes.

In our previous chapter, we created an `onclick` Ajax event using this syntax. Further down in this chapter, we will add a similar Ajax event to our video element.

### Widget arguments

There are some special arguments you can apply to your widgets. These are listed below.

* **[visible]** - Controls a widget's visibility
* **[element]** - Declares which HTML element to render your widget with
* **[widgets]** - Declares its children widgets collection
* **[innerValue]** - Declares the widget's content
* **[events]** - Associates custom *"widget lambda events"* with your widget
* **[parent]** - Parent widget to create widget within
* **[position]** - Positions your widgets as n'th child in its parent's widgets collection
* **[before]** - Inject widget *"before"* specified widget
* **[after]** - Inject widget *"after"* specified widget
* **[oninit]** - An optional custom lambda object, to be executed, when widget is displayed

#### Positioning your widget

The **[parent]**, **[before]** and **[after]** arguments are mutually exclusive, and you can only apply one of these. If you choose to use a **[parent]** argument, then the widget will be injected into this widget's children collection. If you use a **[parent]** argument, you can optionally apply a **[position]** argument, containing an integer number, declaring at which position you want your widget to be injected at.

If you apply an **[after]** or **[before]** argument, you cannot apply a **[parent]**, or a **[position]** argument, and you can only apply one of **[before]** of **[after]**. These arguments refers an existing widget on your page, which you want to inject your widget *"before"* or *"after"* - Depending upon which of these events you use. These four positioning arguments, allows you to inject a widget, at any position in your HTML. Notice how we in the above Hyperlambda, actually completely omitted any positioning arguments. This results in that the default parent widget named *"cnt"* will be implicitly used as a parent to your newly created widget, and that our widget will be appended into its collection of widgets. If no **[parent]**, **[before]** or **[after]** arguments are supplied, the default logic will assume a **[parent]** of *"cnt"*.

#### Which HTML element to render

The **[element]** declares which HTML element you want to render your widget as. Notice, few checks exists in P5 in regards to HTML validity. This allows you to create a widget rendered as the HTML element of *"foo-bar"*. You are yourselves responsible for making sure your code creates valid HTML markup. This argument, if omitted, defaults to *"div"* for **[container]** widgets, *"p"* for **[literal]** widgets, and *"input"* for **[void]** widgets.

#### Controlling the visibility of your widget

The **[visible]** argument, is a boolean, and can take either *"true"* or *"false"*, and declares whether or not your widget should be created initially as visible or not. If you create your widget as invisible, then an invisible *"wrapper"* element will be created for you, at the position you choose to inject your widget. This allows you to later easily make the widget become visible, automatically exchanging this invisible HTML markup, with your widget's actual content, simply by making the widget become visible.

Notice that your **[oninit]** lambda callback, will only be invoked when the widget becomes visible, and it will be invoked **every time** your widget becomes visible. The **[visible]** argument defaults to *"true"* if omitted.

#### Types of widgets you can create

The **[widgets]** and **[innerValue]** arguments are mutually exclusive, and only one of these can be supplied. If you supply a **[widgets]** argument, your widget will be created as a **[container]** widget. If you supply an **[innerValue]** argument, your widget will become a **[literal]** widget. If both of these are omitted, your widget will become a **[void]** widget.

You can also explicitly declare which type of widget you wish to use, by using one of the aliases to **[create-widget]**, which takes an explicit type, as a part of its name. We will look at this later though.

#### Initializing your widget

The **[oninit]** argument declares a lambda object, which will be executed when the widget is displayed. Notice, this lambda will like all other lambda blocks, be executed on the server. It allows you to create initialization logic, which might for instance include some piece of JavaScript, include some stylesheet file, or execute some other type of *"initialization logic"*, intended to be executed, as the widget is displayed. Notice, this lambda block will be executed only when the widget becomes visible, and in fact, once **every time** it becomes visible.

#### Uniquely IDentifying your widgets

As previously discussed, the ID of your widget is the value of your widget creation node. Every widget you create on the same page must have a unique ID.  This sometimes creates a problem for you, as you create reusable lambda objects, intended to be repeatedly executed, that creates some sort of widget for you. For such situations, you can simply omitt the ID, and have an automatically created ID assigned to your widget. This ID will in most cases consist of an *"x"*, followed by a random 7 digits hexadecimal number, resembling something like the following *"x0123adf"*.

This makes it impossible for you to know the ID of your widgets within your Ajax event handlers. However, this poses no real problem for you, since the ID of your widget is always passed into your Ajax event handlers automatically. The name of this node is **[_event]**. If you wish to see this in action, you can remove the explicit ID in our above Hyperlambda that created our video element, and append the following code, before you save and view the page again.

```
  onclick
    sys42.windows.show-lambda:x:/..
```

When you have saved your page, and viewed it, make sure you click the video element, to see the automatically created ID.

The expression to retreieve the ID of a widget is as follows; `:x:/../*/_event?value`.

#### Widget lambda events

The **[events]** argument, is arguably the most complex argument you can apply to your widget. It allows you to associate an Active Event collection with your widget, or what is often referred to as *"widget lambda events"*. We will go into more details of exactly what this is later, but for now, think of these as *"widget methods"*, *"functions"*, or *"pieces of functionality, and/or logic, which you can invoke, which are associated with your widget, and only exists for the life time of your widget*".

Beneath your widget's creation node, you can add a children node, having the name of **[events]** to declare a *"widget lambda events collection"*. The name of the children node beneath your **[events]** node, becomes the name of the Active Event associated with your widget.

### Invisible properties and Ajax events

Sometimes, you might need to associate some piece of data with your widget, that you do not want to render as attributes to the client. This is easily done, by prepending your attribute name with either an underscore *"_"*, or a period *"."*. This makes it possible for you to associate an *"attribute value"* with your widget, that is actually never passed on to the client in any ways. This *"attribute"*, or *"property"* to be more accurate, can easily be retrieved and modified on the server side, the same way any normal attribute can be accessed.

You can also create invisible Ajax events using the same technique, by for instance creating an Ajax event named *".on_foo"*, which is never rendered to the client, but can be invoked, by tapping into the JavaScript API of P5. This allows you to create what's often referred to as *"web methods"*, associate these with some widget, and invoke these web methods from JavaScript.

### Changing attributes and properties

To change an attribute, you can use **[p5.web.widgets.property.set]**. To retrieve the value of an attribute, you can use **[p5.web.widgets.property.get]**. The naming of these Active Events, is a common convention in P5, where the collection type you wish to access is given as a major part of the name of the events, while the operation you wish to perform is supplied as the latter parts of its name. Often these Active Events have a namespace before their names, associating them with a particular parts of P5. Think of *"p5.web.widgets"* as the namespace, *"property"* as the collection type, and *"get"* and *"set"* as the operation you want to perform.

Both of the above mentioned Active Events, takes one or more IDs, and reacts upon the specified widget(s) accordingly. Below is a piece of Hyperlambda that creates a widget, which once the mouse is hovered above it, changes a couple of attributes. When the mouse leaves the widget, it retreieves a couple of attributes, and shows a debug window.

```
create-widget:my_video
  element:video
  width:320
  height:240
  controls
  src:http://www.w3schools.com/html/movie.ogg
  type:video/ogg
  innerValue:Your browser needs to be updated
  onmouseover
    p5.web.widgets.property.set:my_video
      width:640
      height:480
  onmouseout
    p5.web.widgets.property.get:my_video
      src
      type
    sys42.windows.show-lambda:x:/..
```

Try creating a lambda page with the above Hyperlambda, save it, view it, and move your mouse over the video element, for then to move the mouse out from the element again.

## Debugging your Ajax events

Often you need to know the state of some piece of lambda during the execution of an Ajax event. This is easily done, by invoking **[sys42.windows.show-lambda]**, and passing in an expression, leading to whatever it is you wish to inspect. Above in our **[onmouseout]** example, there is an example of how to view the entire lambda object for our *"onmouseout"* Ajax event handler.

Don't worry if you do not understand the `:x:/..` expression above. It will be thoroughly explained in a later chapter.

[Chapter 4, Your first Ajax form](chapter-4.md)