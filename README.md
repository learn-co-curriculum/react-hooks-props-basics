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
  - `BlogPost` - the 'top level' React component, which is responsible for rendering both `BlogContent` and `Comment`


#### Making Components Dynamic

Time to put the **dynamic** aspect of components to use! Let's start with the
`BlogContent` component. The following snippet shows how we can describe
variables in our components' `render()` methods:

```javascript
class BlogContent extends React.Component {
  render() {
    return (
      <div>
        {this.props.articleText}
      </div>  
    )
  }
}
```

You should see something new in the above code. Inside of `render()`'s return
block, we have this funky syntax: `{this.props.articleText}`. Quite clearly not
HTML, this is instead React's special JSX syntax (more on JSX later). 

This line is telling React to place the variable `this.props.articleText` within
the `<div>`. Ok, so where does `this.props.articleText` come from?


#### Passing Information

React allows us to pass information from a parent component down to a child
component. We call these **props**, which we will dig more into later. Let's see
how we can pass information from `BlogPost` down to its child `BlogContent`
component:

```javascript
class BlogPost extends React.Component {
  render() {
    return (
      <div>
        <BlogContent articleText={"Dear Reader: Bjarne Stroustrup has the perfect lecture oration."}/>
      </div>
    )
  }
}
```

In the above, we see that when we render the `BlogContent` component, we also
assign a value to 'articleText'. This value accessible from within the
`BlogContent` component as `this.props.comment`!

#### Expanding our Application

We still need our `Comment` components. Let's add them in. Of course, with
components being re-usable, we can make as many as we want:

```javascript
class BlogPost extends React.Component {
  render() {
    return (
      <div>
        <BlogContent articleText={"Dear Reader: Bjarne Stroustrup has the perfect lecture oration."}/>
        <Comment />
        <Comment />
        <Comment />
      </div>
    )
  }
}
```

...and just as before, we can pass the their content down:


```javascript
class BlogPost extends React.Component {
  render() {
    return (
      <div>
        <BlogContent articleText={"Dear Reader: Bjarne Stroustrup has the perfect lecture oration."}/>
        <Comment commentText={"I agree with this statement.<br/>- Angela Merkel"}/>
        <Comment commentText={"A universal truth.<br/>- Noam Chomsky"}/>
        <Comment commentText={"Truth is singular. Its ‘versions’ are mistruths.<br/>- Sonmi-451"}/>
      </div>
    )
  }
}
```

There is quite a bit going on here. Most notably, we are passing the information
to the children components. Let's expand the HTML that this would ultimately render:

```html
<div>

  <div>
    Dear Reader: Bjarne Stroustrup has the perfect lecture oration.
  </div>

  <div>
    I agree with this statement.<br/>- Angela Merkel
  </div>

  <div>
    A universal truth.<br/>- Noam Chomsky
  </div>

  <div>
    Truth is singular. Its ‘versions’ are mistruths<br/>- Sonmi-451
  </div>

</div>
```

...but seeing is believing so let's look at this in technicolor! Following is an
inspection of the HTML and _real live DOM elements_ that React rendered when we
blasted this code into a project (classes, IDs, and minor CSS has been added for a better visual display):

<object data="https://learn-verified.s3.amazonaws.com/sample-component-video.gif" type="image/png">
  <img src="./completed-example.gif" />
</object>


Alright now! Take a moment. Stretch your limbs, make a sandwich, let the
glorious paradigm sink in. Dynamic components is a core facet of React
programming, and most of what we do going forward is going to build upon this
component parent-child paradigm.


## Summary

**React components:**
  - are modular, reusable, and enable a 'templating' like functionality
  - help us organize our user interfaces _functionality_ and _presentation_
  - enable us to think about each piece in isolation, improving our ability to assert structure on increasingly complex programs

While HTML elements are the basic building blocks of an application (for
example, a `<div>`), a React application usually consists of several React
_components_ combined together. Unlike simple HTML elements, React components
are smarter and bigger. They allow you to do much more and incorporate logic
into how content displays.


## Looking Forward

In this README, we introduced some fundamentals of a React component. Going forward we will expand on what we can do with components, how they fit into the larger React landscape, and what built in functionality they come with.


## A Quick Note About the Past...

React is a living framework that is constantly being updated and improved upon.
Compounding on that, React has spanned the transition from ES5 to ES6, (the
newer version of which has had many updates, including `Class` syntax). This
means old versions of React code will, in some places, look different.

In older versions a method, `React.createClass()`, was used in place of where we
were defining our own `Class`es and extending the `React.component` class (see
code above!). While this `React.createClass()` method of creating React
components has since been deprecated, it is still present in many older code
bases and tutorials. 

For now, we recommend sticking with the up-to-date class syntax we present, but
don't be alarmed if you come across unfamiliar ways to create React components.
The [React documentation][old-react] is always there for you regarding backwards
compatibility.

## Resources
- [React Top-Level API](https://reactjs.org/docs/react-api.html)

[old-react]: https://reactjs.org/docs/react-without-es6.html
[react-component]: https://reactjs.org/docs/components-and-props.html
[bjarne-stroustrup]: https://www.youtube.com/watch?v=JBjjnqG0BP8
