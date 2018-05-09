---
layout: post
title: Segment tree
tags:
  - Data structure
hero: https://picsum.photos/1280/720/?image=195
overlay: purple
published: true
---

## INTRODUCTION
+ ### 특징
부모 노드들이 리프 노드들의 값에 대한 연속적인 구간의 합을 유지하고 있는 트리 형태
1. Root는 모든 리프 노드들의 값을 대표한다
2. 각 리프 노드들은 각각의 단일 값을 갖는다
3. 내부 노드들은 각 리프들의 구간을 대표한다
+ ### Time complexity
트리 생성 = O(n)
쿼리 호출(Worst case) = O(nlgn)

{% highlight bash %}
{% raw %}
$ npm install @agm/core --save
{% endraw %}
{% endhighlight %}

  
  
+ ### Setup @NgModule
open src/app.module.ts and import the `AgmCoreModule`  
**_You need to provide a Google Maps API key to be able to see a Map_**

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

  
  
+ ### Extending the app component

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

  
  
+ ### Setup the template
Open the file src/app/app.component.html and paste the following content:

{% highlight html %}
{% raw %}

<agm-map [latitude]="lat" [longitude]="lng" style="height: 300px;">
  <agm-marker [latitude]="lat" [longitude]="lng"></agm-marker>
</agm-map>

{% endraw %}
{% endhighlight %}
**CSS Styling is mandatory!**
