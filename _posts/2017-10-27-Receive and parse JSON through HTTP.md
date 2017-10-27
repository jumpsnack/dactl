---
layout: post
title: Receive and parse JSON through HTTP
tags:
  - angular
  - typescript
hero: https://picsum.photos/1280/720/?image=421
overlay: yellow
published: true
---

## Simple HTTP Server

### ts

{% highlight typescript %}
{% raw %}
import * as express from "express";
const app = express();

class Contact {
    constructor(
        public id: string,
        public name: string,
        public email: string
    ) { }
}

const contacts = [
    new Contact('c200', "Ravi Tamada", 'ravi@gmail.com'),
    new Contact('c201', "Johnny Depp", "jhonny@gmail.com"),
    new Contact('c202', "Leonardo Johns", "leonardo@gmail.com"),
    new Contact('c203', "Eddie Kim", "eddie@gmail.com"),
    new Contact('c204', "Anna Pyo", "anna@gmail.com")
];

function getContacts(): Contact[] {
    return contacts;
}

app.get('/', (req, res) => res.redirect('/contacts'));

app.get('/contacts', (req, res) => {
    res.setHeader('Access-Control-Allow-Origin', '*');
    res.json(getContacts());
});

const server = app.listen(4300, "localhost", () => {
    const { address, port } = server.address();
    console.log('Listening on http://locahlost:' + port);
})

{% endraw %}
{% endhighlight %}

Usage:
{% highlight bash %}
$ tsc above file.ts //then generated above file.js
$ node above file.js
Listening on http://localhost:4300
{% endhighlight %}

## Angular Client

### ts
{% highlight typescript %}
{% raw %}
import {Component, OnInit} from '@angular/core';
import {Observable} from 'rxjs/Observable';
import {Http} from '@angular/http';
import 'rxjs/add/operator/map';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})

export class AppComponent implements OnInit {
  contacts: Array<any> = [];
  dataReceiver: Observable<any>;
  
  constructor(private http: Http) {
    this.dataReceiver = this.http.get('http://127.0.0.1:4300/contacts')
      .map(res => res.json());
  }

  ngOnInit(){
    this.dataReceiver.subscribe(
      data => {
        if (Array.isArray(data)) {
          this.contacts = data;
          console.log(this.contacts.toString());
        } else {
          this.contacts.push(data);
          console.log(this.contacts.toString());
        }
      },
      err => console.log('Can\'t get contacts. Error code: %s, URL: %s', err.status, err.url),
      () => console.log('Contacts are retrieved')
    );
  }
}
{% endraw %}
{% endhighlight %}

### html

{% highlight html %}
{% raw %}
<h1>Contacts</h1>
<ul>
  <li *ngFor="let contact of contacts">
    {{contact.id}} / {{contact.name}} / {{contact.email}}
  </li>
</ul>

{% endraw %}
{% endhighlight %}

## Result

![800x400](assets/img/posts/2017-10-27-receive and parse json through http-result.png "result image")

## More simple way

{% highlight typescript %}
{% raw %}
import { Component } from '@angular/core';
import {Observable} from "rxjs/Observable";
import {Http} from "@angular/http";

@Component({
  selector: 'app-http-client',
  template: `
    <h1>All Contacts</h1>
    <ul>
      <li *ngFor="let contact of contacts | async">
        {{contact.name}}
      </li>
    </ul>
  `,
  styles: []
})
export class HttpClientComponent {

  contacts: Observable<Array<string>>;

  constructor(private http: Http) {
    this.contacts = this.http.get('http://localhost:4300/contacts').map(res => res.json());
  }
}
{% endraw %}
{% endhighlight %}
