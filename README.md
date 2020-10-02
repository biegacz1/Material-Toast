# Material-Toast
A simple plugin to display a material concept toast (alert message).

**[DEMO](https://dmuy.github.io/Material-Toast/)**

Larger screen layout:

![Material-Toast on large screens](https://i.imgur.com/XGTI6Kd.png "Material-Toast large screen layout")

Smaller screen layout:

![Material-Toast on small screens](https://i.imgur.com/5hjXb8X.png "Material-Toast smaller screen layout")


## Installation
### NPM
Install via npm:
```
npm i @dmuy/toast
```

Include in your app
```javascript
import '@dmuy/toast/dist/mdtoast.css'
import mdtoast from '@dmuy/toast'
```

### CDN
Use the following if you don't want to host the `js` and `css` files:
#### [UNPKG](https://unpkg.com/)
```
https://unpkg.com/@dmuy/toast@{version}/dist/mdtoast.css
https://unpkg.com/@dmuy/toast@{version}/dist/mdtoast.js
```
#### [jsDelivr](https://www.jsdelivr.com/features#gh)
```
https://cdn.jsdelivr.net/gh/dmuy/Material-Toast@{version}/dist/mdtoast.css
https://cdn.jsdelivr.net/gh/dmuy/Material-Toast@{version}/dist/mdtoast.js
```
For production, use the minified version by adding `.min` to the file name (i.e. `mdtoast.min.js`)

***Note: Replace `{version}` with the version you want to use.***

### Local Copy
Copy `mdtoast.css` and `mdtoast.js` (or the minified versions `*.min.js` and `*.min.css`) in the `dist` folder and include in your app:
```html
<link rel="stylesheet" type="text/css" href="{path-to}/mdtoast.css">
<script type="text/javascript" src="{path-to}/mdtoast.js"></script>
```
***Note: Replace `{path-to}` with the absolute or relative path to where you copied the css and js files.***

## Options
You can add options when calling `mdtoast()` to fit your needs. Below are the options you can use:

| Option      | Defaut       | Description  |
| ----------- |--------------|--------------|
| init        | `false`      | Determines if toast is initialize-only (meaning toast will not show unless `show()` is called |
| duration    | `5000`       | Determines the toast display duration (in milliseconds). |
| type        | `default`    | Determines the type of toast to display. Other types in `mdtoast`: `INFO`, `WARNING`, `SUCCESS`, `ERROR`. <br> Or you can just type these string values: `info`, `warning`, `success`, `error`. |
| modal       | `false`      | Determines if toast is modal (pointer events on other elements will be disabled). |
| interaction | `false`      | Determines if toast requires user interaction to dismiss or has some sort of user interaction button to click. |
| interactionTimeout | `null` | Determines the toast duration (timeout to dismiss) if `interaction` is set to `true`. This overrides the `duration` option if `interaction` is set to `true`. |
| actionText  | `OK`         | The action text to display for user interaction (e.g. `UNDO` -> showing toast after archiving items and giving the user an option to undo archiving.) |
| action      | `hide()`     | This will be the function to be called when the user clicks the action text. The default calls the toast's `hide()` method. |
| callbacks   | `{}`         | You can place the callbacks `hidden()` and `shown()` in this option if you have some things to do after the toast is shown or hidden. |

## Usage
Call `mdtoast()`:
```javascript
// Initializes and shows default toast or with the 'new' keyword - i.e new mdtoast(...)
mdtoast('This is a toast message.');
```

### Using configurations
Below is an example of storing your toast in a variable for future reuse:
```javascript
// Initializes default toast with duration of 10 seconds (this will not show the toast since init is set to true)
var myToast = mdtoast('This is a toast message.', { duration: 10000, init: true }); 

// Displays the toast
myToast.show();
```

Different types of toast:
```javascript
// Initializes different toasts with duration of 10 seconds
mdtoast('This is an info toast.', { duration: 10000, type: mdtoast.INFO });      // or type: 'info'
mdtoast('This is an error toast.', { duration: 10000, type: mdtoast.ERROR });    // or type: 'error'
mdtoast('This is a warning toast.', { duration: 10000, type: mdtoast.WARNING }); // or type: 'warning'
mdtoast('This is a success toast.', { duration: 10000, type: mdtoast.SUCCESS }); // or type: 'success'
```

Specifying toast action:
```javascript
// Initializes a toast with action (this toast will not dismiss unless 'interactionTimeout' is specified)
mdtoast('Message archived.', {
  type: 'success', 
  interaction: true, actionText: 'UNDO', 
  action: function(){
    //TODO: Undo codes here...
    this.hide(); // this is the toast instance
  }
});
```

### Remember
Comment or remove the line shown below in the css file if you already have a link to the Roboto font.
```css
@import url('https://fonts.googleapis.com/css?family=Roboto:400,500');
```

Older browsers may need the [classList polyfill](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList) which extends classList support back to IE8 (natively, it’s IE10+).
