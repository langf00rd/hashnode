## How To Create A Custom Mouse Pointer in HTML, CSS and JavaScript

In this tutorial, we'll see how to transform the standard mouse pointer into a fancy emoji that changes style when we click.

I will post a complete video tutorial on my [YouTube channel](https://www.youtube.com/langforddev), and you can view it there.

With that said, let's get coding!

## What we'll be building

![gif of final project](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/w9d0lhubk9vpf9ylc6hq.gif)
 
Start by creating these three files; `index.html`, `styles.css`, and `script.js`.

### The HTML Structure
Start by creating the standard HTML boilerplate code.

```
<!DOCTYPE html>
<html>
    <head>
        <title>Custom Mouse Pointer</title>
    </head>
    <body></body>
</html>

```

Then, in the `<link>` tag of our HTML file, we import the `styles.css`.

```
<!DOCTYPE html>
<html>
    <head>
        <link rel="stylesheet" href="styles.css" />
        <title>Custom Mouse Pointer</title>
    </head>
    <body></body>
</html>
```

Import the JavaScript file by setting the `src` of the `<script>` tag at the bottom of our HTML file to our `script.js` file.

```
<!DOCTYPE html>
<html>
    <head>
        <link rel="stylesheet" href="styles.css" />
        <title>Custom Mouse Pointer</title>
    </head>
    <body>
        <script src="script.js"></script>
    </body>
</html>
```

Finally, create a div with the class `pointer`. This element will be used in place of the default cursor. And since it’s an html element, we can apply numerous styles to it

```
<!DOCTYPE html>
<html>
    <head>
        <link rel="stylesheet" href="styles.css" />
        <title>Custom Mouse Pointer</title>
    </head>
    <body>
        <div class="pointer"></div>
        <script src="script.js"></script>
    </body>
</html>
```

That's all there is to the HTML file! You should get an empty page when you open the `index.html` file in your browser.

### Styling Our HTML

First, we set the background of our webpage to a light purplish color.

```
body {
    background: #8499ff;
}
```

We set the webpage's height and width to the maximum height and width of the device that is viewing the page.

```
body {
    ...
    height: 100vh;
    width: 100vw;
}
```

Then, by setting the `overflow` property to `none`, we prevent vertical and horizontal scrolling.

```
body {
    ...
    overflow: hidden;
}
```

Finally, we hide the pointer.

```
body {
    ...
    cursor: none;
}
```

You should have this for the `body`:

```
body {
    background: #8499ff;
    height: 100vh;
    width: 100vw;
    overflow: hidden;
    cursor: none;
}
```

We're now going to style the `pointer`. We will not style the pointer directly but rather the `::after` pseudo-class.

The `::after` pseudo-class selects content that comes after a selected element—allowing you to insert text after a specific tag, which is what we'll do in this tutorial.

```
.pointer::after {
    content: "🤩";
    font-size: 40px;
}
```

We set the `content` property in the code above to an emoji (🤩). This emoji will be our default cursor icon. The size is then increased to `40px` to make it a little bigger.

We change the default emoji every time the mouse is clicked to (😜). The class `pointer-clicked` class is created to accomplish this. This class will assign this class to the pointer in the JavaScript.

```
.pointer-clicked::after {
    content: '😜';
}
```

### Adding functionality with JavaScript

First select the pointer we created in the HTML with the `document.querySelector()` method

```
const pointer = document.querySelector(".pointer");
```

We have to listen for these two mouse events:
- **mousemove**: When the mouse pointer is moved
- **mousedown**: When the mouse pointer is clicked/pressed down

```
window.addEventListener("mousemove", onPointerMove);
window.addEventListener("mousedown", onMouseClick);
```

Lets create the callback functions for these event listeners.

```
const onPointerMove = (e) => {
    // on pointer move
}

const onMouseClick = () => {
    // on mouse click
}
```

When the actual pointer moves, we want to get its position and pass it to the pointer element we created in HTML.

```
const onPointerMove = (e) => {
    const mouseY = e.clientY;
    const mouseX = e.clientX;
    pointer.style.transform = `translate3d(${mouseX}px, ${mouseY}px, 0)`;
}
```

The `clientY` returns the vertical coordinate of the pointer relative to the viewport. The `clientX` property, on the other hand, returns the horizontal coordinate. 

In the `pointer.style.transform` line, we change the location of the custom pointer by assigning it the coordinates of the actual cursor. Smart move! 😊

When the mouse clicks, we add a new class called `pointer-clicked`. And then remove this newly created class after 150 milliseconds in the `setTimeout` function, resolving the pointer to its default state.

```
const onMouseClick = () => {
    pointer.classList.add('pointer-clicked')
    setTimeout(() => {
        pointer.classList.remove('pointer-clicked')
    }, 150)
}
```

At the end of everything, the `script.js` file should have this:

```
const pointer = document.querySelector('.pointer');

const onPointerMove = (e) => {
    const mouseY = e.clientY;
    const mouseX = e.clientX;
    pointer.style.transform = `translate3d(${mouseX}px, ${mouseY}px, 0)`;
}

const onMouseClick = () => {
    pointer.classList.add('pointer-clicked')
    setTimeout(() => {
        pointer.classList.remove('pointer-clicked')
    }, 150)
}

window.addEventListener("mousemove", onPointerMove);
window.addEventListener("mousedown", onMouseClick);
```

Now opening the `index.html` in your browser, you should see this!

![gif of final project](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/w9d0lhubk9vpf9ylc6hq.gif)

Code is available on [GitHub](https://github.com/langford-dev/custom-mouse-pointer/tree/main)

## Conclusion

That's it for this article.

If you found this article useful, consider following me on [Twitter](https://twitter.com/langford_dev) and signing up for my weekly [newsletter](https://www.getrevue.co/profile/langford_dev) for web and software development content.
