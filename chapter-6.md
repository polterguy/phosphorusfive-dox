# Changing your tree

Hyperlambda and Phosphorus Five is a unique programming platform, since it among other things, doesn't contain the concept of a *"variable"*. This is because everything can be modified, as you execute your lambda objects. Hence, arguably, everything becomes a potential variable in P5.

However, often you need to store some kind of temporary variable, which you change during the execution of your lambda. For such scenarios, you have 4 basic Active Events you can use.

- **[set]**, changes nodes, its values, or its names
- **[add]**, appends children nodes to existing nodes
- **[insert-before]**, inserts nodes, before some specified nodes
- **[insert-after]**, inserts nodes, after some specified nodes

These four Active Events, allows you to modify your lambda objects, during the execution of your lambda. Notice, the **[set]** event, can in addition to changing a node, also completely remove it. Hence, with these four events, you have all *"CRUD"* operations available for your lambda objects.

**Definition**; *"CRUD"* is an acronym, and means *"Create, Remove, Update and Delete"*, and is a reference to all the 4 basic operations necessary to be able to dynamically *"mold"* an object, in any of the necessary axis, to be able to *"create anything you wish, starting from any given starting point"*.

All of these Active Events, can be given multiple destinations. This means that a single invocation, might change multiple things.

## The [set] event

This is the most basic Active Event for modifying your lambda. You can change a node, its value, or its name by using this event. Consider the following code.

```
_foo
set:x:/@_foo?value
  src:I was changed
```

After executing the above Hyperlambda, your **[_foo]** node's value, will be *"I was changed"*. By combining the **[set]** event, with what we refer to as *"formatting expressions"*, you can easily concatenate strings. Consider the following code.

```
_foo:Old value
set:x:/@_foo?value
  src:{0}, and additional value
    :x:/@_foo?value
```

After execution of the above Hyperlambda, you will effectively have concatenated the **[_foo]** node's existing value, with the string *", and additional value"*.

However, unless you execute the above code in the Apps/Executor, it might be difficult to see its results. Let's create a simple form, where we use the **[set]** event, in combination with some *"formatting expressions"*, to ask the user for his name, and create a modal confirmation window, returning some *"Hello there John Doe"* text to him.

```
create-widget
  parent:content
  class:col-xs-6 col-xs-push-3 text-right
  widgets
    void:first_name
      element:input
      placeholder:Give me your first name ...
      class:form-control
    void:last_name
      element:input
      placeholder:Give me your last name ...
      class:form-control prepend-top
    literal
      element:button
      class:btn btn-default prepend-top
      innerValue:Submit
      onclick
        _widgets
          first_name
          last_name
        p5.web.widgets.property.get:x:/@_widgets/*?name
          value
        set:x:/../*/sys42.windows.confirm/*/body?value
          src:Hello there {0}, {1}
            :x:/@p5.web.widgets.property.get/0/*?value
            :x:/@p5.web.widgets.property.get/1/*?value
        sys42.windows.confirm
          header:Hello world
          body
```


The first obvious thing you might see in the above **[onclick]** event handler, is that the **[body]** argument to our **[sys42.windows.confirm]** invocation, is actually initially empty. Still, when our confirmation window is shown, it is perfectly able to show something resembling the following.

![alt tag](screenshots/chapter-6-1.png)

This is because of that our **[set]** invocation concatenates the results from our **[p5.web.widgets.property.get]** invocation, and prepends the text *"Hello there "* in front of the names.

To understand how this happens, realise that the `{0}` and the `{1}` parts of our **[src]** node's value, are replaced with the result of the first and second expressions, that are the children of the **[src]** node. Since these are pointing to the returned value from our **[p5.web.widgets.property.get]** invocation, we end up with a nicely formatted first name, second name, in addition to an initial greeting.

The second thing you may already have noticed, is that instead of supplying a *"static ID"* to which widgets we wish to retrieve the **[value]**s of, we supply an expression, leading to two value; *"first_name"* and *"last_name"*. These happens to be the IDs of our two input elements in our form.

