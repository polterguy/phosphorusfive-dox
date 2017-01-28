# Your first real application

Whoa, finally we are going to create something useful! In this chapter, we will create a contacts application, allowing us to keep track of our friends, their emails, and phone numbers.

Normally, the chapters for this book is written such that every second chapter is an *"advanced topic"*. However, since out previous chapter was in fact quite an advanced chapter, yet still not labeled as such, you can now at least to some extent, pull down your guard, breathe slowly, realizing you're about to embark on something important; **The creation of a useful Ajax web application!**

Before we can dive into our application though, there are some few constructs we'll need to understand first;

* Loading and saving of files
* Parts of the folder structure of Phosphorus Five
* The **[apply]** Active Event
* Widget lambda events

## Loading and saving files

In P5, there are two important events for loading and saving files. These are **[load-file]** and **[save-file]**. Before we start using them though, we'll need to have a look at the folder structure of P5.

If you open up the folder *"/phosphorusfive/core/p5.webapp/"* and have a look at it, then this is the main root folder for your web application. The most important folder within this folder for this chapter is called *"users"*. This folder will contain one folder for each user you have in your P5 installation. By default, P5 only has one user, which is your *"root user"*.

Inside of your user's folder, you can find a *"documents"* folder. This is the equivalent of *"Your documents"* in windows, or *"Home"* on Linux. This is important to understand, since we will store our data, in a file, inside of this folder.

Your *"documents"* folder though, contains two other folders. One *"private"* folder, and another *"public"* folder. We will be using the *"private"* folder, to store a file, containing the data for our CRUD application, which we will be creating during this chapter. Files inside of this folder, cannot in general, be accessed by anyone, except the user whom these files belongs to. Hence, they are *"private files"*.

To create a file inside of this folder, can be done by using a tilde `~`. If you start out a filename with a tilde, this will automatically save a file to your user's home folder. Meaning, if we want to create a file inside of our private document folder, we can do so with the following code;

```
save-file:~/documents/private/foo.txt
  src:Hello filesystem!
```

If you execute the above code in your Apps/Executor, it will create a simple text file for you, inside of your private folder. To understand why, realize that the tilde `~` will be substituted with *"/users/your-username"*, before the file is saved. Since the root folder everything related to files is the main root web application folder, this means your file can be found within *"/phosphorusfive/core/p5.webapp/users/root/documents/private/"* - Where ever that is locally within your system.

## The [apply] event

The **[apply]** Active event, is kind of like the *"superman version"* of **[add]** and **[insert-xxx]** from our previous chapter. It allows you to take a data source, and combine it with a template, to create an entire hierarchy of nodes, and append into some destination.

We will be using this Active Event, to dynamically create an HTML table, from the content of your data file, containing the *"database"* for your contacts.

## Widget lambda events

As vaguely touched upon in one of our first chapters, a widget can associate Active Events with itself. These are *"local"* events, that are only existing, for as long as the widget itself exists. We will create on widget lambda event like this, to *"databind"* our HTML table, containing our contacts, created from our *"database file"*.

## The code for our application

With these concepts, at least partially covered, let's move on to the code, and show you the entire listing for an *"Address book"* Ajax web application. Create new new *"lambda"* page, and make sure you replace the existing code, with the code listed below.

```
/*
 * Creating our main application wrapper widget.
 * This widget contains at the very least our "add contact" button, 
 * in addition to also possible an HTML table, dynamically created, 
 * according to the content of our "database file".
 */
create-widget:app_wrapper
  parent:content
  class:col-xs-12 text-right
  oninit

    /*
     * Making sure we initially databind our address HTML table, 
     * by invoking our "widget lambda event", that is declared 
     * further down on page.
     */
    sys42.examples.databind-addresses

  widgets

    /*
     * This becomes the wrapper widget for our HTML table, 
     * containing our "list of contacts".
     */
    container:table_wrapper
      class:text-left

    /*
     * This becomes our "create new contact button".
     */
    literal:add_btn
      element:button
      class:btn btn-default
      innerValue:+
      style:"width:200px;"
      onclick

        /*
         * Using a "wizard window" to retrieve name, 
         * email and phone from user.
         */
        sys42.windows.wizard
          header:Supply contact information
          body:<p>Please supply the details for your record</p>
          data
            name
            email
            phone
          .onok

            /*
             * Temporary variable containing the content of our "database".
             */
            _content

            /*
             * Retrieving data supplied by user.
             */
            sys42.windows.wizard.get-values

            /*
             * Loading database file, if it exists, and appending 
             * its old values into our [save-file] invocation.
             */
            file-exists:~/documents/private/adr.hl
            if:x:/@file-exists/*?value

              // File exists, appending content into [_content] below.
              load-file:~/documents/private/adr.hl
              add:x:/../*/_content
                src:x:/@load-file/*/*

            /*
             * Then appending the values supplied by user for new record.
             * Notice, we append the entire [sys42.windows.wizard.get-values] 
             * node, for then to later change its name to [item].
             */
            sys42.windows.wizard.get-values
            add:x:/@_content
              src:x:/@sys42.windows.wizard.get-values
            set:x:/@_content/*/sys42.windows.wizard.get-values?name
              src:item

            /*
             * Converting our [_content] node's content to Hyperlambda (string),
             * and saving it to disc.
             */
            lambda2hyper:x:/@_content/*
            save-file:~/documents/private/adr.hl
              src:x:/@lambda2hyper?value

            /*
             * Making sure we databind our HTML table again, to make sure 
             * our newly added record is shown.
             */
            sys42.examples.databind-addresses

  /*
   * This is our "widget lambda events".
   */
  events
  
    /*
     * The "databind" table event.
     *
     * This Active Event simply loads our "database file", and creates 
     * our HTML table accordingly.
     *
     * The first line in our event, becomes its name, meaning we can 
     * invoke it by simply adding a node with a name matching this 
     * Active Event's name.
     */
    sys42.examples.databind-addresses

      /*
       * This invocation clears our HTML table wrapper widget for 
       * any previous content.
       */
      clear-widget:table_wrapper

      /*
       * Here we check if our "database file" exists.
       */
      file-exists:~/documents/private/adr.hl
      if:x:/@file-exists/*?value

        /*
         * There exists a database.
         * Loading it, and creating our HTML table accordingly.
         */
        load-file:~/documents/private/adr.hl

        /*
         * Notice, here we use [apply], to dynamically append to our 
         * [create-widget] invocation's children [widgets].
         */
        apply:x:/..if/*/create-widget/*/widgets/*/container/*/widgets
          src:x:/@load-file/*/*
          template
            container
              element:tr
              widgets
                literal
                  element:td
                  {innerValue}:x:/*/name?value
                literal
                  element:td
                  {innerValue}:x:/*/email?value
                literal
                  element:td
                  {innerValue}:x:/*/phone?value

        /*
         * Now our "tbody" HTML widget below should contain on "tr" widget 
         * for each row from our "database file".
         * Each "tr" widget again, should contain one "td" widget for the name,
         * email and phone from our contact.
         */
        create-widget:contacts_table
          parent:table_wrapper
          element:table
          class:table table-striped
          widgets
            literal
              element:thead
              innerValue:<tr><th>Name</th><th>Email</th><th>Phone</th></tr>
            container
              element:tbody
              widgets
```

Although most of the above are things we have already covered, there are some new concepts, which we will have to walk through, in order to understand everything that's going on.


