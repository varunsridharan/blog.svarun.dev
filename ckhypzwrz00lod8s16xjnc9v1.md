## domQ - Lightweight Wrapper For VanillaJS

## What ❓ 
[domQ] is an absurdly small jQuery alternative for modern browsers (IE11+) that provides jQuery-style syntax for manipulating the DOM. Utilizing modern browser features to minimize the code base, developers can use the familiar chain-able methods at a fraction of the file size. 100% feature parity with jQuery isn't a goal, but [domQ] comes helpfully close, covering most day to day use cases.

## Why 🤔 

>   I was very bored with jQuery script and wanted to try something else 🙈.

Well as a web developer i wanted to move out from jQuery and use Vanilla JS. When i realized i had to write multiple lines of code for a single action thats when i decided to create a lightweight JavaScript library that can do most things that jQuery can.

> [domQ] Uses [Dizzle] which is an alternate to jQuery's Sizzle Framework which is used for Customized CSS Selectors like `:input`, `:hidden` and [Dizzle] is bundled along with [domQ]. we both standalone & bundled versions.


## Comparison

| Size | domQ | domQ + Dizzle | Zepto | jQuery Slim |
| :--- | :--- | :---: | :---: | :---: |
| Unminified | 45.7 KB | 77.1 KB | 58.7 KB | 250 KB | 
| Minified | 20.5 KB | 31.4 KB | 26 KB | 70.6 KB |
| Minified & Gzipped | 7.50 KB | 11.1 KB | 9.8 KB | 24.4 KB |

| Features | domq | domQ + Dizzle  | Zepto | jQuery Slim |
| --- | --- |  :---: |  :---: |  --- |
| Older Browsers | ❌ | ❌ | ❌ | ✔ |
| Modern Browsers | ✔ | ✔ | ✔ | ✔ |
| Actively Maintained | ✔ | ✔ | ❌ | ✔ |
| Namespaced Events | ✔ | ✔ | ❌ | ✔ |
| jQuery Selectors | ✔ | ✔ | ⚠️(Experimental Feature)| ✔ |
| ** Animation | ✔ | ✔ | ⚠️(Custom Workaround) ️| ❌ |


** domQ uses [WebAnimation's](https://github.com/web-animations/web-animations-js) API


domQ gives you a query selector, collection methods and some library methods. If you need more details about our API just check out jQuery's, while we don't implement everything that jQuery provides, everything what we do implement should be compatible with jQuery. domQ can be extended with custom methods, read how [here](https://domq.sva.wiki/developer-guides/extending-domq)

> [domQ] is stable but we still lack documentation. !! if you need help you can contact me directly !

%[https://github.com/domq-js/core]

---

%%[blog-footer]

---

[domQ]: https://github.com/domq-js/core
[dizzle]: https://github.com/varunsridharan/dizzle