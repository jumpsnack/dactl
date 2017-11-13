---
layout: post
title: How to implement the GoogleMap API on the Angular
tags:
  - angular
  - typescript
  - googlemap
hero: https://picsum.photos/1280/720/?image=741
overlay: brown
published: true
---

# Setting up Angular Google Maps
===
  
1. ### Install Angular Google Maps

{% highlight bash %}
{% raw %}
$ npm install @agm/core --save
{% endraw %}
{% endhighlight %}


  
2. ### Setup @NgModule
open src/app.module.ts and import the `AgmCoreModule`
++You need to provide a Google Maps API key to be able to see a Map++

{% highlight typescript %}
{% raw %}
...
import { AgmCoreModule } from '@agm/core';

@NgModule({
imports:[
  ...,
  AgmCoreModule.forRoot({
    apiKey: 'YOUR_KEY_HERE'
  })
],
...
})
export class AppModule{}

{% endraw %}
{% endhighlight %}


  
3. ### Extending the app component

{% highlight typescript %}
{% raw %}

import { Component } from '@angular/core';

@Component({
selector: 'app-root',
templateUrl: 'app.component.html',
styleUrls: ['app.component.css']
})
export class AppModule{
lat: number = 30.4564;
lng: number = 7.80546;
}

{% endraw %}
{% endhighlight %}


  
4. ### Setup the template
Open the file src/app/app.component.html and paste the following content:

{% highlight html %}
{% raw %}

<agm-map [latitude]="lat" [longitude]="lng" style="height: 300px;">
  <agm-marker [latitude]="lat" [longitude]="lng"></agm-marker>
</agm-map>

{% endraw %}
{% endhighlight %}
*CSS Styling is mandatory!*
