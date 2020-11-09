## How To Update URL Parameters In Javascript Without Reloading?

In this post, we are going to learn how to change ***URL Parameters*** on a page using javascript but without reloading the website. 

### Backstory
When I saw websites updating their ***URL*** when loading content via _Ajax_. I was stunned & confused about how they are updating it.

When I tried using the below code it still reloaded the page. 

```javascript
location.href = 'https://example.com/?param1=value1';
```

So I decided to dig deep to find how it was done. 


I know there are some javascript frameworks such as [vueJS](https://vuejs.org/) which support `url` routing but I wanted to get this done in **VanillaJS** so that I can use it in my applications.

---

## How it's done?
This is a very simple thing to do in VanillaJS using built-in browsers' [History.pushState()](https://developer.mozilla.org/en-US/docs/Web/API/History/pushState).
All We need to do is just update the history with the new URL & Page title

```javascript
function change_url_without_reload( title, url ) {
	if( typeof ( history.pushState ) !== 'undefined' ) {
		history.pushState( { page: title, url: url }, title, url );
	}
}
```

#### MDN Docs
%[https://developer.mozilla.org/en-US/docs/Web/API/History/pushState]

#### Browser Support Status
%[https://caniuse.com/?search=pushState]

### Live Demo
%[https://blog.demo.svarun.dev/how-to-update-url-parameters-in-javascript-without-reloading]

### Source Code
https://github.com/varunsridharan/blog-demos/blob/main/how-to-update-url-parameters-in-javascript-without-reloading/index.html