This will make sure that our invocation to **[p5.web.widgets.property.get]**, will in fact return the values from both of our two input textboxes. Almost all Active Events in P5 can take expression values like this, and hence do *"multiple things in one go"*.

To understand the expressions above though, let's us first show a *"debugging window*". This is easily done, by changing your **[onclick]** event handler, adding an invocation to **[sys42.windows.show-lambda]**, just before our **[set]** invocation. Modify your code, to resemble the following;

```
create-widget
  parent:content
  class:col-xs-6 col-xs-push-3 text-right
  widgets
    void:first_name
      element:input
      placeholder:Give me your first name ...
      class:form-control
    void:last_name
      element:input
      placeholder:Give me your last name ...
      class:form-control prepend-top
    literal
      element:button
      class:btn btn-default prepend-top
      innerValue:Submit
      onclick
        _widgets
          first_name
          last_name
        p5.web.widgets.property.get:x:/@_widgets/*?name
          value
        sys42.windows.show-lambda:x:/..
        set:x:/../*/sys42.windows.confirm/*/body?value
          src:Hello there {0}, {1}
            :x:/@p5.web.widgets.property.get/0/*?value
            :x:/@p5.web.widgets.property.get/1/*?value
        sys42.windows.confirm
          header:Hello world
          body
```

As you execute the above code, you will see the returned result, from your invocation to **[p5.web.widgets.property.get]**, where you can confirm that indeed it does return two values. Your screen should at this point resemble something similar to the following code.

![alt tag](screenshots/chapter-6-2.png)

With this in mind, realise that the expression we're using as child formatting expressions to our **[src]** node, are first retrieving the **[p5.web.widgets.property.get]**. Then it is retrieving its zeroth child, which is the node named **[first_name]** from our image above. Then it retrieves this node's children. Since there only happens to be one child beneath this node, it will return this node's value, which happens to be *"Thomas"* for our example.

If you still haven't watched the video from chapter 4, I encourage you to [watch this video](https://www.youtube.com/watch?v=VjG2hGeMnbU), if the above doesn't make much sense to you.

Now it will substitute the `{0}` parts of its **[src]** node's value, with the string *"Thomas"*. Then it does the same thing in the next expression, except it will retrieve the first child node of **[p5.web.widgets.property.get]**, which of course is the **[last_name]** node.

After it has created its **[src]** node's value, by concatenating our strings, it will move the results of this operation into the **[body]** node.

Using this type of logic, we can change parts of our lambda object, that we still haven't execute yet, resulting in that once we execute this lambda, it will have a value, that we dynamically created, up front, before we executed it.

You can of course also create execution instructions too, with a similar technique, by dynamically changing the name of some *"future node"* this way.

## [add]ing things to your tree

The **[add]** event, allows you to append new children into other nodes. However, let's start out with an example.

```
create-widget
  parent:content
  class:col-xs-6 col-xs-push-3 text-right
  widgets
    void:first_name
      element:input
      placeholder:Give me your first name ...
      class:form-control
    literal
      element:button
      class:btn btn-default prepend-top
      innerValue:Submit
      onclick

        /*
         * The content of this node, is dynamically created, according to
         * the input supplied by the user
         */
        .exe

        /*
         * Retrieving the input supplied by the user
         */
        p5.web.widgets.property.get:first_name
          value

        /*
         * This is called "branching".
         * Only if the result of the expression in our "if" node matches
         * the string "Thomas", the lambda object inside of our "if"
         * will be executed.
         * If not matching, our "else" lambda object will execute.
         */
        if:x:/@p5.web.widgets.property.get/*/*?value
          =:Thomas

          /*
           * Adding a confirmation window to our [.exe] node above.
           */
          add:x:/@.exe
            src
              sys42.windows.confirm
                header:Yo boss!
                body:Pleased to see you again
        else

          /*
           * Adding an info-tip window to our [.exe] node above.
           */
          add:x:/@.exe
            src
              sys42.windows.info-tip:Howdy stranger

        /*
         * [eval] will now execute our [.exe] node, almost invoking it, as
         * if it was a "function" or a "method".
         */
        eval:x:/@.exe
```

