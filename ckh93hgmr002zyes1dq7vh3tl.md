## Dizzle - CSS Selector Library

## What is Dizzle?

Dizzle turns CSS selectors into functions that test if elements match them. When searching for elements, testing is executed "from the top", similar to how browsers execute CSS selectors.

## Why I Created this library when jQuery/Sizzle Can do the job? 

Long story short I wanted to move from jQuery to VanillaJS but then I faced a roadblock that I can't use special CSS selectors such as `:input` in VanillaJS to fetch elements due to which I worked on this library. 

## Features:

* Full implementation of CSS 3 & CSS 4 selectors
* Partial implementation of jQuery Extensions
* Pretty good performance
* Light Weight

###  Finding All Input Elements Inside A Form 
```javascript
var $elements = dizzle('div#yourID :input');
console.log($elements);
```

###  Filter Elements 
```javascript
/**
 * Filter All Visible H2 tags
 */
var visibleH2 = dizzle.filter(':visible',dizzle('h2'));
```

%[https://github.com/varunsridharan/dizzle]

---

Questions or feedback?  Please comment below. 

See all my projects at <a href=https://github.com/varunsridharan/>Github</a>.

Follow me on <a href="https://twitter.com/varunsridharan2">Twitter for updates</a>