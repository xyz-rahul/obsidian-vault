Closures
![[closures.png]]
if a nested funtion is called lexcial envrionment surronding that fun is executed but not that function


# Local Storage
Local storage has no expiration date. It is available for multiple sessions. Your data remains in localStorage till you delete it manually. Local storage is commonly used to store the theme(dark/light/other) in the web pages, save notes in a notes app.
https://dev.to/gautham495/learn-about-using-localstorage-in-javascript-and-react-216g
![[Pasted image 20230921015801.png]]
## Session Storage:

In session storage, the data is stored for one session. As the user opens a new tab, the browser creates a new session and when the user closes the browser tab, the data in the sessionStorage gets deleted.



# [Local Storage vs Cookies](https://stackoverflow.com/questions/3220660/local-storage-vs-cookies)
https://stackoverflow.com/q/3220660/21329968
1780

[Q](https://stackoverflow.com/posts/3220802/timeline)
https://stackoverflow.com/a/3220802/21329968
Cookies and local storage serve different purposes. Cookies are primarily for reading **server-side**, local storage can only be read by the **client-side**. So the question is, in your app, who needs this data — the client or the server?

If it's your client (your JavaScript), then by all means switch. You're wasting bandwidth by sending all the data in each HTTP header.

If it's your server, local storage isn't so useful because you'd have to forward the data along somehow (with Ajax or hidden form fields or something). This might be okay if the server only needs a small subset of the total data for each request.

_**You'll want to leave your session cookie as a cookie either way though.**_

As per the technical difference, and also my understanding:

1. Apart from being an old way of saving data, Cookies give you a limit of **4096** bytes (4095, actually) — it's per cookie. Local Storage is as big as **10MB per domain** — **[this Stack Overflow question](https://stackoverflow.com/questions/2989284/max-size-of-localstorage-values)** also mentions it.
    
2. `localStorage` is an implementation of the `Storage` Interface. It stores data with **no expiration date**, and gets cleared **only** through JavaScript, or clearing the Browser Cache / Locally Stored Data — unlike cookie expiry.



# Immediately Invoked Function Expressions (IIFE)

```js
(
		async	funtion(){
	 //...write code here
		}
)()
```


```js
(function () {
  // …
})();

(() => {
  // …
})();

(async () => {
  // …
})();

```



# [What is event bubbling and capturing?](https://stackoverflow.com/questions/4616694/what-is-event-bubbling-and-capturing)

https://stackoverflow.com/a/4616720/21329968
Event bubbling and capturing are two ways of event propagation in the HTML DOM API, when an event occurs in an element inside another element, and both elements have registered a handle for that event. The event propagation mode determines in [which order the elements receive the event](http://www.quirksmode.org/js/events_order.html).

With bubbling, the event is first captured and handled by the innermost element and then propagated to outer elements.

With capturing, the event is first captured by the outermost element and propagated to the inner elements.

Capturing is also called "trickling", which helps remember the propagation order:

> trickle down, bubble up


![[Pasted image 20230921021019.png]](https://stackoverflow.com/a/67346472/21329968)


https://stackoverflow.com/a/30233082/21329968
I have found this [tutorial at javascript.info](http://javascript.info/tutorial/bubbling-and-capturing) to be very clear in explaining this topic. And its 3-points summary at the end is really talking to the crucial points. I quote it here:

1. Events first are captured down to deepest target, then bubble up. In IE<9 they only bubble.
2. All handlers work on bubbling stage excepts `addEventListener` with last argument `true`, which is the only way to catch the event on capturing stage.
3. Bubbling/capturing can be stopped by `event.cancelBubble=true` (IE) or `event.stopPropagation()` for other browsers.


# Debounce And Throttle
https://youtu.be/cjIswDCKgu0

https://stackoverflow.com/a/25991510/21329968
- **Throttling** will delay executing a function. It will reduce the notifications of an event that fires multiple times.
- **Debouncing** will bunch a series of sequential calls to a function into a single call to that function. It ensures that one notification is made for an event that fires multiple times.
You can visually see the difference [here](https://web.archive.org/web/20220117092326/http://demo.nimius.net/debounce_throttle/)

If you have a function that gets called a lot - for example when a resize or mouse move event occurs, it can be called a lot of times. If you don't want this behaviour, you can **Throttle** it so that the function is called at regular intervals. **Debouncing** will mean it is called at the end (or start) of a bunch of events.