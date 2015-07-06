# CSS Namespace

Namespaces in CSS don't exist and recently their has been interest within the community to try and resolve the issues caused by CSSs global nature.

By no means does this mixin prevent developers from modifying a style class directly, but by adopting a few coding best practices with this mixin, it will allow you to isolate styles to a particular component and stop styles leaking into other components.

## Install

```
bower install css-namespace --save
```

## Usage

By default all namespaces are defined with a data attribute on the HTML element

```
<div data-namespace="test-namespace"></div>
```

Then create a file per namespace and use the following code

```
@import '../bower_components/css-namespace/css-namespace';

@include css-namespace('test-namespace') {
  
  background-color: red;
  
  .test {
    background-color: yellow;
  }
}
```

### CSS Class selector Mode

It is possible to override the default behaviour and instead of outputting the namespace as a data-attribute, use a traditional CSS Class. 

If you are starting a new project, I recommend sticking with the data attribute method.

However this was brought in to support legacy/older projects which have been around for a while and prevent a massive refactor.


```
@import '../bower_components/css-namespace/css-namespace';

@include css-namespace($namespace:'test-namespace', $mode:'class') {
  
  background-color: red;
  
  .test {
    background-color: yellow;
  }
}
```

## CSS Singletons

By default, if you define a css-namespace twice, it will throw a warning in your terminal.
To get round this (maybe you wish to seperate your namespace into different files, use the following code). 

The reason singleton mode is set to true is that in most cases you won't want to alter a CSS Namespace, and should treat them as immutable. 

```
@import '../bower_components/css-namespace/css-namespace';

// File 1

@include css-namespace($namespace:'test-namespace', $singleton:false) {
  
  background-color: red;
  
  .test {
    background-color: yellow;
  }
}

// File 2

@include css-namespace($namespace:'test-namespace', $singleton:false) {
  background-color: blue;
}

```

## Warning
This mixin does increase the CSS specificity of classes which isn't ideal but it doesn't override it so much that it is problematic. If you only work within the namespaced files, you will be fine. 

Problems will start to occur if you try overriding something outside of the namespace file, but you shouldn't be doing that anyways. That's the whole point of namespaces ;) 