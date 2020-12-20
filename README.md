# Props Basics

## Overview

We'll take the next step with React components and examine how they can be used
as dynamic templates by using **props**.

## Objectives

1. Understand how React components can be dynamic templates
2. Create dynamic React components and show the HTML they create

## Introduction

As the building blocks of React applications, components are _dynamic_, in that
they can describe a template of HTML and fill in variable data. This lesson
builds a real example of a blogging application to illustrate dynamic
components.

We will use the following components:

- `BlogContent` - contains the content of the blog post
- `Comment` - contains one user's comment
- `BlogPost` - the 'top level' React component, which is responsible for rendering both
  `BlogContent` and `Comment`

### Making Components Dynamic

Time to put the **dynamic** aspect of components to use! Let's start with the
`BlogContent` component. The following snippet shows how we can describe
variables inside a component:

```javascript
function BlogContent(props) {
  return <div>{props.articleText}</div>;
}
```

You should see something new in the above code. Our function now takes an
argument called `props`. Also, inside the return statement, we have this funky
syntax: `{props.articleText}`.

This line is telling React to place the value that `props.articleText`
represents within the `<div>`. Ok, so where does `props.articleText` come from?

### Passing Information

React allows us to pass units of information from a parent component down to a
child component. We call these **props**, which we will dig more into in a later
lesson. Let's see how we can pass information from `BlogPost` down to its child
`BlogContent`:

```javascript
function BlogPost() {
  return (
    <div>
      <BlogContent
        articleText={
          "Dear Reader: Bjarne Stroustrup has the perfect lecture oration."
        }
      />
    </div>
  );
}
```

In the above, we see that when we render the `BlogContent` component, we also
create a prop called `articleText` that we assign a value of "Dear Reader:
Bjarne Stroustrup has the perfect lecture oration." This value is accessible
from within the `BlogContent` component as `props.articleText`!

**To create props, we write them the same way as writing attributes for an HTML tag.**

But remember, this is JSX and not HTML!

One more thing about props: they can be any data type! In our example, we pass a
string as a prop. But we can pass a number, boolean, object, function, etc. as a
prop!

### Props

Let's expand a bit on props here. Taking a look at both of our components will
give us a better understanding of how data can be passed from one component to another:

```js
// BlogPost.js
// PARENT COMPONENT
function BlogPost() {
  return (
    <div>
      {/* BlogContent is being returned from BlogPost */}
      {/* Therefore, BlogContent a child of BlogPost */}
      <BlogContent
        articleText={
          "Dear Reader: Bjarne Stroustrup has the perfect lecture oration."
        }
      />
    </div>
  );
}

// BlogContent.js
// CHILD COMPONENT
function BlogContent(props) {
  return <div>{props.articleText}</div>;
}
```

When one component _returns_ another component, this creates a special
relationship between these two components. The component being returned is the
_child_ component, and the component returning that child is the _parent_
component.

The only way for a _parent_ component to pass data to its _child_ components is
via **props**.

On this line:

```js
// BlogPost.js
<BlogContent
  articleText={
    "Dear Reader: Bjarne Stroustrup has the perfect lecture oration."
  }
/>
```

We are adding a **prop** of `articleText` to our `BlogContent` component.

If we add a `console.log` in the `BlogContent` component to inspect the props:

```js
// BlogContent.js
function BlogContent(props) {
  console.log(props);
  return <div>{props.articleText}</div>;
}
```

We'll see an **object** with **key-value pairs** related to the data we passed
down from the parent component!

```js
// BlogContent.js
console.log(props);
// => { articleText: "Dear Reader: Bjarne Stroustrup has the perfect lecture oration." }
```

We can add as many additional props as we want, by assigning them in the
parent component:

```js
<BlogContent
  articleText={
    "Dear Reader: Bjarne Stroustrup has the perfect lecture oration."
  }
  isPublished={true}
  minutesToRead={1}
/>
```

And all of these props will be added as keys on the props object in the child
component:

