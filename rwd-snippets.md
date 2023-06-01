# RWD notes:

## Fluid layout
```css
/* fluid font size: The font size will change
   as per the viewport width. */
p,a,h1{
  font-size: clamp(1rem, 0.5rem + 2.5vw, 3rem);
}
```

---

```css
/* Dynamic Gap: With the gap property, we can
   create a dynamic spacing that changes based
   on the viewport or container size.*/
.wrapper {
  display: grid;
  grid-template-columns: repeat(auto-fit,
      minmax(200px, 1fr));
  gap: clamp(1rem, 2vw, 24px);
}
```

---

```css
/* We might need to change the vertical padding
 based on the viewport size. CSS 'clamp()'
 with viewport units is perfect for that. */
.hero {
  padding: clamp(2rem, 10vmax, 10rem) 1rem;
}
```
![vertical padding using clamp()](https://ishadeed.com/assets/responsive-design/use-case-padding.jpg)

---

## Size Container Queries

- It provides us with ways to query the container width of a component.
- Container queries are an alternative to media queries, which apply styles to elements based on viewport size or other device characteristics.

![container queries](https://ishadeed.com/assets/responsive-design/media-query-vs-size-container-query.jpeg)

- for info, see:[mdn CSS container queries](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_container_queries)

- To use container queries:
  -  Declare a containment context on an element by `container-type` property with a value of `size, inline-size`, or `normal`.

      - `size`: The query will be based on the inline and block dimensions of the container. Applies layout, style, and size containment to the container.

      - `inline-size`: The query will be based on the inline dimensions of the container. Applies layout, style, and inline-size containment to the element.
      - `normal`: The element is not a query container for any container size queries, but remains a query container for container style queries.

Example:

```css
/* The following example creates a containment
 context with the name sidebar: */

.post {
  /* Define a container type */
  container-type: inline-size;
  /* set a container name */ 
  container-name: sidebar;
  /* shorthand: {container: sidebar / inline-size;} */
}

/* You can then target this containment context using
 the @container at-rule: */
@container sidebar (min-width: 700px) {
  .card {
    font-size: 2em;
  }
}
```
- The container query length units are:

  - `cqw`: 1% of a query container's **width**
  - `cqh`: 1% of a query container's **height**
  - `cqi`: 1% of a query container's **inline size**
  - `cqb`: 1% of a query container's **block size**
  - `cqmin`: The smaller value of either **cqi** or **cqb**
  - `cqmax`: The larger value of either **cqi** or **cqb**
- The following example uses the cqi unit to set the font size of a heading based on the inline size of the container:
```css
@container (min-width: 700px) {
  .card h2 {
    font-size: max(1.5em, 1.23em + 2cqi);
  }
}
```
