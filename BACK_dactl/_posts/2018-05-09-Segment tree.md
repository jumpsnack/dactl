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

## Sequential
9, 4, 3, 2, 1, 4, 5, 6, 7, 10 가 있을 때 a번재 수 부터 b번째 수 까지 합을 구하는 상황을 가정한다.

1번째 수 부터 3번째 수 까지의 합을 구하는 연산을 수행하면
9 + 4 + 3 = 16
2번째 수 부터 5번째 수 까지의 합을 구하는 연산을 수행하면
4 + 3 + 2 + 1 = 10

위 처럼 매번 a번째 부터 b번째 까지 Sequential하게 구하게 된다.
이 때, 최악의 경우를 가정해 n개의 수와 m번의 연산에 대해 O(nm)의 시간복잡도를 가지게 된다.

## Array
이 과정을 달리 생각하면 배열을 이용해 해결할 수 있다.
배열 sum의 각 인덱스는 1번째 부터 i번째 수 까지의 합을 나타낸다.

위 숫자들을 바탕으로 배열을 다음과 같이 정의할 수 있다.
sum[1] = 9      sum[2] = 13
sum[3] = 16     sum[4] = 18
sum[5] = 19     sum[6] = 23
sum[7] = 28     sum[8] = 34
sum[9] = 41     sum[10] = 51

이제 다시 a번째 수 부터 b번째 수 까지 구하는 과정을 가정하자.

2번째 수 부터 4번째 수 까지의 합을 구하는 연산은
sum[4] - sum[1] = 9
1번째 수 부터 10번째 수 까지의 합을 구하는 연산은
sum[10] - sum[0] = 51

위의 경우 sum배열에 대한 전처리에 O(n)이 걸리고 각 질의 M개에 대해 최대 O(1)의 연산이 필요하므로 총 시간복잡도는 O(n + M)으로 이전 방법보다 개선된 성능을 보인다.

* k번째 수가 변경될 때.

10개의 수에 대해 k번째 수를 변경하는 상황이 발생할 수 있다.
1. 3번째 수를 4로 변경하고 3~6번째 수를 구하는 연산
2. 4번째 수를 -10으로 변경하고 1~4번째 수를 구하는 연산

이 경우 바뀐 수를 기준으로 매번 나머지 값을 모두 바꿔줘야 하기 때문에 O(n)번의 연산이 매 연산마다 발생하게 된다.

## Segment tree
Segment tree란 구간을 대표하는 값을 Tree형태로 저장하는 자료구조이다.
각 노드는 자식 노드들을 대표하는 값을 가진다.
10개의 수를 나타내는 Segment tree를 아래와 같이 인덱스를 이용한 그림으로 나타낼 수 있다. 그림의 각 노드는 각각이 대표하고 있는 구간의 범위를 보여주고 있다.
구간 a~b를 대표하는 노드의 왼쪽은 a~(a+b)/2를, 오른쪽 자식은 (a+b)/2+1~b 구간을 대표한다.

![400x200](/assets/img/segment tree/tree1.png "tree image")

위 그림을 이용해 10개의 수를 직접 표기하면 다음과 같다.

![400x200](/assets/img/segment tree/tree2.png "tree image")

### Segment tree에서 합 구하기.
Segment tree에 대해 특정 구간에 대한 연산이 요청된 경우 어떤 대표값들이 선택되는지 나타내면 다음과 같다.
1. 1~4 구간의 합
1~4 구간은 초록색으로 나타낸 하나의 대표노드로 값을 구할 수 있다. 합은 18
![400x200](/assets/img/segment tree/tree3.png "tree image")
2. 2~6 구간의 합
2~6 구간은 초록색으로 나타낸 2, 3~4, 5~6 세개의 대표노드로 합을 구할 수 있다. 합은 4+5+5 = 14
![400x200](/assets/img/segment tree/tree4.png "tree image")

Segment tree에서 합을 구하는 연산의 Time complexity는 O(logn)이다.
이진 트리인 Segment tree는 높이 만큼 대표노드가 최대로 선택될 수 있기 때문이다.

### Segment tree에서 값 갱신.
값이 갱신되면 그 값을 대표하는 모든 노드들의 값도 수정해야 한다.
1. 7번째 수를 6으로 갱신할 때
![400x200](/assets/img/segment tree/tree5.png "tree image")
2. 4번째 수를 10으로 갱신할 떄
![400x200](/assets/img/segment tree/tree6.png "tree image")

Segment tree에서 하나의 값을 갱신하는 연산의 Time complexity는 O(logn)이다.
이진 트리인 Segment tree의 높이 만큼 대표노드가 최대로 선택될 수 있기 때문이다.

* Lazy propagation.

값을 갱신요청 즉시 모두 변경하지 않고 결과에 직접적인 영향을 미치는 값들만 우선적으로 변경해 연산횟수를 낮추는 기법이다.
2번째 값에 대해 +5 연산을 수행한 후 2~4구간의 값을 찾는 과정이다.
1. 먼저 구간 2~4를 대표하는 노드를 찾아서 출발
![400x200](/assets/img/segment tree/tree7.png "tree image")
2. Lazy가 있는 부모노드를 만날 경우 Lazy를 해당 노드에 반영하고 아래쪽에 저나시켜준 뒤 동일한 Lazy가 두 번 전파되지 않도록 Lazy를 0으로 수정한다.
![400x200](/assets/img/segment tree/tree8.png "tree image")
3. 위 과정을 반복한다.
![400x200](/assets/img/segment tree/tree9.png "tree image")
![400x200](/assets/img/segment tree/tree10.png "tree image")
![400x200](/assets/img/segment tree/tree11.png "tree image")
4. Lazy를 전파하면서 마지막 노드까지 도달하면 올바른 값을 얻을 수 있다.
9 + 5 = 14

* Lazy propagation의 상위 전파.
Lazy를 아래쪽으로 전파시켜 조상노드의 Lazy를 자식노드가 필요로 하는 상황을 해결했다.
하지만, 다음과 같은 연산에서 처리는 다른 방안을 고려해야 한다.
1. 구간 1~2에 5를 더하는 업데이트 발생
2. 구간 1~7의 합을 구하는 질의가 발생

이렇게 위쪽으로 Lazy를 전파해야 하는 상황은 Segment tree를 Root에서 출발하는 재귀함수를 이용해 갱신하면 해결할 수 있다.

갱신하는 함수가 호출되면 이 함수는 왼쪽 자식과 오른쪽 자식에도 재귀적으로 갱신 함수를 호출한다.
{% highlight C %}
{% raw %}

갱신함수(현재노드){
  
  //Lazy 아래쪽 전파

  갱신함수(왼쪽 자식 노드)
  갱신함수(오른쪽 자식 노드)

  //Lazy 위쪽 전파
  tree[현재노드].value = tree[왼쪽 자식 노드].value + tree[오른쪽 자식 노드].value
}

{% endraw %}
{% endhighlight %}

* Segment tree 구현

  
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
