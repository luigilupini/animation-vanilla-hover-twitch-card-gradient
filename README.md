## Twitch card (Staggering title)

> Here applied is a very cool gradient effect when we hover the card.

![alt text](./capture.png)

Featuring:

- Our card makes use of `vmin` so its responsive at a specified aspect ratio.
- The aspect ratio makes sure it keeps (x/y) proportions.
- The magic is done by maneuvering a gradient `:before` pseudo element.
- We have it absolutely positioned at (h/w) 100% within the card.

```css
.card {
  width: 50vmin;
  aspect-ratio: 5 / 7;
  border: 0.5vmin solid var(--border);
  cursor: pointer;
}
.card:before {
  content: ""; /* Magic gradient here 🪄 */
  position: absolute;
  height: 100%;
  width: 100%;
  left: 0;
  top: 0;
  background: linear-gradient(
    130deg,
    transparent 0% 33%,
    var(--g1) 66%,
    var(--g2) 83%,
    var(--g3) 100%
  );
  background-position: 0% 0%;
  background-size: 280% 280%;
  transition: background-position 500ms ease;
  z-index: 1;
}
/* Hover effect here 🧙‍♂️ */
.card:hover:before {
  background-position: 100% 100%; /* Gradient is pulled back into visibility */
  transform: scale(1.08, 1.03);
}
```

This pseudo gradient/content needs to be larger than the card like (280% 280%)
percent larger so we can animate into it instead. To animate over our absolutely positioned background, we can on `card:hover:before` change position.

```js
// The goal here is to stagger words
const subtitle = document.getElementsByClassName("card-subtitle")[0];

// Function creates a HTML span with class:
const produceSpan = (text, index) => {
  const word = document.createElement("span");
  word.innerHTML = `${text}`;
  word.classList.add("card-subtitle-span"); // see css selector above!
  word.style.transitionDelay = `${index * 40}ms`;
  return word;
};
// Function takes our produced span & appends it in our subtitle element:
// Function takes sentence and splits it in an array:
const subtitleArray = (text) => {
  // console.log(text.split(" "));
  return text
    .split(" ")
    .map((text, index) => subtitle.appendChild(produceSpan(text, index)));
};
subtitleArray(
  "Join a Twitch community! And discover the best live streams anywhere, anytime."
);
```
