# Eval is not (necessarily) evil

Douglas Crockford, the inventor of JSON, once famously said *"eval is evil"*. When it comes to JavaScript, Douglas might be right. However, in Hyperlambda, eval is not necessarily evil - *Unless* you consume it mindlessly.

The **[eval]** Active Event is arguably the *"definition of Hyperlambda"*. In fact, when you execute a lambda object, what you're doing, is passing in a lambda object to **[eval]**. So **[eval]** is probably the most important Active Event in Hyperlambda.

In our previous chapter, we looked at Active Events. To understand **[eval]**, is to realize that an Active Event, such as the ones we created in our previous chapter - Is really nothing but a lambda object, stored in memory, easily **[eval]**'ed, through its name. This implies, that to **[eval]** a lambda object, is identical to invoking an Active Event.

## Eval defined

The **[eval]** Active Event, allows you to invoke a lambda object, and execute it, as if it was an Active Event. With that in mind, let's use **[eval]** in some code. Paste in the following code into your Apps/Executor.

```
.exe
  sys42.windows.info-tip:x:/../*/txt?value
eval:x:/@.exe
  txt:Jo world!
```

As illutrated above, you can easily pass in arguments to your lambda objects. You can also return arguments from **[eval]**, the same way you do from your normal Active Events. In fact, when you invoke an Active Event, P5 internally uses the **[eval]** Active Event to execute your event.

Combined with the ease of transforming between *"plain text"* and lambda objects that the **[lambda2hyper]** and **[hyper2lambda]** Active Events gives you - This easily allows you to execute literally *anything!*

If you have a Hyperlambda file somewhere for instance, you can easily execute it, and even pass in arguments into it, by doing something similar to the following.

```
// WARNING; This code will not execute correctly.
// Since the file "/foo.hl" does probably not exist on your system.
// It is simply an example of what you COULD do, to "execute" a file, 
// as if it was a "function".

load-file:/foo.hl
eval:x:/@load-file/*
  some-argument:Foo bar
```

The execution of a file, like we illustrated above, might also in fact return arguments. This means that there is very effectively *no semantic difference* between a lambda object, a file, some text fetched from some database, or supplied by a web service invocation - Or for that matter a piece of string, supplied by the user, through some input element in your app.

In fact, the last point largely defines the implementation of the Apps/Executor. The Executor in P5, simply converts your input to a lambda object, using **[hyper2lambda]**, and invokes this lambda object, using the **[eval]** Active Event.

## [eval] overloads

There actually exists three different versions of **[eval]**.

* [eval] - Plain old eval
* [eval-whitelist] - "Sandboxed" version of **[eval]**
* [eval-mutable] - Allows access to entire root lambda object

The first one, which is probably your most important version, actually creates a *copy* of the object(s) you wish to execute, and executes these copies. This is crucial to its implementation, considering how the invocation of a lambda object, potentially changes the state of that object.

Unless **[eval]** had created this copy, and executed the copy of your lambda, it would imply that the execution of an Active Event, potentially entirely changed your Active Event - Which of course would make your system become extremely unpredictable.

You can easily execute multiple lambda objects with **[eval]** in one go. Below is an example.

```
.exe
  sys42.windows.info-tip:Jo world!
.exe
  sys42.windows.confirm
    header:Foo bar
    body:Nope!
eval:x:/../*/.exe
```

If you pass in any arguments to your **[eval]** above, then each lambda object invoked, will have its own copy of your arguments. You can also have multiple lambda objects return values, such as the following illustrates.

```
.exe
  return
    first-name:Thomas
.exe
  return
    last-name:Hansen
eval:x:/../*/.exe
```

If you wish, you can instead of providing an expression to a lambda object, also supply the lambda object *"inline"* to your **[eval]** invocation, such as the following illustrates.

```
eval
  sys42.windows.info-tip:Hello world!
```

### Sandboxing your lambda

The **[eval-whitelist]** version, works similarly to the plain **[eval]** - Except that it expects a *"whitelist"* supplied as an **[events]** argument, that your lambda object can legally invoke. This creates a *"sandbox"* environment for you, where you can execute a lambda object, supplied over for instance an HTTP web service, by an untrusted client, without running the risk of having the client executing malicious events. Imagine the following.

```
.exe
  return:Safely executed by [eval-whitelist]
eval-whitelist:x:/@.exe
  events
    return:Jo world
```

If you tried to add any Active Event into the above **[.exe]** lambda object, that does not exist in the **[events]** argument, an exception would be raised, and the code would be aborted. This allows you to provide an *explicit* set of legal *"whitelisted"* Active Events to some lambda object, enforcing it to obey by a subset of your server's vocabulary of Active Events. The code below for instance, will abort the execution, once it reaches the **[foo]** node, since **[foo]** is not in the list of legal **[events]**.

```
.exe
  foo
  return:Safely executed by [eval-whitelist]
eval-whitelist:x:/@.exe
  events
    return:Jo world
```

This construct, is the reasons why we say that *"In Hyperlambda, eval is not necessarily evil"*.

When you have a piece of code, that you're not entirely sure if you should trust - Then you should definitely run it through some whitelist, using something similar to the above. This ensures the code does not harm your system in any ways.

Notice though, that sometimes one Active Event invokes another Active Event. Imagine if we wanted to whitelist the **[sys42.windows.info-tip]** Active Event for instance. Well, this even, invokes a whole range of other events. So simply legalizing the **[sys42.windows.info-tip]** event, would not be enough. Below is an example of some piece of code, that will *not* execute.

```
.exe
  sys42.windows.info-tip:Doesn't work!
eval-whitelist:x:/@.exe
  events
    sys42.windows.info-tip
```

If you wish to have the above code execute legally, you'll have to *"whitelist"* all events that your **[sys42.windows.info-tip]** event possibly invokes. An example of how to do that, with the current version of P5, is shown below.

```
.exe
  sys42.windows.info-tip:Probably works!
eval-whitelist:x:/@.exe
  events
    sys42.windows.info-tip
    eval
    add
    src
    if
    operators
    fetch
    eval-mutable
    p5.web.widgets.exists
    eval-x
    p5.web.widgets.create-container
```

Notice, that if the implementation of **[sys42.windows.info-tip]** later changes, the above lambda will *stop working*! Simply changing the **[p5.web.widgets.create-container]** to one of its aliases, **[create-container-widget]**, or **[create-widget]**, inside of the event - Will make your whitelist fissle.

This ensures, that as your system grows, and changes - You do not risk having malicious, unintentional code, execute as a consequence. Which is hopefully something you will come to appreciate, after you've used the system for a while.

[Chapter 13, Hyperlambda leads to Hyperhumble](chapter-13.md)
