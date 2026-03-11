# Event Delegation in JavaScript

Event Delegation is a technique in JavaScript where you **attach a single event listener to a parent element** instead of attaching multiple listeners to individual child elements. The parent element catches events from its children using **event bubbling**.

---

## HTML Structure

```html
<ul id="ul"></ul>
<button id="btn">Add List</button>
```

* `<ul>` is the parent element where all `<li>` items will be added dynamically.
* `<button>` is used to add new list items.

---

## JavaScript Code

```javascript
const ul = document.querySelector('#ul');
const btn = document.querySelector('#btn');

let count = 0;

// Add new list items dynamically
btn.addEventListener('click', () => {
    let li = document.createElement('li');
    li.textContent = `New List ${count++}`;
    ul.appendChild(li);
});

// Event delegation: single listener for all list items
ul.addEventListener('click', (e) => {
    if (e.target.tagName === 'LI') {
        console.log(e.target.textContent);
    }
});
```

---

## How It Works

1. When you click the **button**, a new `<li>` element is created and added to the `<ul>`.
2. Instead of adding a click listener to every `<li>`, we attach **one listener to the `<ul>`**.
3. When a `<li>` is clicked:

   * The click event **bubbles** from the `<li>` to the `<ul>`.
   * `e.target` identifies which `<li>` was clicked.
4. The listener logs the content of the clicked `<li>`.

---

## Example Usage

1. Click the button three times. You will get three new list items:

```
New List 0
New List 1
New List 2
```

2. Click **New List 1**, console logs:

```
New List 1
```

---

## Why Event Delegation is Useful

* You don’t need to attach listeners to **each dynamic element**.
* Improves **performance** and **memory usage**.
* Simplifies code when elements are **added dynamically**.

---

## Key Concept

Event Delegation relies on **Event Bubbling**, which means events travel **from child to parent**.
