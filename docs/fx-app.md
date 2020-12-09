
# `abstract class FxApp extends FxElement`
`FxApp` extends `FxElement` and provides a framework for your main element, my-app, app-root or root-element.. This class is meant to be extended in the same way you would extend `Polymer.Element`.

**Example:** 

```js
class MyApp extends FxApp {
  constructor(){
    super();
  }
}
```

`FxApp` has built in methods and properties for navigation.

# static methods

none

# methods

## constructor
It is important that you call `super()` from your `constructor` when you extend `FxApp`.

## abstract _pageNameChanged(pageName)
Your class should define this method `_pageNameChanged(pageName)` where `pageName` is a string containing name of the current path.

**Example:** 

 The navigation strategy is pretty simple. 

`www.mysite.com/user/id:1/banned:false`

If the browser is on the link above, your `_pageNameChanged` will be called with the parameter `pageName` set to `user`. The rest of the path `id:1/banned:false` can be found in `this.subRoute.path`, which you can process using `this.getUrlParameters`.

```js
class MyApp extends FxApp {
  
  _pageNameChanged(pageName){
    doSomethingWithPageName(pageName); // ordoSomethingWithPageName(this.pageName); 
    let params = this.getUrlParameters(this.subRoute.path);
    console.log(params); // { id:1, banned:false }
  }

}
```

## navigateTo(url)
Go to a certain url. Similar to `window.location = url` but handles a few checks internally. You're advised to use it. Note that it is relative unless you specify protocol.

**Example:** 

```js
this.navigateTo('user-details/id:1'); // will go to yoursite.com/user-details/id:1
```

## navigateToPreviousUrl(fallbackUrl)
Go back using window.history. However if there is no history present, it will go to the fallback url. Very useful for modal pages.

**Example:** 
Do this on the back button of a `add-user` page.
```js
this.navigateToPreviousUrl('user-list');
```
That way, even if the user directly opened yoursite.com/add-user, the back button will still function.


## getUrlParameters(path)
Parses the path and summarizes the parameters in an object. 

**Example:** 
See example for `_pageNameChanged`.

## showAlertMessage(title, message)
shows a simple alert in the format `${title}: ${title}`. You can override this class and present your own pretty version.

# attributes

## pageName
`this.pageName` is set before `this._pageNameChanged` is called. See `_pageNameChanged` above.

## subRoute.path
`this.subRoute.path` is set before `this._pageNameChanged` is called. See `_pageNameChanged` above.

## defaultPageName
If you specify `this.defaultPageName` or redefine the property, that name will be used when path is `/` or no path. (i.e. user just navigated to your my.website.com). Default is `home`

# properties

none

# fields

none

# used up internal names
Listed here so that you don't create naming collisions.

* _rootPattern
* _routeData
* _routePageChanged
* _setLocation
