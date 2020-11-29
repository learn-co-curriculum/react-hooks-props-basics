# Dynamic React Components


## Overview

We'll take the next step with React components and examine how they can be used
as dynamic templates.


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


#### Making Components Dynamic

Time to put the **dynamic** aspect of components to use! Let's start with the
`BlogContent` component. The following snippet shows how we can describe
variables inside a component:

```javascript
function BlogContent(props) {
  return (
    <div>
      {props.articleText}
    </div>  
  )
}
```

You should see something new in the above code. Our function now
takes an argument called `props`. Also, inside the return
statement, we have this funky syntax: `{props.articleText}`. 

This line is telling React to place the value that `props.articleText`
represents within the `<div>`. Ok, so where does `props.articleText` come
from?


#### Passing Information

React allows us to pass units of information from a parent component down to a
child component. We call these **props**, which we will dig more into in a later lesson.
Let's see how we can pass information from `BlogPost` down to its child
`BlogContent`:

```javascript
function BlogPost {
  return (
    <div>
      <BlogContent articleText={"Dear Reader: Bjarne Stroustrup has the perfect lecture oration."}/>
    </div>
  )
}
```
 
In the above, we see that when we render the `BlogContent` component, we also create a prop called `articleText` that we assign a value of "Dear Reader: Bjarne Stroustrup has the perfect lecture oration." This value is accessible from within the `BlogContent` component as `props.articleText`! To create props, we write them the same way as writing attributes for an HTML tag. But remember, this is JSX and not HTML! 

One more thing about props: they can be any data type! In our example, we pass a string as a prop. But we can pass a number, boolean, object, function, etc. as a prop! 

#### Expanding our Application

We still need a `Comment` component that we can use for each comment in a
`BlogPost`. The `Comment` component would look something like:

```javascript
function Comment(props) {
  return (
    <div>
      {props.commentText}
    </div>
  )
}
```

This component, when used, will display content that is passed down to it,
allowing us to pass different content to multiple `Comment` components.  Let's
add them in. Of course, with components being re-usable, we can make as many as
we want:

```javascript
function BlogPost() {
  return (
    <div>
      <BlogContent articleText={"Dear Reader: Bjarne Stroustrup has the perfect lecture oration."}/>
      <Comment />
      <Comment />
      <Comment />
    </div>
  )
}
```

...and just as before, we can pass content data down to them:


```javascript
function BlogPost() {
  return (
    <div>
      <BlogContent articleText={"Dear Reader: Bjarne Stroustrup has the perfect lecture oration."}/>
      <Comment commentText={"I agree with this statement. - Angela Merkel"}/>
      <Comment commentText={"A universal truth. - Noam Chomsky"}/>
      <Comment commentText={"Truth is singular. Its ‘versions’ are mistruths. - Sonmi-451"}/>
    </div>
  )
}
```

There is quite a bit going on here. Most notably, we are passing information
from a parent component to many child components. Specifically, we are doing this 
by creating a prop called `commentText` to pass to each `Comment` component, 
which is then accessible in each instance of `Comment` as `props.commentText`. 
Let's expand the HTML that this would ultimately render:

```html
<div>

  <div>
    Dear Reader: Bjarne Stroustrup has the perfect lecture oration.
  </div>

  <div>
    I agree with this statement. - Angela Merkel
  </div>

  <div>
    A universal truth. - Noam Chomsky
  </div>

  <div>
    Truth is singular. Its ‘versions’ are mistruths - Sonmi-451
  </div>

</div>
```

...but seeing is believing so let's look at this in technicolor! Following is an
inspection of the _real live DOM elements_ that React rendered when we
blasted this code into a new application (classes, IDs, and minor CSS have been
added for a better visual display):

<img src="https://curriculum-content.s3.amazonaws.com/react/completed-example-dynamic-components.gif" alt="completed example" />


Alright now! Take a moment. Stretch your limbs, make a sandwich, let the
glorious paradigm sink in. Dynamic components are a core facet of React
programming, and most of what we do as React programmers builds upon them.


## Summary

While HTML elements are the basic building blocks of a website, (for
example, a `<div>`), a React application usually consists of several React
_components_ combined together. Unlike simple HTML elements, React components
are smarter and bigger. They allow you to do much more and incorporate logic
into how content displays.

**React components:**
  - are modular, reusable, and enable a 'templating' like functionality
  - help us organize our user interface's _logic_ and _presentation_
  - enable us to think about each piece in isolation, enabling us to apply structure to complex programs


## Looking Forward

In this lesson, we introduced some fundamentals of a React component. Going
forward we will expand on what we can do with components, how they fit into the
larger React landscape, and what built-in functionality they come with.

## Resources
- [React Top-Level API](https://reactjs.org/docs/react-api.html)

[react-component]: https://reactjs.org/docs/components-and-props.html
[bjarne-stroustrup]: https://www.youtube.com/watch?v=JBjjnqG0BP8
