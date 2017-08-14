
# `abstract class FxView extends FxElement`
`FxView` extends `FxView` and provides a structure for custom views with additional callbacks and properties.

**Example:** 

```js
class MyView extends FxView {
  constructor(){
    super();
  }
}
```

# methods

## constructor
It is important that you call `super()` from your `constructor` when you extend `FxView`.

## connectedCallback
Thie element listens to the connectedCallback. So, if you use `connectedCallback` in your custom view, call `super.connectedCallback()` before you do anything in the callback. Otherwise you do not need to be concerned about it.

# lifetime callbacks

`FxView` gets 3 additional lifetime callbacks in addition to those provided by Polymer.

## onceOnActivate()
This callback is invoked when your view is "Activated" for the first time.

## onActivate()
This callback is invoked each time your view is activated. It is invoked even the first time, after onceOnActivate() finishes.

## onDeactivate()
This callback is invoked each time your view is deactivated.

# attributes

## is-active
Bound to the `isActive` property.

# properties

## isActive
`this.isActive` is bound to the `is-active` attribute. It is meant to be set from outside of your view to indicate whether your view is active or not.

## page
`this.page` points to the page this view is a part of.

## app
`this.app` points to the app containing the page this view is a part of.

# Combined Example

In the example below, we demonstrate how we can use a custom view.

```html
<paper-tabs selected="{{paperTabSelectedViewIndex}}" fit-container>
  <paper-tab>View 1</paper-tab>
  <paper-tab>View 2</paper-tab>
</paper-tabs>

<view-1 is-active="[[$equals(paperTabSelectedViewIndex, 0)]]"></view-1>
<view-2 is-active="[[$equals(paperTabSelectedViewIndex, 1)]]"></view-2>
```

```js
class View1 extends FxPage {

  onceOnActivate() {
    this.log('Doing one time setups, i.e. event listeners etc');
    // you have access to this.page and this.app
  }

  onActivate(){
    this.log('View is active');
    // you have access to this.page and this.app
  }

  onDeactivate(){
    this.log('View is no longer active');
    // you have access to this.page and this.app
  }

}
```
