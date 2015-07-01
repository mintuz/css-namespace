# CSS Namespace

Namespaces in CSS don't exist and recently their has been interest within the community to try and resolve the issues caused by CSSs global nature.

By no means does this mixin prevent developers from modifying a style class directly, but by adopting a few coding best practices with this mixin, it will allow you to isolate styles to a particular component and stop styles leaking into other components.

## Install

## Usage

All namespaces are defined with a data attribute on the HTML element

```
<div data-namespace="test-namespace"></div>
```

Then create a file per namespace and use the following code

```
@include css-namespace('test-namespace') {
  
  background-color: red;
  
  .test {
    background-color: yellow;
  }
}
```

If you define a css-namespace twice, it will throw a warning in your terminal.

## Warning
This mixin does increase the CSS specificity of classes which isn't ideal but it doesn't override it so much that it is problematic. If you only work within the namespaced files, you will be fine. 

Problems will start to occur if you try overriding something outside of the namespace file, but you shouldn't be doing that anyways. That's the whole point of namespaces ;) 