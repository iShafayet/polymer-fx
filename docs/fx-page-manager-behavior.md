
# `mixin FxPageManagerBehavior`
`FxPageManagerBehavior` is a mixin. It adds an arbitrary "Page Title"/"Brand Title" management interface that you can use in your titlebar. It adds compatibilty of the FxPage elements by creating some callbacks in addition to those provided by polymer. (Such as `onNavigateIn`, `onNavigateOut` etc)

**Example:** 

```js
class MyApp extends FxApp.mixin(FxPageManagerBehavior) {
  
}
```

# methods

## pushPageTitle(title)
See example below

## popPageTitle()
See example below

## replacePageTitle(title)
See example below

## $getPageTitle(pageTitleListLength)
**Example:** 

In your app-header
```html
<app-header slot="header">
  <app-toolbar>
    <div main-title>[[$getPageTitle(pageTitleList.length)]]</div>
  </app-toolbar>
</app-header>
```

Somewhere in your code
```js
this.pushPageTitle('My App');
```

When you navigate into another page
```js
this.pushPageTitle('Settings');
```

When you navigate out of that page
```js
this.popPageTitle();
```

See the starter kit for a live example.


## _notifyPageSelect(pageElement)
You need to call this method to notify that a page has been selected. pageElement is a instance that is a subclass of `FxPage`. It will ensure the following callbacks are invoked correctly in the `FxPage`.

* onFirstNavigation
* onNextNavigation
* onNavigateIn
* onNavigateOut

**Example:** 

```html
<iron-pages on-iron-select="mainIronPagesIronSelected" ...>
  <page-home name="home"></page-home>
  ...
</iron-pages>
```

```js
mainIronPagesIronSelected(e, details) {
  if (e.target.nodeName !== 'IRON-PAGES') return;
  if (!details.item) return;
  this._notifyPageSelect(details.item);
}
```

See the starter kit for a live example.

# used up internal names
Listed here so that you don't create naming collisions.

* pageTitleList
* _pageReady