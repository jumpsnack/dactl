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
### 특징
부모 노드들이 리프 노드들의 값에 대한 연속적인 구간의 합을 유지하고 있는 트리 형태
1. Root는 모든 리프 노드들의 값을 대표한다
2. 각 리프 노드들은 각각의 단일 값을 갖는다
3. 내부 노드들은 각 리프들의 구간을 대표한다

### 용도
- 구간에 속하는 원소들의 합
- 구간에 속한 원소들의 곱
- 구간 원소들 중 최댓값
- 구간 원소들 중 최솟값

### Time complexity
* 트리 생성 = O(n)
* 쿼리 호출(Worst case) = O(nlgn)

{% highlight bash %}
{% raw %}
$ npm install @agm/core --save
{% endraw %}
{% endhighlight %}

  
  
## Basics
### Sequential
9, 4, 3, 2, 1, 4, 5, 6, 7, 10, 2 가 있을 때 a번재 수 부터 b번째 수 까지 합을 구하는 상황을 가정한다.

1번째 수 부터 3번째 수 까지의 합을 구하는 연산을 수행하면
9 + 4 + 3 = 16
2번째 수 부터 5번째 수 까지의 합을 구하는 연산을 수행하면
4 + 3 + 2 + 1 = 10

위 처럼 매번 a번째 부터 b번째 까지 Sequential하게 구하게 된다.
이 때, 최악의 경우를 가정해 n개의 수와 m번의 연산에 대해 O(nm)의 시간복잡도를 가지게 된다.

### Array
이 과정을 달리 생각하면 배열을 이용해 해결할 수 있다.
배열 sum의 각 인덱스는 1번째 부터 i번째 수 까지의 합을 나타낸다.

위 숫자들을 바탕으로 배열을 다음과 같이 정의할 수 있다.
sum[1] = 9      sum[2] = 13
sum[3] = 16     sum[4] = 18
sum[5] = 19     sum[6] = 23
sum[7] = 29     sum[8] = 36
sum[9] = 46     sum[10] = 48

이제 다시 a번째 수 부터 b번째 수 까지 구하는 과정을 가정하자.

2번째 수 부터 4번째 수 까지의 합을 구하는 연산은
sum[4] - sum[1] = 9
1번째 수 부터 10번째 수 까지의 합을 구하는 연산은
sum[10] - sum[0] = 48

위의 경우 sum배열에 대한 전처리에 O(n)이 걸리고 각 질의 M개에 대해 최대 O(1)의 연산이 필요하므로 총 시간복잡도는 O(n + M)으로 이전 방법보다 개선된 성능을 보인다.

* k번째 수가 변경될 때
10개의 수에 대해 k번째 수를 변경하는 상황이 발생할 수 있다.
1. 3번째 수를 4로 변경하고 3~6번째 수를 구하는 연산
2. 4번째 수를 -10으로 변경하고 1~4번째 수를 구하는 연산

이 경우 바뀐 수를 기준으로 매번 나머지 값을 모두 바꿔줘야 하기 때문에 O(n)번의 연산이 매 연산마다 발생하게 된다.

### Segment tree
Segment tree란 구간을 대표하는 값을 Tree형태로 저장하는 자료구조이다.
각 노드는 자식 노드들을 대표하는 값을 가진다.


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
