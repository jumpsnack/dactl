---
layout: post
title: Custom pipes
tags:
  - angular
  - typescript
description: >
  presents a brief example and description about Custom pipes
hero: https://picsum.photos/1280/720/?image=223
overlay: purple
published: true
---

Angular offers a simple way to create custom pipes, which can include code specific to your application. You need to create a *`@Pipe`* annotated class that implements the *`PipeTransform`* interface. The *`PipeTransform`* interface has the following signature.

{% highlight typescript %}
export interface PipeTransform {
    transform(value: any, …args: any[]): any;
}
{% endhighlight %}

This tells you that a custom pipe class must implement just one method with the preceding signature. The first parameter of transform takes a value to be transformed, and the second defines zero or more parameters required for your transformation algorithm. The *`@Pipe`* annotation is where you specify the name of the pipe to be used in the template. If your component uses custom pipes, they have to be explicitly listed in its *`@Component`* annotation in the pipes property.
