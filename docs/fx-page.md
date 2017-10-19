
# `abstract class FxPage extends FxElement`
`FxPage` extends `FxElement` and provides additional callbacks and properties for your pages.

**Example:** 

```js
class MyPage extends FxPage {
  constructor(){
    super();
  }
}
```

# methods

## constructor
It is important that you call `super()` from your `constructor` when you extend `FxPage`. Inside the constructor, `this.app` is initialized to the host element of the page (which is expected to be an instance of `FxApp`).

## confirmPageReady();
This method is important if you want the lifetime callbacks to fire correctly. Inside your constructor, invoke `this.confirmPageReady();` to signal that your page is ready. See the combined example below.

# lifetime callbacks

`FxPage` gets 4 additional lifetime callbacks in addition to those provided by Polymer.

## onFirstNavigateIn()
This callback is invoked when your page is first loaded. You can call `super.onFirstNavigation()` in order to have access to `this.params`. You should do your one time setups here.

## onNextNavigateIn()
This callback is invoked when your page is loaded into view. You can call `super.onNextNavigateIn()` in order to have access to `this.params`.

## onNavigateIn()
This callback is invoked after `onFirstNavigateIn()` or `onNextNavigateIn()` finishes. There is no need to call `super`.

## onNavigateOut()
This callback is invoked when your page is no longer loaded into view.

# properties

## app
`this.app` is initialized in the constructor.

## params
`this.app` is initialized in the `super` calls of `onFirstNavigateIn` or `onNextNavigateIn`. It is same as invoking - 
```js 
var path = this.app.paramString
this.params = this.app.getUrlParameters(path);
```
# Combined Example

In the example below, we demonstrate how we can use the various callbacks. We are assuming that the FxApp this page belongs to has a Service databaseProvider that can give us a list of users.

```js
class UserManagerPage extends FxPage {

  static get properties(){
    return {
      newUserForm: {
        type: Object,
        value: () => [
          {
            name: '',
            password: ''
          }
        ]
      }
    }
  }

  constructor(){
    super();
    this.userList = [];
    this.confirmPageReady();
  }

  _loadUser(){
    this.userList = this.app.databaseProvider.getAll('user');
  }

  onFirstNavigation() {
    super.onFirstNavigation();
    this.app.databaseProvider.observe('user', _ => this._loadUsers())
  }

  onNextNavigation() {
    super.onFirstNavigation();
    this.resetProperties('newUserForm');
  }

  onNavigateIn(){
    this._loadUsers();
  }

  onNavigateOut(){
    this.log('Leaving the page');
  }

}
```