The above example, will actually dynamically build our code, according to what you type into the textbox. If you type in *"Thomas"*, it will show a modal confirmation window. If you type in anything else, it will show a simple *"info-tip"* window.

Try typing in *"Thomas"*, and verify your result resembles something like the following.

![alt tag](screenshots/chapter-6-3.png)

Then close your modal conformation window, and type in e.g. *"John"*, and click the button. Make sure it resembles the following.

![alt tag](screenshots/chapter-6-4.png)

To understand what's happening in this code, realise we're doing *"branching"* of our code, according to the return value of our **[p5.web.widgets.property.get]** invocation. We will take a deeper look at the concept of *"branching"* later, but basically if the value of our textbox is *"Thomas"*, it will **[add]** a confirmation window into our **[.exe]** node. Otherwise, it will add a tooltip info-tip window into our **[.exe]** node.

Finally, it will invoke this **[.exe]** node, and execute it as a lambda object. Hence, what we have actually done, is to dynamically create a piece of lambda, depending upon the input of a textbox, for then to execute our dynamically created lambda.

Notice, the above code is also heavily commented. You can create comments in Hyperlambda, either by starting out your comments with `/*` and ending them with `*/` - Resulting in that the Hyperlambda parser will ignore everything inbetween. Alternatively, you can create comments by starting your lines with `//`, which makes the parser ignore the rest of the line.

The above code might be challenging to visualize in the beginning. In fact, especially for experienced developers, since there are no similar concepts in main stream use, as far as I know, in any other programming languages on this planet. However, a simple **[sys42.windows.show-lambda]** invocation, just before our **[eval]** invocation, will do the trick for us. Change your code to resemble the following, and try typing in both *"Thomas"* and *"John"* into your textbox, and compare the results.

```
create-widget
  parent:content
  class:col-xs-6 col-xs-push-3 text-right
  widgets
    void:first_name
      element:input
      placeholder:Give me your first name ...
      class:form-control
    literal
      element:button
      class:btn btn-default prepend-top
      innerValue:Submit
      onclick

        /*
         * The content of this node, is dynamically created, according to
         * the input supplied by the user
         */
        .exe

        /*
         * Retrieving the input supplied by the user
         */
        p5.web.widgets.property.get:first_name
          value

        /*
         * This is called "branching".
         * Only if the result of the expression in our "if" node matches
         * the string "Thomas", the lambda object inside of our "if"
         * will be executed.
         * If not matching, our "else" lambda object will execute.
         */
        if:x:/@p5.web.widgets.property.get/*/*?value
          =:Thomas

          /*
           * Adding a confirmation window to our [.exe] node above.
           */
          add:x:/@.exe
            src
              sys42.windows.confirm
                header:Yo boss!
                body:Pleased to see you again
        else

          /*
           * Adding an info-tip window to our [.exe] node above.
           */
          add:x:/@.exe
            src
              sys42.windows.info-tip:Howdy stranger

        /*
         * Showing a "debug window".
         * This is the only added line of code from our previous example.
         */
        sys42.windows.show-lambda:x:/..

        /*
         * [eval] will now execute our [.exe] node, almost invoking it, as
         * if it was a "function" or a "method".
         */
        eval:x:/@.exe
```

As you can see, as you try the above code, it clearly creates two distinctly different pieces of code as its result. Hence, the code has *"changed"*, according to its environment, and *"morphed"* into becoming something else, than what it originally was. This particular example, is a fairly naive and simple one, but this feature is a highly useful feature of Hyperlambda. It might however be difficult to grasp in the beginning, since there doesn't really exist any similar concepts in other programming languages.

In Hyperlambda, you can dynamically create and *"decorate"* your lambda objects, by inserting execution instructions into your lambda object, almost the same way you'd decorate any object in a classic programming language. You can also remove instructions from existing lambda objects. A lambda object in P5, is a dynamic thing, and not a static thing, as it usually is in other programming languages - Including the so-called *"dynamic"* languages.

## [insert-before] and [insert-after]

These two Active Events works identically to **[add]**, except they don't append nodes to its destination(s), but rather *"injects"* its **[src]**, either *"before"* or *"after"* its destination nodes.

