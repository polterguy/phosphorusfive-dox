# Permanently solving the "CRUD problem"

Since the general theme of our book so far, have been the creation of CRUD app, we're going to permanently solve that problem, by creating an app, that allows anyone, to create any CRUD apps they wish - While storing the data in a _"real"_ database - MySQL that is.

## Meet Camphora Five

Below is a screenshot of [Camphora Five](https://github.com/polterguy/camphora-five), which allows us to do just that.

![alt tag](screenshots/chapter-19-3.png)

In the above screenshot, I have created 4 different CRUD apps. As you create a CRUD app in Camphora Five, you can declare as many (or as few) columns as you wish, and you can choose which underlaying data type each column should have. The latter decides how items in your form are being edited, among other things.

## Architecture

Creating a fully fledged app like Camphora Five, which allows anyone to create their own apps, by going through a wizard form - Is simply not fit for the format of this book. Hence, instead of showing you every single line of code, I will walk through Camphora's architecture, from an abstract point of view - And the design decisions I made, as I created it.

First of all, I wanted users to be able to create _real apps_, and not rely upon generic templates too much. This allows you to modify an existing app, after you have created it, to create additional features in your app. Hence, what I do, as you generate your apps in Camphora, is actually to create a complete _"/modules/"_ folder for your app, containing the app, as you chose to create it.

This implies that after you have created a Camphora app, you've got a pretty nice starting ground, for modifying your app, to create additional features, using Hyperlambda as we've gone through it, from within this book.

Each app you create will hence have its own folder, with lots of Hyperlambda files within, which you can edit as you see fit. These files and folders can be found in the _"/template/"_ folder of Camphora Five's source code.

