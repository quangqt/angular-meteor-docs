{{#template name="tutorials.socially.angular1.step_00.md"}}

Let's start building our Meteor Angular 1 Socially app.

In this step, we will:

- Setup Meteor and create an app
- Become familiar with the app's structure
- Connect an Angular 1 front end
- Run the application in the browser

# Meteor Setup

First step — let's install Meteor!

Open your command line and paste this command:

    $ curl https://install.meteor.com/ | sh

> If you are on a Windows machine, go [here](https://www.meteor.com/install) to install Meteor.

Now let's create our app — write this in the command line:

    $ meteor create socially

Now let's see what we got. Go into the new folder:

    $ cd socially

Run the app like so:

    $ meteor

    => Started proxy
    => Started MongoDB.
    => Started your app.

    => App running at: http://localhost:3000/

Now go to [http://localhost:3000/](http://localhost:3000/)
and look at the amazing app that's running on your computer!

We now have a fully functional app which includes both a server and a client!

The default Meteor app starts life with four files, two `js`, one `html` and one `css` file.

We are going to add our own files for this tutorial. So let's start by deleting the following files:

    - client/main.css    (delete)
    - client/main.html   (delete)
    - client/main.js     (delete)
    - server/main.js     (delete)

Now we can start building our app.

Create a new `index.html` file and place this code inside. Then run the app again.

{{> DiffBox tutorialName="meteor-angular1-socially" step="0.3"}}


Note that there is no `<html>` tag and no `<head>` tag - it's very simple.

This is because of how Meteor structures and serves files to the client.

Meteor scans all the HTML files in your application and concatenates them together.

Concatenation means merging the content of all `HTML`, `HEAD` and `BODY` tags found inside these HTML files together.

So in our case, Meteor found our `index.html` file, found the `BODY` tag inside and added it's content to the `BODY` tag of the main generated file.

> (right-click -> inspect element on the page of your Meteor app in the browser to see the generated file)


# Adding Angular 1

It's time to add Angular 1 to our stack!

Because we decided to work with AngularJS in the client side, we need to remove the default UI package of Meteor, called `Blaze`.

We also need to remove Meteor's default ECMAScript2015 package named `ecmascript` because Angular-Meteor uses a package named `angular-babel` in order to get both ECMAScript2015 and [AngularJS DI annotations](https://github.com/olov/ng-annotate).

So let's remove it by running:

    $ meteor remove blaze-html-templates
    $ meteor remove ecmascript

Now let's add the Angular 1 package to Meteor, back in the command line, launch this command:

    $ meteor npm install --save angular angular-meteor
    $ meteor add angular-templates pbastowski:angular-babel

That's it! Now we can use Angular 1's power in our Meteor app.

# HTML

To start simple, create a new file called `main.html` under the project's client folder, this will be our main `HTML` template page.

Then move the `p` tag from `index.html` into it:

{{> DiffBox tutorialName="meteor-angular1-socially" step="0.7"}}

Now let's include that file into our main `index.html` file:

{{> DiffBox tutorialName="meteor-angular1-socially" step="0.8"}}


But if you load this in your browser, **you won't see anything**. That's because we still need to **create the actual Angular app**, which we'll do next.

> Note: **paths are absolute, not relative!** You should always specify a full path regardless which file you're at. The path will begin from the app's root dir.

> E.g. let `main.html`, a file in the app's root dir, should be loaded like so:

    <div ng-include="'main.html'"></div>

# Building The Angular 1 App

Angular 1 apps are actually individual modules. So let's create our main module.

Create a new `main.js` file on the project's root folder.

Here you see another example of Meteor's power and simplicity - no need to write boilerplate code to include that file anywhere. Meteor will take care of it by going through all the files in the `socially` folder and including them automatically.

One of Meteor's goals is to break down the barrier between client and server, so the code you write can run everywhere! (more on that later).
But we need Angular 1's power only in the client side, so how can we do that?

There are a few ways to tell Meteor to run code only on the client/server/mobile side.

The simplest way is to use - [Meteor.isClient](http://docs.meteor.com/#/full/meteor_isclient) variable.
Everything inside this `if` statement will only run on the client side.

We recommend you to use special directories to keep files in the right place. To read more about it, you can go to [*"Application structure"*](http://guide.meteor.com/structure.html#special-directories) chapter of The Official Meteor Guide.

And let's continue defining our Angular 1 application module. Give it the name `socially` and add `angular-meteor` module as a dependency:

{{> DiffBox tutorialName="meteor-angular1-socially" step="0.9"}}

As you can see, we imported two modules, `angular` and `angular-meteor`.
Since the second one exports the name of angular module it easier to add it as a dependency.

And use the same application name in the `ng-app` directive in `index.html`:

{{> DiffBox tutorialName="meteor-angular1-socially" step="0.10"}}

Now run the app.

Everything is the same, so now inside our `main.html` let's add an Angular 1 expression:

{{> DiffBox tutorialName="meteor-angular1-socially" step="0.11"}}

Run the app again and the screen should look like this:

    Nothing here yet!

Angular 1 interpreted the expression like any other Angular 1 application.

# Experiments
Try adding a new expression to the `main.html` that will do some math:

    <p>1 + 2 = {{dstache}} 1 + 2 }}</p>

# Done!
Go to [step 1](/tutorial/step_01) to add some content to our application.

{{/template}}
