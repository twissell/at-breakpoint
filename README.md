#at-breakpoint
easy media queries for stylus

## Config

define your breakpoints in the breakpoints hash inside breakpoints.styl, breakpoints has a name and are defined by a string indicating the feature and a value establishing when the condition will trigger. There are two shortcuts for common media features like min and max width.

```
  $bps = {
    'xs': 349px,                     // (min-width: 349px)
    'sm': 350px 779px,               // (min-width: 350px) and (max-width: 779px) 
    'md': in-resolution 2dppx 780px  // (in-resolution: 2dppx) and  (min-width: 780px)
  }
```

## Usage

at-breakpoint is very easy to use, just call the mixin as a block inside any css selector width the name of the breakpoint as paremeter.

```
.foo
  margin: 0
  padding: 0
  +at-breakpoint('sm')
    display: block

```
renders

```
.foo {
  margin: 0;
  padding: 0;
};

@media screen and (min-width: 350px) and (max-width: 779px) {
  .foo {
    display: block;
  }
};
```

### create new breakpoints on the flow

you don't need to define a new breakpoint in the $bps hash, you can do it when you want to use that new breakpoint, at-breakpoint will add it for you to the $bps hash, the only thing you need
is pass the name of the breakpoint and a features string.

```
.foo
  margin: 0
  padding: 0
  +at-breakpoint('xl', 1560px)
    display: table
```

### print classes with breakpoint suffix

here is where at-breakpoint is slighty different for other media querie libraries, it allows you to output a css class with a suffix representing the breakpoint name of the media querie, just
pass suffix:true to at-breakpoint.

```
.foo
  +at-breakpoint('xs', suffix:true)
    display: block
```

renders

```
@media screen and (min-width: 349px) {
  .foo-xs {
    display: block;
  };
};
```

additionaly you can print a class inside all breakpoints as follows.

```
.foo
  +at-breakpoint('all', suffix:true)
    display: inline-block;
    vertical-align: top
```

renders

```
@media screen and (min-width: 349px) {
  .foo-xs {
    display: inline-block;
    vertical-align: top;
  };
};

@media screen and (min-width: 350px) and (max-width: 779px) {
  .foo-sm {
    display: inline-block;
    vertical-align: top;
  };
};
```
