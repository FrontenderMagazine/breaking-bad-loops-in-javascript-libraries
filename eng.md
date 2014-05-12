# Breaking Bad Loops in JavaScript Libraries)

It was sort of a surprise for me when I discovered inconsistencies in the most
popular JavaScript libraries in how they handle their each and forEach loops.
This post compares:

- forEach Loop in Native JavaScript
- each Loop in Lo-Dash
- each Loop in jQuery
- each Loop in Underscore.js
- forEach Loop in Underscore.js

## forEach Loop in Native JavaScript

JavaScript Libraries are important (e.g., jQuery, Lo-Dash, Underscore), but in
the case of functional loops
(`forEach` and `each`) they create a lot of confusion (for loop can be broken
with ‘break’). Let’s inspect the example of native JavaScript code for the
`forEach` method:

    [1,2].forEach(function(v){
      alert(v);
      return false;
    })

This will display us two alert boxes. Try the native JavaScript code yourself
in[JSFiddle][1].

This is an expected behavior in most cases because with each iteration we
invoke a new function. Unlike the`for (var i=0; i<arr.length; i++) {}` code
that has no function/iterators.

However, in Lo-Dash and jQuery similar code breaks the loops!

## Breaking each Loop in Lo-Dash

The Lo-Dash code with `each` produces only **one alert**:

    _.each([1,2],function(v){
      alert(v);
      return false;
    })

Try the above Lo-Dash code yourself in [JSFiddle][2].

## Breaking each Loop in jQuery

Likewise, the jQuery `each` example shows only the first alert:

    $.each([1,2],function(i, v){
      alert(v);
      return false;
    })

Try the jQuery code yourself in [JSFiddle][3].

## Non-Breaking each Loop in Underscore.js

To complicate the matter, Underscore.js and Backbone.js remain true to the
native JavaScript interpretation.

The Underscore.js `each` example that iterates through the each item and
**doesn’t break**:

    _.each([1,2],function(v){
      alert(v);
      return false;
    })

Try the Underscore `each` method in [JSFiddle][4].

## Non-Breaking forEach Loop in Underscore.js

Just for the sake of it, the Underscore `forEach()` was tested. It reliably
produced the results similar to the native`forEach()`: **two alerts!**

The Underscore `forEach()` code:

    _.forEach([1,2],function(i, v){
      alert(v);
      return false;
    })

Try the Underscrore.js `forEach()` code yourself at [JSFiddle][5].

## The Code-Breaking Difference Between Lo-Dash and Underscore

The conclusion of this brief post is that
**Lo-Dash is not equal to Underscore**,
unless a special underscore-compatible version is being used. This was
kindly pointed out to me by John-David Dalton (@jdalton):

> [@azat_co][6] Right Lo-Dash isn't a drop-in unless you use the Lo-Dash.
> underscore.js build (it's linked to on the homepage). Also in cdnjs.
>
> — John-David Dalton (@jdalton) [November 22, 2013][7]

PS: Underscore.js `forEach` is more browser compatible than native `forEach`
because the latter was a later addition to the JavaScript API and is
[not supported by older browsers][8].

 [1]: http://jsfiddle.net/MMbrR/
 [2]: http://jsfiddle.net/x65jp/2/
 [3]: http://jsfiddle.net/x65jp/3/
 [4]: http://jsfiddle.net/x65jp/1/
 [5]: http://jsfiddle.net/x65jp/4/
 [6]: https://twitter.com/azat_co
 [7]: https://twitter.com/jdalton/statuses/403993905575641088

 [8]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach#Browser_compatibility