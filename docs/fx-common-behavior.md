
# `mixin FxCommonBehavior`
`FxCommonBehavior` is a mixin. It adds some of the most commonly computed functions. Use FxElement.mixin() to use it or apply directly to your class.

**Example:** 

```js
class MyApp extends FxApp.mixin(FxCommonBehavior) {
  
}
```

or 

```js
class MyApp extends FxCommonBehavior(Polymer.Element) {
  
}
```
# methods (computed functions)

## $equals(left, right)
returns true if left === right

**Example:** 

```html
<div hidden="[[!$equals(userType, 'admin')]]">
  ... admin features ...
</div>
```

## $isNull(value)
returns true if value === null

**Example:** 

```html
<div hidden="[[!$isNull(user)]]">
  show user details
</div>
```

## $and(left, right)
returns true if left && right

**Example:** 

```html
<div hidden="[[!$and(user.isHidden, user.isDeleted)]]">
  show user
</div>
```

## $or(left, right)
returns true if left || right

**Example:** 

```html
<div hidden="[[$or(user.isHidden, user.isDeleted)]]">
  show user
</div>
```