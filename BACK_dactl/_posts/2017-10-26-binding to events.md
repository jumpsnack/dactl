---
layout: post
title: Binding to events
tags:
  - angular
  - typescript
hero: https://picsum.photos/1280/720/?image=3
overlay: red
published: true
---

To assign an event-handler function to an event, you need to pit the event name in parentheses in thecomponent's template. The following code snippet shows how to bind the function `onClickEvent()` to the click event, and the function `onInputEvent()` to the input event

{% highlight html %}
<button (click) = ‘onClickEvent()’>Get Products</button>
<input placeholder=‘Product name’ (input)=‘onInputEvent()’>
{% endhighlight %}

When the event specified in parentheses is triggered, the expression in double quotes is reevaluated. In the preceding example, the expressions are functions, so they’re invoked each time the corresponding event is triggered.
If you’re interested in analyzing the properties of the event object, add the $event argument to the handler function. In particular, the target property of the event object represents the DOM node where the event occurred. The instance of the event object will be available only within the binding scope (that is, in the event-handler function).
