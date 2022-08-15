# Application Overview and Setup

## Learning Goals

- Setup a base Angular application.
- Describe how to break down a UI.

## Introduction

Let's begin by considering our component hierarchy. As we consider the wireframe
above, we can see multiple sections of the application:

1. We have two main "views" in the application:
   1. The "messaging" view, which lets the user view the message history for
      various conversations and send new messages
   2. The "contacts" view, which lets the user select which contacts they want
      to send a message to
2. At the top of both views, we have a "header" section, which provides login
   functionality and is persistent between views
3. Below the header in both views, we have an "application panel":
   1. On the contacts view, the application panel is fairly simple in that it
      has a header and a list of contacts, where each contact can be selected.
      Each contact will be its own component.
   2. On the messaging view, the application panel has multiple components in
      it:
      1. An area to control which conversation is active, the "conversation
         control" area
      2. An area to display the active conversation's history. Within the
         "conversation history" panel, we have:
         1. Messages from each sender who is not the current user
         2. Messages from the current user
         3. A control area to let the current user send a new message

All in all, we have a component structure that looks like this:

![Messaging Application Component Hierarchy](https://curriculum-content.s3.amazonaws.com/java-mod-8/ng-messaging-component-hierarchy.png)

## Start a new application

Let's create a new application called `flatiron-ng-messenger` by following the
same steps we followed with our previous project. First, let's create the
project with the Angular CLI:

```
ng new flatiron-ng-messenger --no-strict
```

> Note: the `--no-strict` option is give ourselves more flexibility with
> TypeScript and Angular as we build our project incrementally

Then let's install `bootstrap` so we can add some basic CSS styling and layout
to our application:

```
npm install --save bootstrap
```

As we did before, update the configuration of your project to make sure the
Bootstrap styles are usable:

- Look for the `angular.json` file in the base directory of your project:
  `<project-root>/angular.json`
- Look for the following entry:
  `projects->flatiron-angular->architect->build->options->styles`

![Bootstrap Configuration](https://curriculum-content.s3.amazonaws.com/java-mod-8/ng-basics-bootstrap-config.png)

- Add the following entry before the existing `src/styles.css`:
  - `node_modules/bootstrap/dist/css/bootstrap.min.css`
- Now you can use `styles.css` in your HTML just like you did before and Angular
  will resolve that to the entry you just configured in the `angular.json`
  configuration file
- Let's also add `bootstrap.bundle.main.js` to the `scripts` entry, which is
  right below the `styles` entry:

```json
            "scripts": [
              "node_modules/bootstrap/dist/js/bootstrap.bundle.min.js"
            ]
```

Let's make sure your configuration is correct and also clean up your
`app.component.html` file at the same time. Let's remove everything in
`app.component.html` and replace it with this simple div:

```html
<div class="contain p-3">
  <button type="button" class="btn btn-primary">Test button</button>
</div>
```

This should show you a simple button with bootstrap's default styling:

![Bootstrap Button Default Styling](https://curriculum-content.s3.amazonaws.com/java-mod-8/ng-bootstrap-default-button-styling.png)

## Bootstrap Styling Overview

Bootstrap is a powerful CSS framework and would be worthy of its own course.
We're going to cover the basics here so that we can leverage Bootstrap to give
our application a clean look and feel without having to do much CSS ourselves.

With Bootstrap, we can use rows and columns to structure content within a given
container. The default layout is divided in 12 columns and Bootstrap provides
classes to be able to assign any `div` element any number of columns.

Consider the following example:

```html
<div class="container">
  <div class="row">
    <div class="col-12 border p-3">
      <div class="contain">This column is 12 cells wide and has padding</div>
    </div>
  </div>
  <div class="row border">This row has no columns and no padding</div>
  <div class="row">
    <div class="col-1 border">This column is 1 cell wide</div>
    <div class="col-2 border">This column is 2 cells wide</div>
    <div class="col-3 border">This column is 3 cells wide</div>
    <div class="col-4 border">This column is 4 cells wide</div>
  </div>
  <div class="row">
    <div class="col-3 p-3">
      <button type="button" class="btn btn-primary">Test button</button>
    </div>
  </div>
</div>
```

It will give you the following output:

![Bootstrap Layout](https://curriculum-content.s3.amazonaws.com/java-mod-8/ng-bootstrap-layout.png)

Let's look at this sample layout code:

1. Bootstrap provides many built-in classes to control various aspects of your
   application's look and feel. We use a few basic ones in this example:
   1. `border` gives the corresponding element a `1px` solid line border all
      around - we use this here to make the layout more obvious
   2. `p-3` is an easy way to add `padding` to any element. The numerical value
      corresponds to a level of padding.
   3. (The same can be done with `m-3` for `margin`)
2. Each area of the application where you want to lay out a few elements should
   be inside a `container` div: `<div class="container"></div>`
3. Each row is defined with a `<div class="row"></div>` element and will
   automatically receive its own "line" of space in your layout
4. Inside each row, you have 12 columns worth of space available, which you can
   break up however you'd like
5. Here we have an example of a row with a single column that takes the entire
   12-cell width: `<div class="col-12 border p-3">`
6. We also have an example where the row is made up of several columns of
   different widths
7. Note that the columns on a given row do not have to take up the entire width
   of the row
