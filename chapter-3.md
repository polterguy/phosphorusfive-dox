# Ajax widgets

An Ajax widget always is defined as one single HTML element. Advanced extension widgets, which we will have a look at later, might have children widgets of themselves. But all the native main widgets, corresponds to a single HTML element on your page. By cleverly combining the **[void]**, **[literal]** and **[container]** widgets, you can create any HTML markup you wish. Contrary to other Ajax frameworks, you have 100% perfect control over your resulting HTML markup in P5.

## Widget attribues

When you create a widget, you often want to add up some attribute for it. This is easily done, by simply adding the attributes as a key/value argument to your widget. Consider the following code, which create an HTML5 video element for you.

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

In the above code, almost all arguments will create some sort of attribute, and the resulting HTML will look like this;

```xml
<video 
  id="my_video"
  width="320"
  height="240"
  controls
  src="//www.w3schools.com/html/movie.ogg"
  type="video/ogg">Your browser needs to be updated</video>
```

All nodes you add to a widget, that does not have some special meaning, will simply translate into an HTML attribute, with its name becoming the name of the attribute, and its value becoming its attribute value.

P5 knows nothing of any *"video"* element, but the ability to dynamically declare any attributes you wish, combined with being able to control the HTML element used for rendering the widget, allows you to easily create any HTML you wish.

In fact, in the above code, the only arguments which are handled by P5 as *"non-attribute arguments"* are **[element]** and **[innerValue]**. All the other arguments are assumed to be attributes to the HTML rendered. Notice the `controls` declaration above, that translates into an *"empty attribute"*. If you wish to create XHTML compliant HTML, you can exchange it with `controls:controls`.

### Widget arguments

There are however some few special arguments to your widgets. These are listed below;

* **[visible]** - Controls a widget's visibility
* **[element]** - Declares which HTML element to render widget with
* **[widgets]** - Declares its children widget collection
* **[innerValue]** - Declares the widget's content
* **[events]** - Associates custom events with your widget
* **[parent]** - Parent widget to create widget within
* **[position]** - Positions your widgets as n'th child in parent's widgets collection
* **[before]** - Inject widget *"before"* specified widget
* **[after]** - Inject widget *"after"* specified widget
* **[oninit]** - An optional custom lambda object, to be executed, when widget is initially displayed

The **[parent]**, **[before]** and **[after]** arguments are mutually exclusive, and you can only apply one of these arguments. If you choose to use a **[parent]** argument, then the widget will be injected into this widget's children collection. If you use a **[parent]** argument, you can optionally apply a **[position]** argument, containing an integer number, declaring at which position your widget will be injected.

If you apply an **[after]** or **[before]** argument, you cannot apply a **[parent]**, or a **[position]** argument. And you can only apply one of **[before]** of **[after]**. These arguments declares an existing widget on your page, which you want to inject your widget *"before"* or *"after"*, depending upon which of them you use. These four positioning arguments, allows you to inject a widget, at any position in your HTML. Notice how we in the above Hyperlambda, actually completely omitted any positioning arguments. This results in that the default parent widget named *"cnt"* will be implicitly used as a parent to your newly created widget.

The **[element]** declares which HTML element you want to render your widget as. Notice, few checks exists in P5 in regards to HTML validity, which allows you to create a widget rendered as the HTML element of *"foo-bar"*. You are yourselves responsible for making sure your code creates valid HTML markup. This argument defaults to *"div"* for **[container]** widgets, *"p"* for **[literal]** widgets, and *"input"* for **[void]** widgets, if omitted.

The **[visible]** argument, is a boolean, and can take either *"true"* or *"false"*, and declares whether or not your widget should be created initially as visible, or if you wish to create it as invisible. If you create your widget as invisible, then an invisible *"wrapper"* element will be created for you, at the position you choose to inject your widget. This allows you to later easily make the widget become visible, exchanging this invisible HTML markup, with your widget's actual content. Realise that your **[oninit]** lambda callback, will only be invoked when the widget becomes visible. And it will be invoked **every time** your widget becomes visible. This argument defaults to *"true"* if omitted.

The **[widgets]** and **[innerValue]** arguments, are mutually exclusive, and only one of these can be applied. If you use a **[widgets]** argument, your widget will be created as a **[container]** widget. If you use **[innerValue]**, your widget will become a **[literal]** widget. You can also explicitly declare which type of widget you wish to use, by using one of the aliases to **[create-widget]**, which takes an explicit type, as a part of its name. We will look at this later though. If you do not apply neither a **[widgets]**, nor an **[innerValue]** argument, your widget will be assumed to be of type **[void]**.

The **[oninit]** argument, declares a lambda block, which will be executed when the widget is initially displayed. Notice, this lambda will (of course) like all other lambda blocks, be executed on the server. It allows you to create initialization logic, which might for instance include some piece of JavaScript, include som CSS stylesheet file, etc, when your widget is initially displayed. Notice, as we discussed in the **[visible]** argument, this lambda block will be executed only when the widget becomes visible, and in fact, once every time it becomes visible.