Execute the following code in your Apps/Executor, and watch its result.

```
_foo
insert-before:x:/@_foo
  src
    _foo1:bar1
insert-after:x:/@_foo
  src
    _foo2:bar2
```

Probably exactly as you'd expect, it injects one node before **[_foo]**, and another node after **[_foo]**. Besides from that fact, **[insert-before]** and **[insert-after]** shares most of its functionality with **[add]**. Hence, learning how to use any one of these Active Events, very effectively teaches you how to use all of them.

## Commonalities for [add] and [insert-xxx]

Besides from inserting before/after, and appending children nodes, these three Active events works 100% identically. So let us have a look at how they actually work, and how we can parametrize them.

So far, we have only used *"static sources"*. A static source, is a bunch of static nodes, being children of the **[src]** node. However, you can also supply an expression, leading to another node-set as its **[src]**.

Imagine I have a node-set, which I want to copy, into some destination.

```
_src
  foo1:bar1
  foo2:bar2
_dest
add:x:/@_dest
  src:x:/@_src/*
```

After execution of the above Hyperlambda, the **[_dest]** node, will have a copy of all children from **[_src]**.

Both the **[add]** and the **[insert-xxx]** Active Events, can be given multiple **[src]** arguments. Imagine something like the following for instance.

```
_src1
  foo1:bar1
_src2
  foo2:bar2
_dest
add:x:/@_dest
  src:x:/@_src1/*
  src:x:/@_src2/*
```

Of course, the above could also be accomplished by using a boolean algebraic expression instead. However, the simplified syntax of using multiple **[src]** nodes, sometimes outweighs the benefits of the condensed syntax using algebra.

Notice though that **[set]** can only handle one **[src]** argument.

## Multiples destinations

All of the above Active Events can be given multiple destinations. This is a general pattern in P5, which allows you to do multiple things, with one invocation. We saw this in a previous chapter, where we retrieved the values of two widgets, with a single invocation. Both **[set]**, **[add]** and **[insert-xxx]** have similar semantics. Try to run the following Hyperlambda in your Executor to see this for yourselves.

```
_data
_data
set:x:/../*/_data?value
  src:SUCCESS!
```

This feature means that you must be careful, to make sure you are only referencing one node, unless you want to risk having unintentional side-effects of your lambda. On the positive side, it is also a feature that allows you to *"do a lot, with a little"*.

## Deleting stuff

This leaves us with only one remaining concept we'll need to understand, before we can wrap up this chapter, having all four CRUD operations within our toolbelt - Which is deletion of stuff.

Deletion is extremely simple though. Simply use the **[set]** event, without a **[src]** argument. Considering the following.

```
_foo:bar
set:x:/@_foo
```

The above code will simply delete the **[_foo]** node entirely. If you supply a type declaration for your expression pointing to its value instead, its value will become *"null"*. If you point it to its name, its name will become the *"empty string"*. Consider the following.

```
_foo1:bar
set:x:/@_foo1?value
_foo2:bar
set:x:/@_foo2?name
```

## Wrapping up

You should now have a basic understanding of all four CRUD operations for nodes and lambda objects, allowing you to dynamically create and change lambda objects as you see fit. However, as we started out this chapter with, no other programming languages on this planet, contains any similar constructs to what you have been shown here. Hence, possibly the biggest problem you're now faced with, is creating a mental model for understanding, this very unique and highly useful idea ...

### Don't panic!

If things are unclear after having read through this chapter, just relax; Things will become more understandable as we proceed, and start using the constructs we learned in this chapter. As you gain a more thorough understanding of the art of *"molding lambda objects"*, you can come back to this chapter, and repeat the basics. This chapter have described, possibly one of the most difficult to understand concept in P5. As you get your hands on some real live examples, it will be much more easily understood.

### Video for this chapter

Feel free to watch [this video](https://www.youtube.com/watch?v=w7A4TcWHolk), which repeat some of the concepts we have gone through in this chapter. If you are reading this book in some sort of paper format, you can find the video here; https://www.youtube.com/watch?v=w7A4TcWHolk

[Chapter 7, Your first real application](chapter-7.md)