```js
// BlogContent.js
console.log(props);
/* 
  { 
    articleText: "Dear Reader: Bjarne Stroustrup has the perfect lecture oration.",
    isPublished: true,
    minutesToRead: 1 
  }
*/
```

Having the ability to share this data between components by passing _props_ down
to a child component from a parent makes our components incredibly flexible! For
example, here's how we could expand our `BlogContent` component based on those
additional props:

```js
function BlogContent(props) {
  console.log(props);

  // hide unpublished content
  if (!props.isPublished) return null;

  // show published content
  return (
    <div>
      <h1>{props.articleText}</h1>
      <p>{props.minutesToRead} minutes to read</p>
    </div>
  );
}
```

### Expanding our Application

We still need a `Comment` component that we can use for each comment in a
`BlogPost`. The `Comment` component would look something like:

```javascript
function Comment(props) {
  return <div>{props.commentText}</div>;
}
```

This component, when used, will display content that is passed down to it,
allowing us to pass different content to multiple `Comment` components. Let's
add them in. Of course, with components being re-usable, we can make as many as
we want:

```js
function BlogPost() {
  return (
    <div>
      <BlogContent
        articleText={
          "Dear Reader: Bjarne Stroustrup has the perfect lecture oration."
        }
      />
      <Comment />
      <Comment />
      <Comment />
    </div>
  );
}
```

...and just as before, we can pass content data down to them:

```js
function BlogPost() {
  return (
    <div>
      <BlogContent
        articleText={
          "Dear Reader: Bjarne Stroustrup has the perfect lecture oration."
        }
      />
      <Comment commentText={"I agree with this statement. - Angela Merkel"} />
      <Comment commentText={"A universal truth. - Noam Chomsky"} />
      <Comment
        commentText={
          "Truth is singular. Its ‘versions’ are mistruths. - Sonmi-451"
        }
      />
    </div>
  );
}
```

There is quite a bit going on here. Most notably, we are passing information
from a parent component to many child components. Specifically, we are doing
this by creating a prop called `commentText` to pass to each `Comment`
component, which is then accessible in each instance of `Comment` as
`props.commentText`. Let's expand the HTML that this would ultimately render:

```html
<div>
  <div>Dear Reader: Bjarne Stroustrup has the perfect lecture oration.</div>

  <div>I agree with this statement. - Angela Merkel</div>

  <div>A universal truth. - Noam Chomsky</div>

  <div>Truth is singular. Its ‘versions’ are mistruths - Sonmi-451</div>
</div>
```

...but seeing is believing so let's look at this in technicolor! Following is an
inspection of the _real live DOM elements_ that React rendered when we blasted
this code into a new application (classes, IDs, and minor CSS have been added
for a better visual display):

![completed example](https://curriculum-content.s3.amazonaws.com/react/completed-example-dynamic-components.gif)

Alright now! Take a moment. Stretch your limbs, make a sandwich, let the
glorious paradigm sink in. Dynamic components are a core facet of React
programming, and most of what we do as React programmers builds upon them.

## Summary

While HTML elements are the basic building blocks of a website, (for example, a
`<div>`), a React application usually consists of several React _components_
combined together. Unlike simple HTML elements, React components are smarter and
bigger. They allow you to do much more and incorporate logic into how content
displays.

**Components:**

- are modular, reusable, and enable a 'templating' like functionality
- help us organize our user interface's _logic_ and _presentation_
- enable us to think about each piece in isolation, enabling us to apply
  structure to complex programs

**Props:**

- are passed from a _parent component_ to a _child component_
- can be accessed in the _child components_ via an _object_ that is passed into
  our component function
- can hold any kind of data (strings, numbers, booleans, objects, even functions!)

## Looking Forward

In this lesson, we introduced some fundamentals of a React component. Going
forward we will expand on what we can do with components, how they fit into the
larger React landscape, and what built-in functionality they come with.

## Resources

- [Components and Props][react-component]

[react-component]: https://reactjs.org/docs/components-and-props.html
[bjarne-stroustrup]: https://www.youtube.com/watch?v=JBjjnqG0BP8
