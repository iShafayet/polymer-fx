
# `abstract class FxElement extends Polymer.Element`
`FxElement` extends `Polymer.Element` from Polymer Project and adds in a number of utilities. This class is meant to be extended in the same way you would extend `Polymer.Element`.

**Example:** 

Instead of 
```js
class MyCustomElement extends Polymer.Element 
```
Now you do
```js
class MyCustomElement extends FxElement 
```

# static methods

## static mixin(...behaviors)
Mixes one or more behaviors (aka Polymer Mixins) into the *current* class. 

**Example:** 

```js
class MyCustomElement extends FxElement.mixin(MyDbBehavior, MyHttpBehavior)
```

## static getOwnTemplate()
Returns the template of *current* class. Bypasses Polymer's `static get template` getter.

For en example see the one for `insertExternalTemplate` below.

## static insertExternalTemplate(externalTemplate, insertionPointQuery)
Inserts an external template (any external template node with a content property will do) into the template of *current* class at the node specified by `insertionPointQuery`. `insertionPointQuery` is a query selector.

**Example:** 

```html
<template>
  <div>Local Content</div>
  <!-- content from FxDialogBehavior's template will be inserted here -->
  <div class="super-class-insertion-point"></div>
</template>
```
```js
class MyCustomElement extends FxElement.mixin(FxDialogBehavior){
  static get template() {
    this.insertExternalTemplate(FxDialogBehavior.template, '.super-class-insertion-point');
    return this.getOwnTemplate();
  }
}
```

# methods

## elem(query)
Equivalent to `this.shadowRoot.querySelector(query);`

**Example:** 

```js
hideButton(){
  this.elem('#myButton').hidden = true;
}
```

## elemAll(query)
Equivalent to `this.shadowRoot.querySelectorAll(query);`

**Example:** 

```js
hideButtons(){
  this.elemAll('.myButton').foreach(el => el.hidden = true);
}
```

## resetProperties(...propertyList)
It will reset those *own* properties of an element to the initial value.

**Example:** 

```js
static get properties(){
  return {
    myForm: {
      type: Object,
      value: () => {
        name: '',
        email: '',
        password: ''
      }
    }
  }
}
clearForm(){
  this.resetProperties('myForm');
}
```

## forceRefreshModel(path, temporaryReplacementValue = null) 
It will forcefully re-render the view related the model specified by the `path`. `path` is anything you can pass to Polymer's `this.set`.

For Arrays, you should specify the second parameter as `[]`.

**Example:** 

```js
static get properties(){
  return {
    userList: {
      type: Array,
      value: () => [
        {
          name:{
            first: "John",
            last: "Doe"
          }
        }
      ]
    }
  }
}
clearForm(){
  this.userList[0].name.first = "Jane";
  this.forceRefreshModel('userList', []);
}
```

## log
A helper method that in turn calls `console.log`. Has the same signature. If the current element or it's parent element has a property called `mode`, it will use that value to decide whether to output the parameters to console or not. If mode is set to `development`, it will output the content to console.


**Example:** 

```js
somethingHappened(data){
  // instead of 
  console.log("That happened", data);
  // if you do
  this.log("That happened", data);
  // then it will only be shown to console if this.mode === 'development'
}
```
# attributes

none

# properties

none

# fields

### mode
You may specify `this.mode = 'production'` to indicate that current app is in production.
