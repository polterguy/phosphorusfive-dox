# Lambda Expressions

This chapter contains some fairly advanced study subjects. If this is your first encounter with P5, you would probably benefit from skipping it for now, and rather move on the to [next chapter](chapter-6.md). Later when you wish to dive really deep into P5, you can come back to this chapter, to acquire an understanding of all the gory details.

Lambda expressions are what truly makes Hyperlambda unique. Hyperlambda is nothing like your traditional programming language. For instance, there doesn't even exist the notion of variables in Hyperlambda. This is because everything is changeable, and potentially a variable - Including Hyperlambda execution instructions. This allows you to create lambda objects, that changes their instruction set, during the execution of themselves. This opens up a whole new way of thinking in regards to programming, and does not, as far as I know, exist in any other programming execution platforms on the planet today. In fact, arguably, Hyperlambda is the *"weirdest"* programming language on the planet, and technically, it isn't even a programming language. Hence, if you should learn only two programming languages, Hyperlambda should probably be one of theme. Simply put, since it allows you to *"think differently"* in regards to code and programming, which widens your mind, and creates a larger general vocabulary, and understanding of the art of programming, in general.

## An overview of lambda expressions

A lambda expression, is type declared in Hyperlambda, with the type string of `:x:`. If you wish to create a lambda expression, you will hence have to make sure your node containing your expression, resembles something like the following; `_foo:x:/expression`. The `:x:` parts, makes sure the Hyperlambda parser, understands that the value of the previously defined **[_foo]** node is handled as an expression.

The correct scientific name for lambda expressions are; *"Hyperdimensional boolean algebraic graph object expressions"*, because they allow you to use boolean algebra, to create sub tree results, out of other tree objects, resulting in creating a hyperplane through your graph objects, which again results in retrieving a sub-portion of your tree structures. If you imagine your graph objects as a 2 dimensional structure, then lambda expressions allows you to create *"worm holes"* through these graph objects, that extracts a sub-portion of your tree, and yielding its results.

The expression itself, can contain several different segments, all of which are optional to declare.

* Zero or more *"iterators"*
* An expression type declaration
* A type conversion

All of the above mentioned segments are in fact optional, and the shortest possible legal expression you can create, is in fact completely empty, and would look like the following; `_foo:x:`. And empty expression like this, is often referred to as the *"identity expression"*.

The iterators of your expressions are said to be *"left associative"*, because they are evaluated in order of appearance, from left to right. Hence, you start out with the identity node, and apply zero or more iterators to it, to retrieve whatever result you are interested in retrieving. There are many different types of iterators, and in theory, they might even vary from implementation to implementation. However, the most common ones, are listed in the appendix at the end of this book. Each iterator though, reacts upon the results of its previous iterator, starting from left to right. Whenever an iterator yields a *"null result"*, the rest of the expression is discarded, and the expression as a while, will yield a *"null result"*. Each iterator starts with a *"/"*.

Below is a piece of Hyperlambda, intended to be executed in the Apps/Executor of your System 42 installation.

```
_foo
set:x:/@_foo?value
  src:Jo dude
```

The above code, uses the **[set]** Active Event, to change the `?value` of the first *"elder relative node"*, having the name of **[_foo]**, to *"Jo dude"*. After execution of the above Hyperlambda, your lambda object will have changed, and turned into the following;

```
_foo:Jo dude
set:x:/@_foo?value
  src:Jo dude
```

Notice how the value of **[_foo]** changed.

### Your expression's type declaration

All of your expressions have a type declaration. If omitted, a type of `?node` will be assumed. The type declaration, informs the expression engine, which part of your resulting node-set you are interested in. There are four different possible type declarations for your expressions.

* `?node` - The nodes' themselves, in their entirety
* `?value` - Only the nodes' value parts
* `?name` - The nodes' name
* `?count`- The number of nodes your result set contains

If you changed the above Hyperlambda, such that it had a `?name` type declaration for its expression, it would result in the following;

```
Jo dude
set:x:/@_foo?name
  src:Jo dude
```

Using **[set]**, you can also change the entire node, by using a `?node` type declaration, which is the default type declaration for your expressions, if you omitt the type declaration all together. Below is an example;

```
_foo
set:x:/@_foo
  src:"_bar:howdy"
```

An expression of type `?count` is read only though, and cannot be used as a destination for a **[set]** invocation for instance. It can however be used as the **[src]**. Try the following code to see an example of this.

```
_foo
set:x:/@_foo?value
  src:x:/../*?count
```

### Some common iterators

You could probably get away with understanding a handful of iterators, and never bothering your mind with any of the boolean algebraic parts of expressions, and still be able to create anything you wish to create, using P5. The most common iterators, you probably should at least teach yourself, is listed below.

* `/xxx` - Named nodes, filtering away anything not matching the specified *"xxx"* name
* `/n` - Numbered child node, returning the *n'th* child of the previous result set.
* `/..` - Returns the root node of your graph object, lambda structure
* `/*` - Returns all children nodes of the previous result set
* `/=xxx` - Nodes containing the specified *"xxx"* value, in their values

In addition to the above mentioned iterators, possibly the most important iterator, is the *"named elder relative"* iterator, which starts out with an *"@"*, for then to contain the *"xxx"* name of the node you wish to retrieve. This iterator, will look for the first node, amongst its elder sibling nodes first, for then to traverse upwards in its ancestor node hierarchy if not found, and yield the first node matching the specified *"xxx"* name, amongst either its direct ancestors, or its ancestors' *"elder sibling"* nodes.

Think of this iterator as an easy way to retrieve the first node, matching the specified name, within the *"scope"* of your currently executed lambda object. Below is an example of its use.

```
_foo
_bar
  _foo
set:x:/@_foo?value
  src:SUCCESS
```

Notice, after evaluation of the above Hyperlambda, only the first **[_foo]** node will have its value changed. This is because the second **[_foo]**, inside of our **[_bar]** node, is not an elder sibling, or direct elder relative in any ways, of the identity node of **[set]**, which is where our iterator starts out iterating, looking for a match.

If you tried something like the following though, only the last **[_foo]** node would have its value changed. This is because the *"named elder relative"* iterator, will stop iterating, once it finds its first match.

```
_foo
_foo
set:x:/@_foo?value
  src:SUCCESS
```

The named elder relative iterator, is probably the closest you come in P5 to something allowing you to reference nodes, in a *"variable fashion"* you might argue.

### Converting your expression's result

Optionally, you can convert the results of an expression, by appending a ".", and the type you wish to convert the results of your expression into. Imagine the following code, that copies the value from **[_foo]**, and puts it into **[_bar]**'s value, but converting it from a string, to an integer.

```
_foo:5
_bar
set:x:/@_bar?value
  src:x:/@_foo?value.int
```

### Creating a mental mind model for expressions

One way of realising what lambda expressions are, is to imagine them as the *"tree version of SQL"*. Where SQL allows you to extract two dimensional tables and data-sets, lambda expressions allows you to extract 3 dimensional relational stree structures, from another pre-existing tree structure. If you have some experience with XPath, they might come more natural to you.

For more about expressions, and iterators, please refer to the appendix section. However, I encourage you to read the appendix sections at last, since the contains the by far most advanced parts of the book, and might discourage you to continue reading, if you expose yourself to them too early.

- [Appendix, Expression iterators](appendix-expressions-iterators.md)
- [Appendix, Boolean algebra on expressions](appendix-expressions-boolean-algebra.md)

[Chapter 6, Changing your tree](chapter-6.md)