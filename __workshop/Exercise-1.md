# Questions

**With a partner**, answer these questions as completely as possible. Feel free to look at past lecture notes, the web, anything.

Take the time to explain it to each other.

The power of this exercise is in the act of _formulating_ and _explaining_ the concepts to someone else (your teammate).

## One

Run the app. Write out the steps, the _pseudo code_, required to create this app. It doesn't have to be totally accurate, or in the right order.

Only move on to the next question when you have enough detail that you would be able to start coding it yourself.

```
// Answer here
-- set up yarn instal and yarn dev and make sure your modules are on..
1. make a constant app that is used to call the express function
2. define a port
3.render pages upom request, those renders will point to pages with the right information.
4. once on the page, the css for that page is called upon to style the page. images are also called upon.
5. the html, footer and form are called upon by with the <%-includes-%> function within the embedded ejs page.
6. when the form is inputted, the array has the inputted 'item' which is in the forEach loop, updates on the page. it refreshes the page after each input.
7. in extra detail, the for each goes through each element in the items array and as a new item is inputted in the <li> tag..

define the port:

in order to avoid interference with other communications, we a specific pathway/ channel in which to communicate our browser and server. this is the port number. for ports, process.env.PORT is used for public use whereas || 8000 is only for local use.
```

## Two - `server.js`

Take a look at the `server.js` file.

We have a new module in there, `body-parser` that is required on line `4`. What is it for? What is its use-case? What other lines are related to this module?

_The NPM site might be a good place to start. Feel free to provide links as relevant._

```
// Answer here
body parser is a dependency in our json file. it appears to function within middleware and is called upon. body-parser is an object and functions with true
and false statements.
```

## Three - `server.js`

Look at lines `23` and `24`. Explain the methods used. How are they different? What are the usecases for each?

```
// Answer here
the .get allows for us to create a homepage and is rendered as "/". homepages have no other links associated with them like other pages.
-the const { handleHomePage, handleFormData, handle404 } = require('./handlers');
this above code has three functions that need to be called. the calls for these functions and their set-up is in the handlers.js page.


in handlers.js, we call the handle home, it renders the homepage and pass through it an empty object called items which has an empty array inside of it.

the .post line is used because it send feedback to our page each time an item is placed in our to do list which is the "req.body;". the res.redirect allows
us to refresh the page to update more information on our to do list. if you knock off res.redirect and add items to the list, it wont appear on your body. uuntil you refrwsh the page...


const handleFormData = (req, res) => {
    const { item } = req.body;
    items.push(item);

    res.redirect('/');
}
```

## Four - `server.js`

Line `6`. That's new. What do you think it's for?

```
// Answer here
essentially, you want to keep the server file clean and ordered, therefore, we use the new file, handlers.js to store functions and their codeblocks. in this method, we can clearly organize functions and their function calls.
```

## Five - `handlers.js`

Explain line `1`. Where, why and how is `items` being used?

```
// Answer here
items is used in our to do inputs. it is an empty array and only has items pushed into it when we add them. the page refreshes every time an item is added to it.each time a new item is added to our to do list the header.js adds a new list item to the page.
```

## Six - `handlers.js`

Why is there `redirect` on line `11`;

```
// Answer here
the "/" redirect button allows us to refesh the page instantaeously after each new item is added to our list form.
```

## Seven - `handlers.js`

The `handle404` function is a more complex than we've seen thus far, what is the extra functionality for?

```
// Answer here

if a user does not find a home page, there are multiple ways for the error 404 to respond. at first, the intial if statement explains that if the request accepts the html code, it will respond with the fourOHfour page. ejs with the created html output explaining the 404 message. the { path: req.originalUrl });
is found on the ejs file with the <%-path %> function. this is how to get linked to our first path and req.accepts('html) is true. the <% path%> allows us to say which /path the user placed and was not expecting.


const handle404 = (req, res) => {
    res.status(404);

    // respond with html page
    if (req.accepts('html')) {
        res.render('pages/fourOhFour', { path: req.originalUrl });
        return;
    }

    // respond with json
    if (req.accepts('json')) {
        res.send({ error: 'Not found' });
        return;
    }

    // default to plain-text. send()
    res.type('txt').send('Not found');
}
```

## Eight - `ejs`

Take a look at `homepage.ejs` and `todoInput.ejs`. What is happening in there? Explain line-by-line...

```
// Answer here
homepage.ejs//
the homepage ejs begins with an <%-includes%> fnction that links the partial of a normal html page.
afterwardswe create a div and use the <%-includes%> function to link the partials todoinput. the div closes and a new div is opened
which creates an unordered list with a forEach loop in it. the forEach loop goes through every item in items and produces a new list for when it is inputted in the input box.
the footer is <%-includes%> with another partial

the todoinput.ejs is a simple form tag allows a user to input any words into the input box to then make it be placed in the list form. this form also links us to the server file and handler js file with the method"POST" call and the action'/form-data'. this allows for the page to refresh each time a new list item is added to our form.
```

## Nine - `styles.scss`

What are lines `2` to `7` for this file? Where are these values being used? Take a look at `_homepage.scss` as well? What do you notice?

```
// Answer here
line 2 and 7 are variables that have assigned values to them which then allows us to reference them continusolsy throughout our scss page. this will allow us to use the same value continusoly without making px or color mistakes.

for the _homepage.scss we use the .input-container class and includes the element tags from the container within the {} of input container. its a short hand of influencing all the children of my container which is the label element. it gets all the descendants no matter how deeply embeded it is.

the &-- notation references the list items and ensures each new list item shares the same structure.

the functionality of the &-- notation IS A SHORTHAND NOTATION


.todo-list {
    background: $bg-color;
    border: 1px solid $border-color;
    width: 400px;
    min-height: 600px;

    &--item {
        border-bottom: 1px solid $border-color;
        padding: 10px 14px;
    }
    //this can be written instead as .todo-list--item... which is longer...
}
```

## Ten - `_homepage.scss`

Line `16`. See if by searching the Sass documentation, you can determine what _exactly_ is going on here. That `#{}` notation very specific to this use-case. Why?

```
// Answer here
    width: calc(#{$content-width} - 60px); content-width is a variable with a preset variable to it... the width now is a mathimatical equation that adjusts the width specifically to input section of label. calc allows you to calculate the variables with pixels involved.

```
