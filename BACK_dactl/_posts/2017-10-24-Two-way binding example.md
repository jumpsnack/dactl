---
layout: post
title: Two-way binding example
tags:
  - angular
  - typescript
description: >
  presents a brief example about Two-way binding
hero: https://picsum.photos/g/1280/720/?image=23
overlay: orange
published: true
---

## Inner component

### **.ts**

{% highlight typescript %}
@Component({
    selector : 'app-processor',
    template : `
        Buying ((quantity)) share of ((stockSymbol))
    `,
    styles : [':host {background: cyan;}']
})
export class OrderComponent {
    @Input() stockSymbol : string;
    @Input() quantity : string;
}
{% endhighlight %}

## Outer component

### **.ts**

{% highlight typescript %}
@Component(…)

export class AppComponent {
    stock: string;
    onInputEvent({target}) : void {
        this.stock = target.value;
    }
}
{% endhighlight %}

### **.html**

{% highlight html %}
<input type='text' (change)='onInputEvent($event)'></br>
<app-processor [stockSymbol]='stock' [quantity]=100></app-processor>
{% endhighlight %}
