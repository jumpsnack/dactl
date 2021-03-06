---
layout: post
title: 'Callback methods of Angular'
tags:
  - angular
  - typescript
description: >
  A basic decription of Callback methods of Angular
hero: https://picsum.photos/g/1280/720/?image=1
overlay: orange
published: true
---

## ngOnChanges( )
Called when a parent component modifies (or initializes) the values bound to the input properties of a child. If the component has no input properties, `ngOnChages()` isn’t invoked. If you wish to implement a custom chage-detection algorithm, it must be placed in `DoCheck()`. But implementing manual changes detection there may be costly, because `DoCheck()` is invoked after every chage-detection cycle.

## ngOnInit( )
Invoked after the first invocation of `ngOnChanges()`, if any. Although you might initialize some component variables in the constructor, the properties of the component aren’t ready yet. By the time `ngOnInit()` is invoked the component’s properties will have been initialized.

## ngAfterContentInit( )
Invoked when the child component's state is initialized, if you used the `ngContent` directive to pass some HTML code to it.

## ngAfterContentChecked( )
Invoked on the child component that used `ngContent` after it gets the content from the parent (or during the chage-detection phase), if the bindings used in `ngContent` chage.

## ngAfterViewInit( )
Invoked when the binding on the component's template is complete. The parent component is initialized first, and , if it has children, this callback is invoked after all children are ready.

## ngAfterViewChecked( )
Invoked when the chage-detection mechanism checks whether here are any changes in the component template’s bindings. This callback may be called more than once as the result of modifications in this or other components.

---

Whenever you see the word Content in the name of the lifecycle callback method, that method is applied if content is projected using `<ng-content>`. When you see the word View in the name of the callback method, it applies to the template of the component.
