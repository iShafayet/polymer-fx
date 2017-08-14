
# `mixin FxDialogBehavior`
`FxDialogBehavior` is a mixin. It adds 4 kind of ui elements and their methods to your app.

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


## showPlainToast(message)
Shows a small semi-transparent toast in the bottom left corner.

## showModalDialog(title, message, callback)
Shows a dialog box with an "Okay" button. callback is a function that receives no parameters. It is called when the "Okay" button is pressed.

**Example:** 

```js
this.showModalDialog("Success", "What you wanted is done!", ()=> {
  // user has pressed "Okay"
});
```

## showModalConfirmation(title, message, callback)
Shows a dialog box with an "Okay" an a "Cancel" button. callback is a function that receives one single parameter. it's true if the user presses okay. false otherwise.

**Example:** 

```js
this.showModalConfirmation("Delete?", "Are you sure?", (answer)=> {
  if (answer){
    // delete
  } else {
    // do not delete
  }
});
```

## showModalInput(title, label, defaultValue, callback)
Shows a dialog box with an "Okay" button and an input. callback is a function that receives one single parameter. the value of the input is passed as a parameter. It is false if the user pressed cancel.

**Example:** 

```js
this.showModalInput("Your name?", "If you don't mind", "John Doe", (answer)=> {
  if (answer){
    this.showModalDialog("Great!", "Pleased to meet you");
  } else {
    // Didn't tell you a name.
  }
});
```

# used up ids
Listed here so that you don't create naming collisions.
* generic-modal-input
* generic-modal-dialog
* generic-modal-confirmation
* plain-toast

# used up internal names
Listed here so that you don't create naming collisions.

* genericModalInput
* genericModalDialog
* genericModalConfirmation
* _patchForPolymerModalDialogIssue
* genericModalInputCancelPressed
* genericModalInputDonePressed
* genericModalDialogGotItPressed
* genericModalConfirmationOkayPressed
* genericModalConfirmationCancelPressed


