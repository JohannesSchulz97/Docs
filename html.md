## HTML Basics

### Elements and Structure

- HTML consists of a hierarchical forest structure of elements inside other elements. Elements that can hold content (**container elements**) can be created with the following syntax, here tag is the keyword that specifies the type of element to be created:

    ```html
    <tag> 
        content inside the element 
    </tag>
    ```

- Elements can also be **self-closing**:

    ```html
    <img src="image.jpg" alt="Example">
    ```

- An HTML element can have so-called **attributes** to specify additional properties of the given element, like the `src` and `alt` attributes in the example above.

### JavaScript Integration

- JavaScript can be used inside HTML within the `<script>...</script>` element:

    ```html
    <script>
      console.log("Hello, World!");
    </script>
    ```

### High-Level Structure

1. On the top level, each HTML document needs to first define the document type inside the self-closing `<!DOCTYPE ...>` element. The exclamation mark here signals special content. (It is also used to create comments: `<!-- comment here -->`).
2. Then the **HTML root element** is defined, inside which all further elements will be contained. Inside the root element, we can find two elements, `head` and  `body`.
The `head` element contains information for the browser, while the `body` element is intended to store user content:

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8">
        <title>My Document</title>
      </head>
      <body>
        <h1>Hello, World!</h1>
      </body>
    </html>
    ```

### Some Important Elements

- `<p>...</p>` creates a paragraph of text
- `<div>...</div>` creates a *container* to group together other elements

To create a list of elements use the following syntax:
```html
  <ul>
    <li> item1 </li>
    <li> item2 </li>
  </ul>
  ``` 
  Here, the `<ul>` keyword creates an unordered list (bullet points). To make it ordered, meaning numbered, use `<ol> ... </ol>`.
  `<li>` here stands for list item and does not need to be changed.
To create *hyperlinks*, the `<a>` element is used: 
```html
  <a href="https://www.example.com">Click here</a>
```

### Global vs Local Attributes

As we said, attributes can be used to specify elements further and to provide additional information. 
**Global attributes** are attributes that can be applied to any HTML element, making them quite important and essential: 
- `id` is used to give an element a unique identifier within the current HTML file. It is a very useful attribute to have, especially, to access elements with JavaScript.
- the `class` attribute can be used to access all elements that belong to a particular class. The class names are arbitrary and can be defined by the developer as per his needs. An element can belong to multiple classes: 
```html
<div class="container highlight"></div>
```
- `style` is used to add inline CSS directly to an element
- `title` is used to give users extra information if hovering over an element
- `lang` specifies the language of the element
- `hidden` hides an element
- `data_*` can be used to store information inside an element, i.e. `data_name`, `data_age`, ...
- `onclick` and `onmouseover` can trigger JavaScript functions, to dynamically respond to user input.

