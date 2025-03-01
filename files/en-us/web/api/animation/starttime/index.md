---
title: Animation.startTime
slug: Web/API/Animation/startTime
page-type: web-api-instance-property
browser-compat: api.Animation.startTime
---

{{ APIRef("Web Animations") }}

The **`Animation.startTime`** property of the {{domxref("Animation")}} interface is a double-precision floating-point value which indicates the scheduled time when an animation's playback should begin.

An animation's **start time** is the time value of its {{domxref("timeline", "DocumentTimeline")}} when its target {{domxref("KeyframeEffect")}} is scheduled to begin playback. An animation's **start time** is initially unresolved (meaning that it's `null` because it has no value).

## Value

A floating-point number representing the current time in milliseconds, or `null` if no time is set. You can read this value to determine what the start time is currently set at, and you can change this value to make the animation start at a different time.

## Examples

In the [Running on Web Animations API example](https://codepen.io/rachelnabors/pen/zxYexJ?editors=0010), the we can sync all new animated cats by giving them all the same `startTime` as the original running cat:

```js
const catRunning = document
  .getElementById("withWAAPI")
  .animate(keyframes, timing);

/* A function that makes new cats. */
function addCat() {
  const newCat = document.createElement("div");
  newCat.classList.add("cat");
  return newCat;
}

/* This is the function that adds a cat to the WAAPI column */
function animateNewCatWithWAAPI() {
  // make a new cat
  const newCat = addCat();

  // animate said cat with the WAAPI's "animate" function
  const newAnimationPlayer = newCat.animate(keyframes, timing);

  // set the animation's start time to be the same as the original .cat#withWAAPI
  newAnimationPlayer.startTime = catRunning.startTime;

  // Add the cat to the pile.
  WAAPICats.appendChild(newCat);
}
```

## Reduced time precision

To offer protection against timing attacks and fingerprinting, the precision of `animation.startTime` might get rounded depending on browser settings.
In Firefox, the `privacy.reduceTimerPrecision` preference is enabled by default and defaults to 20 µs in Firefox 59; in 60 it will be 2 ms.

```js
// reduced time precision (2ms) in Firefox 60
animation.startTime;
// 23.404
// 24.192
// 25.514
// …

// reduced time precision with `privacy.resistFingerprinting` enabled
animation.startTime;
// 49.8
// 50.6
// 51.7
// …
```

In Firefox, you can also enabled `privacy.resistFingerprinting`, the precision will be 100ms or the value of `privacy.resistFingerprinting.reduceTimerPrecision.microseconds`, whichever is larger.

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [Web Animations API](/en-US/docs/Web/API/Web_Animations_API)
- {{domxref("Animation")}}
- {{domxref("Animation.currentTime")}} for the current time of the animation.
